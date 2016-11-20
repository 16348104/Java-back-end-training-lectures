# Chapter 3 选择器

## CSS 的 3 种使用方式

> 优先级： 内联 > 内部 = 外部

1. 内联样式 `Inline Styles`

    > Source code
    
    ```html
    <!-- index.html -->
    <h1 style="color: #f00;">headline...</h1>
    ```

2. 内部样式 `Internal Style Sheet`

    > Source code
    
    ```html
    <!-- index.html -->
    <head>
        <style>
            h1 {
                color: #f00;
            }
        </style>
    </head>
    <body>
    <h1>headline...</h1>
    </body>
    ```

3. 外部样式 `External Style Sheet`

    > Source code
    
    ```css
    /* style.css */
    h1 {
        color: #f00;
    }
    ```
    
    ```html
    <!-- index.html -->
    <head>
        <link href="style.css">
    </head>
    <body>
    <h1>headline...</h1>
    </body>
    ``` 

## CSS 选择器

- 基本选择器
    - 标记(元素/标签)选择器
    - `class` 选择器
      - 以 `.` 开头
      - 自定义选择器名
    - `id` 选择器
      - 以 `#` 开头
      - 自定义选择器名
    - `class` 和 `id` 的区别
      - `class` 用 `.` 开头，`id` 用 `#` 开头
      - `class` 值在一个页面中可以使用多次，`id` 只能使用一次
      - `class` 和 `id` 同时存在并发生样式冲突时，`id` 优先级高
      - `class` 可以用空格引用多个值，`id` 不可以
    - 何时用 `class` 何时用 `id`?
- 复合选择器
    - 交集选择器
      - 由元素选择器和 `class` 或 `id` 选择器直连构成
      - 选择二者同时满足的标记
    - 并集选择器
      - 由多个基本选择器使用逗号 `,` 连接
      - 选择所有的标记
    - 派生选择器
      - 由多个基本选择器使用空格 ` ` 连接
      - 选择含有嵌套关系的标记
    
## 伪类 `pseudo-class`

> A pseudo-class is used to define a special state of an element.

- 锚点的 LoVe - HeAt
    
  - `:link`
  - `:visited`
  - `:hover`
  - `:active`
- `:focus`
- `:first-child` 
- `:last-child`
- `:nth-child()`
- `:first-of-type`
 

    
## 伪元素 `pseudo-element`

> A CSS pseudo-element is used to style specified parts of an element.

  - `::before`
  - `::after`
  - `::first-letter`
  - `::first-line`
  - `::selection`


