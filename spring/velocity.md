# Velocity with Spring

> [Velocity - Java Template Engine](http://velocity.apache.org/)

> Note: Starting from version 4.3, Spring does not support Velocity, and the Velocity will be be removed from Spring from version 5 (In the future).

1. Edit `builde.gradle` file

  ```gradle
  compile 'org.apache.velocity:velocity:1.7'
  compile 'org.springframework:spring-context-support:4.2.6.RELEASE'
  ```
  
2. Edit `applicationContext.xml` file

  ```xml
  <bean id="velocity" class="org.springframework.web.servlet.view.velocity.VelocityConfigurer">
          <property name="resourceLoaderPath" value="classpath:template"/>
  </bean>
  ```
  
3. Create `resources/template/test.vm` file

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>velocity test</title>
  </head>
  <body>
  <h1>Hello, ${name}!</h1>
  </body>
  </html>
  ```
  
4. Create `test.FreemarkerTest` class

  ```java
  public class VelocityTest {
      public static void main(String[] args) throws IOException {
          ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
          VelocityConfig velocityConfig = (VelocityConfig) applicationContext.getBean("velocity");
  
          Template template = velocityConfig.getVelocityEngine().getTemplate("test.vm");
  
          VelocityContext velocityContext = new VelocityContext();
          velocityContext.put("name", "Velocity");
  
          try (Writer writer = new PrintWriter("test.html")) {
              template.merge(velocityContext, writer);
          }
      }
  }
  ```
