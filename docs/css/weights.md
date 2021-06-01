# 权重

## css 选择器

id、class、标签、伪元素、伪类
id > class > 标签
带有!important 标记的样式属性的优先级最高；
内联样式> 内部样式 > 外部样式 > 浏览器用户自定义样式 > 浏览器默认样式

分组选择器：，如：div ,p {...}，div 和 p 将有同样的样式

组合器：
后代选择器：空格 div p {}，div 下的所有 p 的样式
直接子代：ul > li {}，ul 下的 直级 li 的样式
一般兄弟：～，p ~ span {}，同一个父元素下，p 后面的 所有 span
紧邻兄弟：+，p + span {}，同一个父元素下，p 后面的 所有 紧邻的 span

伪选择器：
伪类：a: visited、hover
伪元素：first-child

## 根据代码写出各文字的颜色（或颜色值）

> 题目来源：2020.12-好未来

```html
<div class="box">
  第一行字  // #000
  <div id="second" class="second">第二行字</div> // #0f0
  <div class="third" style="color: #f00;">第三行字</div> // #00f
</div>

<style>
  .box {
    color: #000;
  }

  #second {
    color: #f00;
  }

  .box .second {
    color: #0f0;
  }

  .third {
    color: #00f !important;
  }
</style>
```
