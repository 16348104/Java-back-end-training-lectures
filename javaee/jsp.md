# Chapter 2 JSP 语法

1. 一个典型的JSP

  > classic.jsp

  ```html
  <!DOCTYPE html>
  <%@ page language="java" contentType="text/html; charset=UTF-8" %>
  <!--这是一个典型的JSP，它包含了JSP中常用的元素-->
  <%!
      String getDate() {
          return new java.util.Date().toString();
      }
      int count = 10;
  %>
  <html>
  <head><title>一个典型的JSP</title></head>
  <body>
  <jsp:include page="header.jsp"/>
  <div style="text-align: center">
      <table style="margin: 0 auto;">
          <tr style="background: #777;">
              <th>----------------</th>
          </tr>
          <%
              // color
              String c1 = "#9cf", c2 = "#8c3";
              for (int i = 0; i < count; i++) {
                  String color;
                  if (i % 2 == 0) {
                      color = c1;
                  } else {
                      color = c2;
                  }
                  out.println("<tr style=\"background:" + color + ";\"><td>-</td></tr>");
              }
          %>
      </table>
      <hr/>
      当前的时间是：
      <%-- 下面是使用表达式的例子 --%>
      <%=getDate()%>
  </div>
  </body>
  </html>
  ```
    
  > header.jsp

  ```html
  <%@ page language="java" contentType="text/html; charset=UTF-8" %>
  <div style="text-align: center">
      <hr/>
      JSP的典型例子
      <hr/>
  </div>
  ```
    
  > build.gradle
    
  ```gradle
  compile 'javax:javaee-api:7.0'
  
  // 同步 gradle
  ```

2. `JSP` 页面元素
    1. 注释
        - `HTML` 注释 `<!-- comment... -->`
        - `JSP` 隐藏注释 `<%-- comment... --%>`
        - `Java` 注释 
          - `// comment`
          - `/* comment */`
    2. 模板元素
        - 静态 `HTML` 元素
    3. 脚本元素
        - 声明 `declaration` `<%! %>` class 类体内
        - 小脚本 `scriptlet` `<% %>` _jspService() 方法体内
        - 表达式 `expression` `<%= %>` out.print() 方法的参数
    4. 指令元素
        - page 指令 `<%@ page %>`
        - include 指令 `<%@ include %>`
        - taglib 指令 `<%@ taglib %>`
    5. 动作元素
        - include 动作` <jsp:include page=""/>`
    
3. JSP 的本质是 Java Class