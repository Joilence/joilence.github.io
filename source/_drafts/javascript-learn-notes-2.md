---
title: JavaScript 学习笔记（2）
tags:
---

HTML 中 `<script>` 标签可添加 defer 属性和 async 属性。

`<noscript>` 标签的使用。

typeof null 将返回 object。undefined 派生自 null，所以 null == undefined 将返回 true。

NaN 与任何数都不想等，包括 NaN 自己。所以有了 isNaN()。

全等与相等。由于 JavaScript 是弱类型语言，『相等』判断是判断经过转换后的值，『全等』才是直接判断。

JavaScript 的 with 语句设置特定作用域。
``` JavaScript
var aa = s.a;
var bb = s.b;
var cc = s.c;
// 可用 with
with (s) {
    var aa = a;
    var bb = b;
    var cc = c;
}
```

ECMAScript 不存在函数签名，所以不能够进行函数重载。

参考文献：
《JavaScript 高级编程艺术》 第一章至第三章

