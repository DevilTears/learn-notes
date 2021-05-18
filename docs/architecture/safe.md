# 浏览器安全

## 转译避免XSS注入攻击的符合都有那些

> 题目来源：2020.12 好未来

```js
str = str.replace(/&/g, '&amp;')
str = str.replace(/</g, '&lt;')
str = str.replace(/>/g, '&gt;')
str = str.replace(/"/g, '&quto;')
str = str.replace(/'/g, '&#39;')
str = str.replace(/`/g, '&#96;')
str = str.replace(/\//g, '&#x2F;')
