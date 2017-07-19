# Chapter 2 核心组件

> Mapper / Configuration / Mapper Interface / SqlSessionFactory / SqlSession / Service

1. Create `sql/db_test.sql` file

  ```sql
  DROP DATABASE IF EXISTS test;
  CREATE DATABASE test;

  # user
  DROP TABLE IF EXISTS test.user;
  CREATE TABLE test.user (
    id       INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255),
    password VARCHAR(255)
  );

  SELECT *
  FROM test.user;
  ```
    
2. Update `build.gradle` file

  ```gradle
  compile 'mysql:mysql-connector-java:5.1.39'
  compile 'org.mybatis:mybatis:3.3.0'
  ```
    
3. Create `model.User` model class

  ```java
  public class User implements Serializable {
      private Integer id;
      private String username;
      private String password;

      // setters and getters
  }
  ```

4. Create `resources/user-mapper.xml` mapper file

    > 注意：在使用 `Mapper` 接口时， `namespace` 的取值是 `Mapper` 接口的全限定名

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <mapper namespace="mapper.UserMapper">
      <insert id="create" parameterType="model.User" useGeneratedKeys="true" keyProperty="id">
          INSERT INTO user VALUES (NULL, #{username}, #{password})
      </insert>
  </mapper>
  ```
    
5. Create `resources/mybatis-config.xml` config file

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE configuration
          PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-config.dtd">
  <configuration>
      <properties resource="jdbc.properties"/>
      <environments default="dev">
          <environment id="dev">
              <transactionManager type="JDBC"/>
              <dataSource type="POOLED">
                  <property name="driver" value="${driver}"/>
                  <property name="url" value="${url}"/>
                  <property name="username" value="${username}"/>
                  <property name="password" value="${password}"/>
              </dataSource>
          </environment>
      </environments>
      <mappers>
          <mapper resource="user-mapper.xml"/>
      </mappers>
  </configuration>
  ```

6. Create `jdbc.properties` file

  ```properties
  # jdbc.properties
  driver = com.mysql.jdbc.Driver
  url = jdbc:mysql:///test
  username = your_username
  password = your_password
  ```
    
7. Create `util.MyBatisSession` sigleton class             

  ```java
  import org.apache.ibatis.io.Resources;
  import org.apache.ibatis.session.SqlSession;
  import org.apache.ibatis.session.SqlSessionFactory;
  import org.apache.ibatis.session.SqlSessionFactoryBuilder;

  import java.io.IOException;
  
  public class MyBatisSqlSession { 
      private static SqlSessionFactory sqlSessionFactory;

      private static SqlSessionFactory getSqlSessionFactory() { 
          if (sqlSessionFactory == null) {
              try { 
                  sqlSessionFactory = new SqlSessionFactoryBuilder().build(Resources.getResourceAsStream("mybatis-config.xml"));
              } catch (IOException e) {
                  e.printStackTrace();
              } 
          } 
          return sqlSessionFactory;
      } 

      public static SqlSession getSqlSession(boolean autoCommit) {
          return getSqlSessionFactory().openSession(autoCommit);
      } 
  } 
  ```
    
8. Create `mapper.UserMapper` interface

  ```java
  public interface UserMapper { 

      int create(User user);
  }  
  ```
    
9. Create `service.Userservice` class

  ```java
  import mapper.UserMapper;
  import model.User;
  import org.apache.ibatis.session.SqlSession;
  import util.MyBatisSqlSession;

  public class UserService {

      // create record by XML configuration
      private static int createUserViaXML() {
          try (SqlSession sqlSession = MyBatisSqlSession.getSqlSession(true)) {
              return sqlSession.insert("mapper.UserMapper.create", new User("Tester1", "password1"));
          }
      }

      // create record by Mapper interface
      private static int createUser() {
          try (SqlSession sqlSession = MyBatisSqlSession.getSqlSession(true)) {
              UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
              return userMapper.create(new User("Tester2", "password2"));
          }
      }

      public static void main(String[] args) {
  //        createUserViaXML(); // MyBatis method 1
          createUser(); // MyBatis method 2: Type Safer
      }
  }
  ```    
