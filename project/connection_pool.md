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
// ...
```

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
