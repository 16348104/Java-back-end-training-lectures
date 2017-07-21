# 日志处理

1. SLF4J

    > Simple Logging Facade `[fə'sɑːd]` for Java
    
    - `Logger` interface
    - `LoggerFactory` class

2. Log4j

    > Log For Java
    
    1. build.gradle
    
        ```gradle
        compile 'org.slf4j:slf4j-log4j12:1.7.21'
        ```
    
    2. 在类路径根目录下创建 `log4j.properties` 文件
    
    3. 配置 `rootLogger`
    
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
    
    4. 配置日志信息输出目的地 `Appender`
    
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
    
    5. 配置日志信息的输出格式 `Layout`
    
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
    
    6. Log4j Test
    
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
        
    7. `log4j.properties` 参考配置            
        
        ```properties
        # 1. rootLogger: all trace debug info warn error fatal off
        log4j.rootLogger = error, console
        
        log4j.logger.user.queryByUsername = trace
        log4j.logger.book = debug
        
        # 2. console appender
        log4j.appender.console = org.apache.log4j.ConsoleAppender
        
        #log4j.appender.file=org.apache.log4j.FileAppender
        #log4j.appender.file.File=/Users/mingfei/Desktop/idea.log
        #log4j.appender.file.Append=true
        
        # mail SMTP = Simple Mail Transfer Protocol
        #log4j.appender.MAIL=org.apache.log4j.net.SMTPAppender
        #log4j.appender.MAIL.Threshold=trace
        #log4j.appender.MAIL.BufferSize=1
        #log4j.appender.MAIL.SMTPDebug=true
        #log4j.appender.MAIL.SMTPHost=smtp.qq.com
        #log4j.appender.MAIL.Subject=Log4J \u63D0\u9192\u60A8\uFF1A\u7CFB\u7EDF\u53D1\u751F\u4E86\u4E25\u91CD\u9519\u8BEF
        #log4j.appender.MAIL.SMTPUsername=65775105
        #log4j.appender.MAIL.SMTPPassword=
        #log4j.appender.MAIL.SMTPPort=587
        #log4j.appender.MAIL.From=65775105@qq.com
        #log4j.appender.MAIL.To=675835357@qq.com,330286610@qq.com,32694110@qq.com,1096161287@qq.com,1291813139@qq.com,19072390@qq.com
        #log4j.appender.MAIL.Bcc=65775105@qq.com
        
        # 3. console layout
        log4j.appender.console.layout = org.apache.log4j.PatternLayout
        log4j.appender.console.layout.ConversionPattern = %d\t%p\t%c{1}\t%m%n
        
        #log4j.appender.file.layout=org.apache.log4j.PatternLayout
        #log4j.appender.file.layout.ConversionPattern=%d\t%p\t%c{1} : %l - %m%n
        
        #log4j.appender.MAIL.layout=org.apache.log4j.PatternLayout
        #log4j.appender.MAIL.layout.ConversionPattern=%d{yyy MMM dd HH:mm:ss,SSS}\t%p\t%c{1} : %l - %m%n
        
        #登录qq邮箱
        #进入设置
        #进入账户
        #点击开启 POP3/SMTP服务
        #按照操作一步一步开启
        #生成授权码
        #所有程序登录都次啊用授权码登陆
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
