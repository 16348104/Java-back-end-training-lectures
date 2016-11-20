# Mybatis + Spring

1. Edit `build.gradle` file

  ```gradle
  compile 'org.mybatis:mybatis-spring:1.3.0'
  compile 'org.springframework:spring-jdbc:4.2.6.RELEASE'
  ```

2. Create `resources/jdbc.properties` file

  ```properties
  jdbc_driverClassName = com.mysql.jdbc.Driver
  jdbc_url = jdbc:mysql:///db_name
  jdbc_username = your_username
  jdbc_password = your_password
  ```

2. Edit `resources/applicationContext.xml` file

  ```xml
  <context:property-placeholder location="classpath:jdbc.properties"/>
  
  <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
      <property name="driverClassName" value="${jdbc_driverClassName}"/>
      <property name="url" value="${jdbc_url}"/>
      <property name="username" value="${jdbc_username}"/>
      <property name="password" value="${jdbc_password}"/>
  </bean>

  <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
      <property name="dataSource" ref="dataSource"/>
      <property name="mapperLocations" value="classpath:mapper/*.xml"/>
      <property name="typeAliasesPackage" value="demo.model"/>
  </bean>

  <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
      <constructor-arg ref="sqlSessionFactory"/>
  </bean>
  ```
  
3. Edit Controller

  ```java
  // ...
  @Autowired
  private SqlSession sqlSession;
  // ...
  ```