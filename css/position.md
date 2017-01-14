# Chapter 6 Position & display & visibility

## `position`

- 静态定位
    - 标准流
- 相对定位
    - 没有脱离标准流
    - 相对于自己原来的位置
- 绝对定位
    - 脱离了标准流
    - 相对于距离它 **最近的** **已定位** 的 **祖先元素**
        - 已定位指 `position` 值不是 `static`
- 固定定位
    - 脱离了标准流
    - 相对浏览器的最左上角
- 偏移量
    - `top`
    - `left`
    - `right`
    - `bottom`
- `z-index`
    - 对于已定位元素，值越大越靠近上边
    
## `display`

- `inline` 块级变行内
- `block` 行内变块级
- `inline-block` 对外行内，对内块级
- `none` 不显示且不保留位置

## `visibility`
- `hidden` 不显示但保留位置