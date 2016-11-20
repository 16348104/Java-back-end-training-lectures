# Chapter 4 Servlet

> 服务器端小程序

1. `Servlet`

    > 扩展了 `javax.servlet.http.HttpServlet` 的类
    
2. `Servlet` 用来： 
    
    > 接收请求

    > 处理请求
    
    > 返回响应
    
3. 注解式配置

    ```java
    @WebServlet(urlPatterns="/your_pattern")
    ```
4. Servlet 生命周期

  > [](https://www.ibm.com/developerworks/cn/java/j-lo-servlet/)

  - init()
    - servlet 被创建时 init() 执行一次，此后不再执行
  - service()
    - 处理请求的主要方法，由 servlet 容器调用
    - 判断请求的方法，然后调用 doGet(), doPost()等方法处理请求
  - destroy()
    - 在 servlet 生命周期结束时被调用一次，做清理的工作

5. Refactoring 重构

    > 在不改变软件系统外部行为的前提下，改善其内部代码结构