# CSS

## BFC

可以理解为一个封闭的大箱子，内部元素绝不会影响其外部的元素
BFC 触发条件：

1. body 根元素
2. position: absolute、fixed
3. float 值除 none 外
4. overflow 值除 visible 外（hidden、scroll、 auto）
5. display: inline-block、flex、table-cells

## 块元素和行元素

块元素独占一行，并且会自动填满父元素，可以设置宽高、padding、margin
行元素不会独占一行，设置宽高将会失效，垂直方向 padding、margin 也会失效

## link 标签 和 import 标签的区别

link 属于 html 标签，而 @import 是 css 提供的。
因此 link 没有兼容性，@import只有 IE5 以上才能识别
页面加载时，link 会同步加载，@import 引用的 css 会等到页面加载结束后再加载，但 link 样式的权重高于 @import 的样式。
