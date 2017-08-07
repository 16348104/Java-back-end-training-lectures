# 数据库连接池

> 连接池：数据库连接的复用，通过建立一个数据库连接池以及一套连接使用、分配、管理策略，使得该连接池中的连接可以得到高效、安全的复用，避免了数据库连接频繁建立、关闭的开销

> [Wikipedia: Connection pool](https://en.wikipedia.org/wiki/Connection_pool)

>  In software engineering, a connection pool is a cache of database connections maintained so that the connections can be reused when future requests to the database are required.[citation needed] Connection pools are used to enhance the performance of executing commands on a database. Opening and maintaining a database connection for each user, especially requests made to a dynamic database-driven website application, is costly and wastes resources. 

> [Stackoverflow: What is database pooling?](http://stackoverflow.com/a/4041136/3414180)

      +---------+
      |         |
      | Clients |
    +---------+ |
    |         |-+        +------+          +----------+
    | Clients | ===#===> | Open | =======> | RealOpen |
    |         |    |     +------+          +----------+
    +---------+    |         ^
                   |         |
                   |     /------\
                   |     | Pool |
                   |     \------/
                   |         ^
                   |         |
                   |     +-------+         +-----------+
                   #===> | Close | ======> | RealClose |
                         +-------+         +-----------+


- 连接池的建立
  - 在系统初始化时，连接池会根据系统配置建立，并在池中创建了几个连接对象，以便使用时能从连接池中获取
  - 连接池中的连接不能随意创建和关闭，这样避免了连接随意建立和关闭造成的系统开销
  - Java中提供了很多容器类可以方便的构建连接池，例如Vector、Stack等
 
- **连接池的管理**
  - 当客户请求数据库连接时，首先查看连接池中是否有空闲连接，如果存在空闲连接，则将连接分配给客户使用
  - 如果没有空闲连接，则查看当前所开的连接数是否已经达到最大连接数，如果没达到就重新创建一个连接给请求的客户
  - 如果达到就按设定的最大等待时间进行等待，如果超出最大等待时间，则抛出异常给客户
  - 当客户释放数据库连接时，先判断该连接的引用次数是否超过了规定值，如果超过就从连接池中删除该连接，否则保留为其他客户服务
  - 该策略保证了数据库连接的有效复用，避免频繁的建立、释放连接所带来的系统资源开销
 
- 连接池的关闭
  - 当应用程序退出时，关闭连接池中所有的连接，释放连接池相关的资源，该过程正好与创建相反
 
- 连接池的配置与维护
  - 连接池中到底应该放置多少连接，才能使系统的性能最佳
  - 系统可采取设置最小连接数 min 和最大连接数 max 来控制连接池中的连接
  - 最小连接数是系统启动时连接池所创建的连接数
    - 如果创建过多，则系统启动就慢，但创建后系统的响应速度会很快
    - 如果创建过少，则系统启动的很快，响应起来却慢
    - 可以在开发时，设置较小的最小连接数，开发起来会快
    - 在系统实际使用时设置较大的，因为这样对访问客户来说速度会快些
  - 最大连接数是连接池中允许连接的最大数目
    - 具体设置多少，要看系统的访问量
    - 可通过反复测试，找到最佳点

> [ConnectionPoolTest](https://github.com/thu/DemoMVC/blob/master/src/main/java/demo/test/ConnectionPoolTest.java)

```java
import lombok.Getter;
import lombok.Setter;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.sql.*;
import java.util.Vector;

public class ConnectionPoolTest {

    private static final int INITIAL_CONNECTIONS_NUMBER = 10; // 连接池初始连接数
    private static final int INCREMENTAL_CONNECTIONS_NUMBER = 5; // 每次动态添加的连接数

    private static int maxConnectionsNum = 50; // 连接池最大连接数
    private static Logger logger = LoggerFactory.getLogger(ConnectionPoolTest.class);

    private String driver; // 数据库驱动
    private String url; // 数据库url
    private String user; // 数据库用户名
    private String password; // 数据库密码
    private String table; // 数据库表

    private Vector<PooledConnection> connections; // 向量，存放连接池中的连接

    /**
     * 有参构造方法
     * 初始化数据库驱动、数据库url、数据库用户名、数据库密码
     */
    public ConnectionPoolTest(String driver, String url, String user, String password, String table) {
        this.driver = driver;
        this.url = url;
        this.user = user;
        this.password = password;
        this.table = table;
        try {
            this.createPool();
        } catch (InstantiationException | IllegalAccessException | SQLException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        ConnectionPoolTest pool = new ConnectionPoolTest("com.mysql.jdbc.Driver", "jdbc:mysql:///test", "root", "system", "book");
        Connection connection = pool.getConnection();
        try {
            String sql = "SELECT * FROM test.book";
            PreparedStatement preparedStatement = connection.prepareStatement(sql);
            ResultSet resultSet = preparedStatement.executeQuery();
            System.out.println("\t--------- output ---------");
            while (resultSet.next()) {
                System.out.println("\t--------- " + resultSet.getString("title"));
            }
            System.out.println("\t--------- output ---------");
        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            pool.returnConnection(connection);
        }
    }

    /**
     * 创建连接池
     */
    public synchronized void createPool()
            throws InstantiationException, IllegalAccessException,
            ClassNotFoundException, SQLException {
        // 确保连接池为创建，如果已经创建，则保存连接的向量不为空
        if (this.connections != null) {
            return;
        }
        // 驱动器实例化
        Driver driver = (Driver) (Class.forName(this.driver).newInstance());
        // 注册驱动器
        DriverManager.registerDriver(driver);
        // 创建保存连接的向量
        this.connections = new Vector<>();
        // 创建数据库连接
        logger.info("init the pool...");
        this.createConnections(INITIAL_CONNECTIONS_NUMBER);
    }

    /**
     * 创建数据库连接
     */
    private void createConnections(int number) throws SQLException {
        logger.info("init pooled connection number: " + number);
        // 循环创建连接
        for (int i = 0; i < number; ++i) {
            // 需要首先检查当前连接数是否已经超出连接池最大连接数
            if (this.connections.size() >= maxConnectionsNum) {
                return;
            }
            // 创建连接
            PooledConnection pooledConnection = new PooledConnection(newConnection());
            this.connections.addElement(pooledConnection);
            logger.info("add a new connection into the pool: " + pooledConnection.getConnection());
        }

    }

    /**
     * 创建一个数据库连接
     */
    private Connection newConnection() throws SQLException {
        // 创建连接
        Connection connection = DriverManager.getConnection(url, user, password);
        // 如果是第一次创建连接，则检查所连接的数据库的允许最大连接数是否小于最大连接数
        if (this.connections.size() == 0) {
            DatabaseMetaData metadata = connection.getMetaData();
            // 得到数据库最大连接数
            int dbMaxConnectionsNum = metadata.getMaxConnections();
            logger.info("dbMaxConnectionsNum: " + dbMaxConnectionsNum);
            // 如果数据库最大连接数更小，则更改我们所设定的连接池最大连接数
            if (dbMaxConnectionsNum > 0 && maxConnectionsNum > dbMaxConnectionsNum) {
                maxConnectionsNum = dbMaxConnectionsNum;
            }
        }
        return connection;
    }

    /**
     * 得到一个可用连接
     */
    public synchronized Connection getConnection() {
        Connection connection = null;
        // 检查连接池是否已经建立
        if (this.connections == null) {
            return null;
        }
        // 得到一个可用连接
        try {
            connection = this.getFreeConnection();
        } catch (SQLException e) {
            e.printStackTrace();
        }
        // 如果未找到合适连接，循环等待、查找，知道找到合适连接
        while (connection == null) {
            this.wait(30);
            try {
                connection = this.getFreeConnection();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        logger.info("get a connection from the pool: " + connection);
        return connection;
    }


    /**
     * 得到一个可用连接
     */
    private Connection getFreeConnection() throws SQLException {
        // 查找一个可用连接
        Connection connection = this.findFreeConnection();
        // 如果未找到可用连接，就建立一些新的连接，再次查找
        if (connection == null) {
            this.createConnections(INCREMENTAL_CONNECTIONS_NUMBER);
            // 再次查找
            connection = this.findFreeConnection();
        }
        return connection;
    }


    /**
     * 从现有连接中查找一个可用连接
     * 在现有的连接中（向量connections中）找到一个空闲连接，
     * 并测试这个链接是否可用，若不可用则重新建立连接，替换原来的连接
     */
    private Connection findFreeConnection() throws SQLException {
        Connection connection = null;
        for (PooledConnection pooledConnection : this.connections) {
            if (!pooledConnection.isBusy()) {
                // 如果此链接未被使用，则返回这个连接并，设置正在使用标志
                connection = pooledConnection.getConnection();
                pooledConnection.setBusy(true);
                // 测试连接是否可用
                if (!this.testConnection(connection)) {
                    connection = this.newConnection();
                    pooledConnection.setConnection(connection);
                }
                break;
            }
        }
        return connection;
    }

    /**
     * 测试连接是否可用
     */
    private boolean testConnection(Connection connection) {
        boolean usable = true;
        try {
            Statement st = connection.createStatement();
            ResultSet rs = st.executeQuery("SELECT count(*) FROM " + table);
            rs.next();
        } catch (SQLException e) {
            // 抛出异常，连接不可用，关闭
            usable = false;
            this.closeConnection(connection);
        }
        return usable;
    }

    /**
     * 将使用完毕的连接放回连接池中
     */
    public void returnConnection(Connection connection) {
        // 确保连接池存在
        if (this.connections == null) {
            return;
        }
        //noinspection Convert2streamapi
        for (PooledConnection pooledConnection : connections) {
            // 找到相应连接，设置正在使用标志为 false
            if (connection == pooledConnection.getConnection()) {
                pooledConnection.setBusy(false);
                logger.info("return the connection to pool: " + connection);
            }
        }
    }

    /**
     * 刷新连接池中的连接
     */
    @SuppressWarnings("unused")
    public synchronized void refreshConnectionPool() throws SQLException {
        // 确保连接池存在
        if (this.connections == null) {
            return;
        }
        for (PooledConnection pooledConnection : connections) {
            if (pooledConnection.isBusy()) {
                this.wait(5000);
            }
            this.closeConnection(pooledConnection.getConnection());
            pooledConnection.setConnection(this.newConnection());
            pooledConnection.setBusy(false);
        }
    }

    /**
     * 关闭连接池
     */
    @SuppressWarnings("unused")
    public void closeConnectionPool() {
        // 确保连接池存在
        if (this.connections == null) {
            return;
        }
        for (int i = 0; i < this.connections.size(); ++i) {
            PooledConnection pool = this.connections.get(i);
            if (pool.isBusy()) {
                this.wait(5000);
            }
            this.closeConnection(pool.getConnection());
            this.connections.remove(i);
        }
        this.connections = null;
    }

    /**
     * 暂时无可用连接，进入等待队列等待，再试
     *
     * @param millis 毫秒
     */
    private void wait(int millis) {
        try {
            Thread.sleep(millis);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }


    /**
     * 连接使用完毕，关闭连接
     */
    private void closeConnection(Connection con) {
        try {
            con.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }


    /**
     * 内部类,数据库连接
     */
    @Setter
    @Getter
    class PooledConnection {

        private Connection connection; // 连接
        private boolean isBusy; // 是否正在使用

        /**
         * 构造方法
         */
        public PooledConnection(Connection connection) {
            this.connection = connection;
        }
    }
}
```
> []()

> []()

> []()

[Druid](https://github.com/alibaba/druid) datasource basic configuration

```xml
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource" init-method="init" destroy-method="close">
    <!-- 基本属性 url、user、password -->
    <property name="url" value="${jdbc_url}"/>
    <property name="username" value="${jdbc_user}"/>
    <property name="password" value="${jdbc_password}"/>

    <!-- 配置初始化大小、最小、最大 -->
    <property name="initialSize" value="${jdbc_initialSize}"/>
    <property name="minIdle" value="${jdbc_minIdle}"/>
    <property name="maxActive" value="${jdbc_maxActive}"/>

    <!-- 配置获取连接等待超时的时间 -->
    <property name="maxWait" value="60000"/>

    <!-- 配置间隔多久才进行一次检测，检测需要关闭的空闲连接，单位是毫秒 -->
    <property name="timeBetweenEvictionRunsMillis" value="60000"/>

    <!-- 配置一个连接在池中最小生存的时间，单位是毫秒 -->
    <property name="minEvictableIdleTimeMillis" value="300000"/>

    <property name="validationQuery" value="SELECT 'x'"/>
    <property name="testWhileIdle" value="true"/>
    <property name="testOnBorrow" value="false"/>
    <property name="testOnReturn" value="false"/>

    <!-- 配置监控统计拦截的filters -->
    <property name="filters" value="stat"/>
</bean>
```
