# Chapter 3 Spring MVC

1. Edit `build.gradle` file

  ```gradle
  compile 'javax:javaee-api:7.0'
  compile 'org.springframework:spring-webmvc:4.2.6.RELEASE'
  ```

2. Edit `WEB-INF/web.xml` file

  ```xml
  <!-- Spring DispatcherServlet registry -->
  <servlet>
      <servlet-name>web</servlet-name>
      <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
  </servlet>
  <!-- Spring DispatcherServlet mapping -->
  <servlet-mapping>
      <servlet-name>web</servlet-name>
      <url-pattern>/</url-pattern>
  </servlet-mapping>

  <!-- default servlet mapping -->
  <servlet-mapping>
      <servlet-name>default</servlet-name>
      <url-pattern>/static/*</url-pattern>
  </servlet-mapping>

  <!-- Spring ContextLoaderListener Registry -->
  <listener>
      <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
  </listener>

  <!-- Spring applicationContext.xml Location -->
  <context-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:applicationContext.xml</param-value>
  </context-param>
  ```

3. Create `WEB-INF/web-servlet.xml` file

  > `web-servlet.xml = your_dispatcher_serlet_name + -servlet.xml`

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns:context="http://www.springframework.org/schema/context"
         xmlns:mvc="http://www.springframework.org/schema/mvc"
         xsi:schemaLocation="
         http://www.springframework.org/schema/beans
         http://www.springframework.org/schema/beans/spring-beans.xsd
         http://www.springframework.org/schema/context
         http://www.springframework.org/schema/context/spring-context.xsd
         http://www.springframework.org/schema/mvc
         http://www.springframework.org/schema/mvc/spring-mvc.xsd">

      <mvc:annotation-driven />
      <context:component-scan base-package="controller" />

      <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
          <property name="prefix" value="/"/>
          <property name="suffix" value=".jsp"/>
      </bean>
  </beans>
  ```

4. Create `controller.UserController` class
    
  ```java
  import org.springframework.stereotype.Controller;
  import org.springframework.web.bind.annotation.PathVariable;
  import org.springframework.web.bind.annotation.RequestMapping;

  @Controller
  @RequestMapping("user")
  public class UserController [extends BaseController] {

      @RequestMapping("create")
      private String create(User user) {
          // save user...
          System.out.println("created...");
          return "redirect:/index.jsp"
      }
  }
  ```
  
5. Create `controller.BaseController` class

  ```java
  import org.springframework.web.bind.annotation.ModelAttribute;

  import javax.servlet.ServletContext;
  import javax.servlet.http.HttpServletRequest;
  import javax.servlet.http.HttpServletResponse;
  import javax.servlet.http.HttpSession;

  class BaseController {
      HttpServletRequest request;
      HttpServletResponse response;
      HttpSession session;
      ServletContext application;

      @ModelAttribute
      private void set(HttpServletRequest request, HttpServletResponse response) {
          this.request = request;
          this.response = response;
          session = request.getSession();
          application = request.getServletContext();
      }
  }
  ```