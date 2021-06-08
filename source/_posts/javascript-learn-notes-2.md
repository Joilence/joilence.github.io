---
title: JavaScript 学习笔记（2）
date: 2016-10-22 14:05:33
tags:
---

## 引用类型

引用类型是一种数据结构，类似 C++ 的类，对象是引用类型的实例。

Object 是 JavaScript 中最常见的引用类型。

构造 Object 对象的方法有两种：1）new + 构造函数。2）使用对象字面量表示法。
``` JavaScript
var person = {
    name: "Jonathan",
    age: 20
}
```

访问对象属性的方法有两种。1）`person["name"]`。2）`person.name`。前者的优势是可以利用另一个字符串变量来访问属性。

## Array 类型

JavaScript Array 与其他语言相似之处就不谈了。

Array 的动态特性：
1）直接修改 length 改变其长度。
2）直接给 Array 某一位元素赋值即可修改或者*添加*元素。
3）使用 `people[people.length] = "Jonathan"` 即可方便的在末尾追加元素。

Array 最多可以包含 4,294,967,295 个元素。

检测 Array 的两种方法：
1）Array.isArray()。
2）instanceof （有缺陷，它假定只有一个全局环境。若包含多个框架，存在不同版本的 Array 构造函数，就会返回错误结果）

## Function 类型

JavaScript 中的函数实际上是对象，是 Function 类型的实例。

函数内部有两个特殊对象：arguments 和 this。
1）arguments 包含传入参数的类数组对象。该对象拥有 callee 属性指针，指向拥有这个 arguments 对象的函数。
2）this 引用函数执行的环境对象。

Function 拥有两个属性：length 和 prototype。

使用 call() 和 apply() 函数可以扩展函数运行的作用域，而对象和方法不需要有任何耦合关系。

bind() 函数返回一个绑定作用域的函数版本。`objectFunction = generalFunction.bind(object)`。

单体内置对象：
Global 对象，window 对象，eval 方法（关系到代码注入），Math 对象，暂不详细展开，仅做记录。


参考文献：
《JavaScript 高级程序设计》第五章

