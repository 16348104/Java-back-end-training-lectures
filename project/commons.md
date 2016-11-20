# 通用组件

1. 加密

  > [Jasypt](http://www.jasypt.org/)

  ```gradle
  // build.gradle
  compile 'org.jasypt:jasypt:1.9.2'
  ```
  - 密码

    ```java
    // 加密
    StrongPasswordEncryptor encryptor = new StrongPasswordEncryptor();
    password = encryptor.encryptPassword(password);
    // 验证
   StrongPasswordEncryptor encryptor = new StrongPasswordEncryptor();
   if (encryptor.checkPassword(password, encryptedPassword)) {
         // ...
   } else {
         // ...
   }
   ```
 - 文本

2. 文件上传

  - 基于 `Servlet` 的文件上传实现

    > [Apache Commons FileUpload](http://commons.apache.org/proper/commons-fileupload/)

    > [quick use](http://commons.apache.org/proper/commons-fileupload/using.html)

    Edit `build.gradle` file
    ```gradle
    // build.gradle
    compile 'commons-fileupload:commons-fileupload:1.3.2'
    ```
    - Edit `*.jsp` file

      ```html
      <form action="your_action_url" method="post" enctype="multipart/form-data">
          <input type="file" name="upload">
      </form>
    ```

    - Edit `Servlet` class

      ```java
      DiskFileItemFactory diskFileItemFactory = new DiskFileItemFactory();
      ServletContext servletContext = request.getServletContext();
      String attribute= "javax.servlet.context.tempdir";
      File repository = (File) servletContext.getAttribute(attribute);
      diskFileItemFactory.setRepository(repository);

      ServletFileUpload servletFileUpload = new ServletFileUpload(diskFileItemFactory);

      try {
          List<FileItem> fileItems = servletFileUpload.parseRequest(request);
          for (FileItem fileItem : fileItems) {
              if (fileItem.isFormField()) {
                  System.out.print(fileItem.getFieldName());
                  System.out.print(" : ");
                  System.out.println(fileItem.getString());
              } else {
                  // FILE
                  System.out.println(fileItem.getFieldName());
                  System.out.println(fileItem.getName());
                  System.out.println(fileItem.getContentType());
                  System.out.println(fileItem.isInMemory());
                  System.out.println(fileItem.getSize());

                  File file = new File("d:/" + fileItem.getName());
                  fileItem.write(file);
              }
          }
      } catch (Exception e) {
          e.printStackTrace();
      }
      ```
  - 基于 `Spring` 的文件上传实现
    - Edit `build.gradle` file
    
      ```gradle
      compile 'commons-fileupload:commons-fileupload:1.3.2'   
    ```
    - Edit `register.jsp` file
    
      ```html
      <form action="${ctx}/student/register" method="post" enctype="multipart/form-data">
          <%-- change name from photo to photoFile --%> 
          <input type="file" name="photoFile" placeholder="PHOTO">
      </form>
      ```
    
    - Edit `web-servlet.xml` file

      ```xml
    <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
          <property name="defaultEncoding" value="UTF-8"/>
    </bean>
      ```
      
    - Create directory `/webapp/static/photo`      
    
    - Edit `StudentController` class

      ```java
      
      public static final String PHOTO_PATH = "/static/photo";
      
      @RequestMapping("register")
      private String register(Student student, @RequestParam MultipartFile photoFile) throws IOException {
          String photoPath = application.getRealPath(PHOTO_PATH);
          photoFile.transferTo(new File(photoPath, photoFile.getOriginalFilename()));
          student.setPhoto(photoFile.getOriginalFilename());

          // register ...
      }
      ```
    
3. Lombok

  > [Project Lombok](https://projectlombok.org/)

  > [Lobmok Plugin on Github](https://github.com/mplushnikov/lombok-intellij-plugin)

  - bulid.gradle
  ```gradle
  compile 'org.projectlombok:lombok:1.16.8'
  ```
  
  - IDEA
      - install Lombok plugin
        - [Lombok Plugin](http://plugins.jetbrains.com/plugin/6317?pr=idea)
      - File > Settings > Build, Execution, Deployment > Compiler > Annotation Processors
        - check "Enable annotation processing"

  - Model class
  
    ```java
    import lombok.Data;
    import lombok.EqualsAndHashCode;

    @Data
    @EqualsAndHashCode(callSuper = true)
    public class Admin extends BaseModel {
        private Integer id;
        private String email;
        private String username;
        private String password;
    }
    ```
    
    ```java
    Warning: java: 
    Generating equals/hashCode implementation but without a call to superclass, 
    even though this class does not extend java.lang.Object. 
    If this is intentional, add '@EqualsAndHashCode(callSuper=false)' to your type.
    ```

4. 日志处理

  - SLF4J

    > Simple Logging Facade `[fə'sɑːd]` for Java

    - `Logger` interface
    - `LoggerFactory` class

  2. Log4j

    > Log For Javaw

    - build.gradle

        ```gradle
        compile 'org.slf4j:slf4j-log4j12:1.7.21'
        ```

    - 在类路径根目录下创建 `log4j.properties` 文件

    - 配置 `rootLogger`

        ```properties
        # rootLogger: all trace debug info warn error fatal off
        log4j.rootLogger = error, console
        ```

      - 日志级别
        - `all`
        - `trace` 
        - &#10003; `debug`
        - &#10003; `info`
        - &#10003; `warn`
        - &#10003; `error`
        - `fetal`
        - `off`

    - 指定具体类的日志输出级别，覆盖 `rootLogger` 级别

        ```properties
        log4j.logger.demo = trace
        ```

    - 配置日志信息输出目的地 `Appender`

        ```properties
        # console appender
        log4j.appender.console=org.apache.log4j.ConsoleAppender
        ```

        - `log4j.ConsoleAppender` `控制台`
        - `log4j.FileAppender` `文件`
        - `log4j.DailyRollingFileAppender` `每天产生一个日志文件`
        - `log4j.RollingFileAppender` `文件到达指定尺寸时产生一个新的文件`
        - `log4j.WriterAppender` `以流格式发送到任意指定的地方`
        - `log4j.appender.MAIL` `发送邮件`

    - 配置日志信息的输出格式 `Layout`

        ```properties
        # console layout
        log4j.appender.console.layout=org.apache.log4j.PatternLayout
        log4j.appender.console.layout.ConversionPattern=%m%n
        ```

      - 布局方式
        - `org.apache.log4j.HTMLLayout` `HTML 表格形式布局`
        - `org.apache.log4j.PatternLayout` `灵活地指定布局模式`
        - `org.apache.log4j.SimpleLayout` `日志信息的级别和信息字符串`
        - `org.apache.log4j.TTCCLayout` `日志产生的时间、线程、类别等等信息`
      - 输出格式
        - `%m` 输出代码中指定的消息
        - `%p` 输出优先级，即 `DEBUG`，`INFO`，`WARN`，`ERROR`，`FATAL`
        - `%r` 输出自应用启动到输出该 log 信息耗费的毫秒数
        - `%c` 输出所属的类目，通常就是所在类的全名
        - `%t` 输出产生该日志事件的线程名
        - `%n` 输出一个回车换行符，Windows 平台为 `\r\n`，Unix 平台为 `\n`
        - `%d` 输出日志时间点的日期或时间，默认格式为 `ISO8601`，也可以在其后指定格式
            - 举例：`%d{yyy MMM dd HH:mm:ss,SSS}`
            - 输出类似：2016年05月27日 12:10:28,921
        - `%l` 输出日志事件的发生位置，包括类目名、发生的线程，以及在代码中的行数
          - 举例：`Log4jTest.main(Log4jTest.java:10)`

    - Log4j Test

        ```java
        package demo.test;

        import org.slf4j.Logger;
        import org.slf4j.LoggerFactory;

        public class Log4jTest {
              private static Logger logger = LoggerFactory.getLogger(Log4jTest.class);
              public static void main(String[] args) {
                  logger.trace("trace...");
                  logger.debug("debug...");
                  logger.info("info...");
                  logger.warn("warn....");
                  logger.error("error...");
              }
          }

        /*

        output:

        trace...
        debug...
        info...
        warn....
        error...

        */
        ```

  3. Logback

    > [Logback Project](http://logback.qos.ch/)

    > Based on our previous work on log4j, logback internals have been re-written to perform about ten times faster on certain critical execution paths. Not only are logback components faster, they have a smaller memory footprint as well.

    - build.gradle
    
        ```gradle
        compile 'ch.qos.logback:logback-access:1.1.3'
        compile 'ch.qos.logback:logback-site:1.1.3'
        compile 'org.slf4j:slf4j-simple:1.7.21'
        ```
        
5. 数据库连接池

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
    ```
    连接池中到底应该放置多少连接，才能使系统的性能最佳
    系统可采取设置最小连接数 min 和最大连接数 max 来控制连接池中的连接
    
    最小连接数是系统启动时连接池所创建的连接数
        1. 如果创建过多，则系统启动就慢，但创建后系统的响应速度会很快
        2. 如果创建过少，则系统启动的很快，响应起来却慢
        3. 可以在开发时，设置较小的最小连接数，开发起来会快
        4. 在系统实际使用时设置较大的，因为这样对访问客户来说速度会快些
    
    最大连接数是连接池中允许连接的最大数目
        1. 具体设置多少，要看系统的访问量
        2. 可通过反复测试，找到最佳点
    
    确保连接池中的最小连接数有动态和静态两种策略
        1. 动态即每隔一定时间就对连接池进行检测，如果发现连接数量小于最小连接数，则补充相应数量的新连接
        2. 静态是发现空闲连接不够时再去检查
    ```
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