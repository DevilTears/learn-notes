# 权重

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
