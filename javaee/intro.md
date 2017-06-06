# Chapter 1 引言

1. JSP

    > Java Server Pages    

2. Servlet

    > servlet
    
3. JSP & Servlet
    
    > JSP 的本质是 Servlet， Servlet 的本质是 Class

4. 环境配置
    - 应用服务器
        - ~~<a href="../doc/the-great-java-app-server-debate.pdf" target="_blank">[PDF] the great java app server debate</a>~~
    - `JSP` 和 `Servlet` 的容器
    - <a name="tomcat_install"></a>`Tomcat`
    
        <img src="../image/javaee/Tomcat-logo.svg" width="100"> 
        
        > [Apache Tomcat](http://tomcat.apache.org/)

        - unzip [apache-tomcat-version-windows-x86](http://tomcat.apache.org/download-80.cgi) to your_tomcat_directory
        - Windows
            - set environment variable:
                
                your_tomcat_directory/bin/setclasspath.bat
            
                set JAVA_HOME=your_jdk_directory
            
            - startup or shutdown:
                
                your_tomcat_directory/bin/
                
                ```
                startup.bat
                
                or
                
                shutdown.bat
                ```
               
            - find port using and kill task

              ```
              Win:
              > netstat -ano|findstr <port>
              > taskkill /f /pid <pid>
              
              Mac:
              $ lsof -i :<port>
              $ kill -9 <pid>
              ```
        - browser:
        
            ```
            localhost:8080
            127.0.0.1:8080
            your_ip:8080
            ```

5. Java EE Hello,world！
6. HTTP(s)

    > Hyper Text Transfer Protocol 超文本传输协议
