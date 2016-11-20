# Chapter 5 Float

- 标准流的概念
  
  > 没有 **布局样式** 时，网页呈现的布局

  > 布局样式：`float` `clear` `position` `display` `visibility` 等

- `float` 改变了什么
  1. 浮动的 box 脱离了标准流，原位置被其他 box 占据
  2. 浮动的 box 宽度自适应于内容
  3. 占据浮动 box 的内容在浮动 box 的 `margin` 之外
- 塌缩 `collapse` 的解决
- 清除浮动 `clear`
- 图文混排的实现

    > Source code
    
    ```html
    <!-- index.html -->
    <div>
        <div id="d1">div1...</div>
        <div id="d2">div2...</div>
        <div id="d3">div3...</div>
        <div class="clear"></div>
    </div>    
    ```
    
    ```css
    /* style.css */
    .clear {
        clear: both;
    }
    
    #d1,
    #d2,
    #d3 {
        float: left;
    }
    ```
