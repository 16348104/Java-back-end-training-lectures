# Chapter 3 JSP 隐式对象

> `Implicit Object` JSP 隐式 / 隐藏 / 隐含 / 内建 / 内置  对象

- `out`
- `request` 请求

    > request 封装了用户的所有请求信息
    
    1. `getParameter()` 获取用户填写的表单参数
    2. `getParameterValues()` 获取用户填写的表单参数(多选下拉列表 / 复选框)
    3. `getRemoteAddr()` 
    4. `getSession()`
    5. `setAttribute()`
    6. `getAttribute()`
    7. `getRequestDispatcher().forward()` 页面跳转 `forwrad` 转发
    8. `setCharacterEncoding()`
- `response` 响应
    1. `sendRedirect()` 页面跳转 `redirect` 重定向
    2. `setCharacterEncoding()`
    3. `setContentType()`
    3. `getWriter()`
    2. 转发 与 重定向
        - 都可以实现页面的跳转
        - 转发不改变地址，重定向改变地址
        - 转发可以保存 `request` 范围内的属性，重定向不能
    3. 表单提交方式 `get` 和 `post`
        - 都可以提交表单参数
        - `get` 会在地址栏中显示表单参数与值，`post` 不会
        - `get` 提交参数有最大长度限制，`post` 没有
        - 注：来自于链接的请求都是 `get` 
- `session` 会话
    1. web 应用中，属性的存在范围
        - `pageContext`
        - `request`
        - `session`
        - `application`
    2. `setAttribute()`
    3. `getAttribute()`
    4. `getId()`
        - `HTTP` `stateless` `stateless` 无状态性
    5. `invalidate()`
- `application`
    1. `setAttribute()`
    2. `getAttribute()`
- `pageContext`
    1. `setAttribute()`
    2. `getAttribute()`
- `page`
- `config`
- `exception`