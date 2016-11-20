# Chapter 4 Box model 

1. box **无处不在**

2. box 的并列关系和嵌套关系


> preview

<div style="border:1px dashed #333;">
    <div style="color:#666; text-align:center; height:50px; line-height:50px;">margin</div>
    <div style="border:1px solid #ddd; margin:0 50px 50px; background: #ddd;">
        <div style="color:#666; text-align:center; height:20px; line-height:20px;">border</div>
        <div style="margin:0 20px 20px; background:#fff">
            <div style="color:#666; text-align:center; height:30px; line-height:30px;">padding</div>
            <div style="height:50px; color:#333; margin:0 30px 10px; background:#999; color: #fff">
                content
            </div>
<br>

> Source code

```html
<!-- html -->
<div>
    content
</div>    
```

```css
div {
    color: #fff;
    background: #999;
    border: 20px solid #ddd;
    height: 50px;
    margin: 50px;
    pading: 30px;
}
```

- box 之间的边距
  - 并列关系 
    - 块级
      - 垂直外边距取最大值
    - 行内
      - 水平外边距取和
      - 行内元素的宽度 / 高度 / 上下内外边距均无效
  - 嵌套
   - 块级
   - 行内