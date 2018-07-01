---
title: JavaScript 学习笔记（1）
date: 2016-10-19 20:40:10
tags:
---

JavaScript 是一种弱类型、动态的语言，体现在对象类型不固定，可随时增删属性与方法。

JavaScript 的对象均为引用传递，无按值传递。

函数相关 {
    `function func()` 声明具有声明提升的特性，即函数可在调用之后声明，但是 `var func = function` 匿名函数声明则不具备。
}

闭包 {
    阮一峰博客中的理解是：闭包就是能够读取其他函数内部变量的函数。
    
> 1）由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。
> 2）闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。
}

使用 `var that = this` 方法使得闭包函数可以调用外部函数的 this。

由于 JavaScript 不存在块级作用域，如 for 循环中暂时使用的 i，会在函数内部任何一处有效。为防止潜在的不稳定因素，可以通过匿名函数来模仿块级作用域（私有作用域）。

一些 OO 编程传统特性实现的奇技淫巧 {

**私有变量**

``` javascript
function MyObject() {
    // Private Member
    var privateVar = 10;
    function privateFunc {}
    // Public Method
    this.publicMethod = {
        return privateFunc;
    }
}
```

上述代码中，除了 PublicMethod 这一途径，没有任何方法访问其私有成员。

**静态私有变量**

``` javascript
(function() {
    // Private Member
    var privateVar = 10;
    function privareFunc() {}
    // Constructor
    MyObject = function() {} // Make it global without 'var'
    // Public Method
    MyObject.prototype.publicMethod = function() {}
})();
```

**单例模式**

``` javascript
var singleton = function() {
    // Private Member
    var privateVar = 10;
    function privateFunc() {}
    // Public Method
    return {
        publicVar: true,
        publicMethod: function() {
            return privateFunc();
        }
    }
}
```

**确定类型的单例模式**
只需要在原型内创建对象，`var object = customType()`，最后返回 `return object` 即可。公共接口也可以借由该 object 添加。
}

> 如何实现一个完善的对象，同时具备私有变量和静态私有变量？


上周踩到的一个坑 {
document.getElementByClassName() 返回的不是一个简单的数组，而是 HTMLCollection 对象。这个集合对象是动态的：当文档改变时，其改变都会影响 HTMLCollection 的内容。

这样一来，想要使某个 class 的所有元素改变到另一个 class，使用如下代码即可：

``` javascript
var elements = document.getElementByClassName("old-class");
while (elements.length) {
    elements[0].className = "new-class"
}
```
}

参考文献：
《JavaScript 高级程序设计》 第七章
[学习Javascript闭包（Closure） - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)


