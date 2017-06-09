# Nginx

<image src="../image/nginx/Nginx_logo.svg" height="100">

> /engine x/

> 是一个网页服务器，它能反向代理 HTTP, HTTPS, SMTP, POP3, IMAP 的协议链接，以及一个负载均衡器和一个HTTP缓存

1. 代理
    - 中介
2. 正向代理
    - 正向代理隐藏真实客户端
3. 反向代理 `Reverse Proxy`
    - 反向代理隐藏真实服务端
        - 需要有一个负载均衡设备来分发用户请求，将用户请求分发到空闲的服务 
        - 服务器返回自己的服务到负载均衡
        - 负载均衡将服务器的服务返回用户

