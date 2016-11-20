# Chapter 5 EL & JSTL

> Expression Language

> JSP Standard Tag Library

- EL 表达式语言
  1. `${expression}`
  2. get attribute

      ```
       PageContext    pageScope
       Request        requestScope
       Session        sessionScope
       Application    applicationScope
      ```
  3. `param.request_key`
  4. EL 运算
    - `eq`
    - `ne`
    - `lt`
    - `gt`

- JSTL JSP 标准标记库

  > build.grdle

  ```
  compile 'jstl:jstl:1.2'
  ```

  > *.jsp

  ```
  <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
  ```

  1. core 核心标签
      - `c:out`
      - `c:set`
      - `c:remove`
      - `c:catch`
      - **`c:if`**
      - **`c:choose`** 用来包含 `c:when` 或 `c:otherwise`
      - **`c:when`** 在 `c:choose` 中，至少有一个，可以有多个
      - **`c:otherwise`** 在 `c:choose` 中，可有可无，若有只能有 1 个，并位于最后
      - `c:import`
      - **`c:forEach`**
      - `c:forTokens`
      - `c:param`
      - **`c:redirect`**
      - `c:url`
  2. fn 函数
     - `fn:length`
  3. fmt 格式化
     - `fmt:formatDate` 
    ```jsp
    <fmt:formatDate value="${datetime_as_timeStamp_format}" pattern="yyyy-MM-dd HH:mm:ss"/>
    ```

  4. ~~sql 数据库~~
  5. ~~xml xml~~