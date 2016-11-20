# Chapter 3 配置

1. `mybatis-config.xml`

    > 使用 XML 文件进行配置的方式

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
  <configuration>
      <properties resource="application.properties">
          <property name="username" value="your_username"/>
          <property name="password" value="your_password"/>
      </properties>
      <settings>
          <setting name="cacheEnabled" value="true"/>
      </settings>
      <typeAliases>
          <typeAlias alias="user" type="model.User"/>
          <package name="model"/>
      </typeAliases>
      <typeHandlers>
          <typeHandler handler="typehandler.YourTypeHandler"/>
          <package name="typehandler"/>
      </typeHandlers>
      <environments default="development">
          <environment id="development">
              <transactionManager type="JDBC"/>
              <dataSource type="POOLED">
                  <property name="driver" value="${jdbc.driverClassName}"/>
                  <property name="url" value="${jdbc.url}"/>
                  <property name="username" value="${jdbc.username}"/>
                  <property name="password" value="${jdbc.password}"/>
              </dataSource>
          </environment>
          <environment id="production">
              <transactionManager type="MANAGED"/>
              <dataSource type="JNDI">
                  <property name="data_source" value="java:comp/jdbc/MyBatisDemoDataSource"/>
              </dataSource>
          </environment>
      </environments>
      <mappers>
          <mapper resource="user-mapper.xml"/>
          <mapper url="file:///absolute_path/user-apper.xml"/>
          <mapper class="mapper.UserMapper"/>
      </mappers>
  </configuration>
  ```
  - `Environment`
      - 每个数据环境定义为一个 `environment`
      - `environment` 的 id 表明数据环境的不同用途，如 `development` / `test` / `production` 等
      - 通过 `environments` 的 `default` 属性指定当前的数据环境
      - 一个应用程序可以使用多个数据环境

        ```java
        // use default environment
        inputStream = Resources.getResourceAsStream("mybatis-config.xml");
        defaultSqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);

        // use environment a
        aSqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream, "environment-id_a");

        // use environment b
        bSqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream, "environment-id_b");
        ```

      - 每个 `environment` 中须定义 `transactionManager` 和 `dataSource`
  - `Datasource`
      - `dataSource` 主要用来指定数据库连接属性
      - `dataSource` 的 `type` 属性可以为以下 3 种值
          1. `UNPOOLED`
              - 每次数据库操作创建一个新的连接，操作结束关闭连接
              - 适用于用户少的系统
          2. `POOLED`
              - 数据库连接池方式，每次操作从池中取出一个连接，操作结束放回池中
              - 适用于大多数开发或测试场景
          3. `JNDI`
              - 从 `JNDI` 数据源中取得数据库连接
              - 适用于生产环境
  - `TransactionManager`
      - `MyBatis` 支持两种事务管理方式
          1. `JDBC` 
              - 应用程序负责事务处理
              - 使用 `commit / rollback` 等方式进行事务处理
              - 使用 `JdbcTransactionFactory` 创建 `TransactionManager`
              - 如使用 `Tomcat` 部署的应用程序
          2. `MANAGED`
              - 应用服务器负责事务处理
              - 使用 `ManagedTransactionFactory` 创建 `TransactionManager`
              - 如使用 `JBoss / WebLogic / GlassFish`
  - `Properties`
      - 指定属性文件
      - 属性文件以 `key - value` 方式存储属性信息
      - `properties` 中可以使用 `property` 元素设置默认属性信息，会被属性文件的同名属性覆盖
  - `TypeAliases`
      - 类型别名
      - 简化 `mapper` 中的全限定名 `Fully Qualified Name`
      - 如果指定 `package` `name` 会自动注册包中的类型为全部小写的别名
      - 还可以用 `@alias` 注解指定一个类型的别名，这种方式覆盖 `typeAliases` 元素的设置

      ```java
      @Alias("specified-alias")
      public class Model {}
      ```
  - `TypeHandlers`
      - `MyBatis` 内置类型处理器能够处理的类型
          - 基本数据类型及其封装类
          - byte[]
          - java.util.Date / java.sql.Date / java.sql.Time / java.sql.TimeStamp
          - java enums
      - 对其他特定类型，需要使用类型处理器进行类型转换
          1. 扩展 `BaseTypeHandler<T>` 抽象父类

            ```java
            public YourCustomTypeHandler extends BaseTypeHandler<CustomType> {
            }
            ```

          2. 在 `mybatis-config.xml` 中注册类型处理器

            ```xml
            <typeHandlers>
                <typeHandler handler="your.package.YourCustomTypeHandler"/>
            </typeHandlers>
            ```
              
  - `Settings`
      - `MyBatis` 默认全局设定

      ```xml
      <settings>
          <setting name="cacheEnabled" value="true"/>
          <setting name="lazyLoadingEnabled" value="true"/>
          <setting name="multipleResultSetsEnabled" value="true"/>
          <setting name="useColumnLabel" value="true"/>
          <setting name="useGeneratedKeys" value="false"/>
          <setting name="autoMappingBehavior" value="PARTIAL"/>
          <setting name="defaultExecutorType" value="SIMPLE"/>
          <setting name="defaultStatementTimeout" value="25000"/>
          <setting name="safeRowBoundsEnabled" value="false"/>
          <setting name="mapUnderscoreToCamelCase" value="false"/>
          <setting name="localCacheScope" value="SESSION"/>
          <setting name="jdbcTypeForNull" value="OTHER"/>
          <setting name="lazyLoadTriggerMethods" value="equals,clone,hashCode,toString"/>
      </settings>
      ```

  - `Mappers`
      - 配置 `Mapper XML` 文件的路径
          - `resource` 定义 `classpath` 映射文件
          - `url` 定义全限定文件系统路径或网络 `URL`
          - `class` 定义映射接口
          - `package` 映射接口所在的包路径
            
2. `Java API`

    > 使用 Java API 的方式进行配置
    
  ```java
  public static SqlSessionFactory getSqlSessionFactory() {
      SqlSessionFactory sqlSessionFactory = null;
      try{
          DataSource dataSource = DataSourceFactory.getDataSource();
          TransactionFactory transactionFactory = new JdbcTransactionFactory(); // new ManagedTransactionFactory();
          Environment environment = new Environment("development", transactionFactory, dataSource);
          Configuration configuration = new Configuration(environment);
          configuration.getTypeAliasRegistry().registerAlias("user", User.class);
          configuration.getTypeHandlerRegistry().register(YourTypeHandler.class,YourTypeHandler.class);
          configuration.addMapper(UserMapper.class);
          sqlSessionFactory = new SqlSessionFactoryBuilder().build(configuration);
      } catch (Exception e){
          throw new RuntimeException(e);
      }
      return sqlSessionFactory;
  }
  ```

  ```java
  public class DataSourceFactory {
      public static DataSource getDataSource() {
          String driver = "com.mysql.jdbc.Driver";
          String url = "jdbc:mysql:///test";
          String username = "your_username";
          String password = "your_password";
          PooledDataSource dataSource = new PooledDataSource(driver, url, username, password);
          return dataSource;
      }
  }
  ```