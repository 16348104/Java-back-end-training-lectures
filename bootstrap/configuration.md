# Chapter 2 基本配置

1. Download latest Bootstrap (currently v3.3.6)
  - [download Bootstrap](http://getbootstrap.com/getting-started/#download)
2. Create first HTML file
3. Add Bootstrap component
  - `<meta name="viewport" content="width=device-width, initial-scale=1">`
  - `bootstrap.min.css`
  - `jquery.js`
  - `bootstrap.min.js`
  - a basic `container` or `container-fluid` div in the body
    - `container` 固定宽度并支持响应式布局的容器
    - `container-fluid` 100% 宽度，占据全部视口（viewport）的容器

> source code

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>index page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <link rel="stylesheet" href="static/bootstrap/css/bootstrap.min.css">
      <script src="static/js/jquery-1.11.2.min.js"></script>
      <script src="static/bootstrap/js/bootstrap.min.js"></script>
  </head>
  <body>
  <div class="container">
      <h1>Hello, Bootstrap!</h1>
      <p>p...</p>
  </div>
  </body>
  </html>
  ```