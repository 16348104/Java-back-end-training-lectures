# Freemarker with Spring

> [Freemarker - Java Template Engine](http://freemarker.org/)

> [Manual](https://sourceforge.net/projects/freemarker/files/chinese-manual/)

<img title="Freemarker Overview" src="../image/spring/overview_freemarker.png" style="margin-left:32px; padding:10px; background:#fff">

1. Edit `builde.gradle` file

  ```gradle
  compile 'org.freemarker:freemarker:2.3.24-incubating'
  compile 'org.springframework:spring-context-support:4.2.6.RELEASE'
  ```
  
2. Edit `applicationContext.xml` file

  ```xml
  <bean id="freemarker" class="org.springframework.web.servlet.view.freemarker.FreeMarkerConfigurer">
      <property name="templateLoaderPath" value="classpath:template"/>
  </bean>
  ```
  
3. Create `resources/template/test.ftl` file

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>freemarker test</title>
  </head>
  <body>
  <h1>Hello, ${name}!</h1>
  </body>
  </html>
  ```
  
4. Create `test.FreemarkerTest` class

  ```java
  public class FreemarkerTest {
      public static void main(String[] args) throws IOException, TemplateException {
          ApplicationContext applicationContext = new ClassPathXmlApplicationContext("applicationContext.xml");
          FreeMarkerConfig freeMarkerConfig = (FreeMarkerConfig) applicationContext.getBean("freemarker");

          Template template = freeMarkerConfig.getConfiguration().getTemplate("test.ftl"); // 1. Template
          Map<String, String> map = new HashMap<>(); // 2. Java Object
          map.put("name", "world");
          Writer writer = new FileWriter("d:/test.html"); // 3. Output
          template.process(map, writer); // Freemarker Processing...
      }
  }
  ```