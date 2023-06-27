---
layout: "@layouts/MarkdownPost.astro"
title: "面试知识点-JavaScript"
pubDate: 2022-10-01
description: "笔记总结"
author: "XMeng"
cover:
  url: "https://www.geekboots.com/_next/image?url=https%3A%2F%2Fcdn.geekboots.com%2Fgeek%2Fjavascript-hero-1652702096795.webp&w=1080&q=75"
  alt: "cover"
tags: ["JavaScript"]
theme: "light"
featured: true
---

# 面试知识点---JavaScript

# 数据类型

(1)一共有八中数据类型,哪八种? 其中有两种是 es6 新添加的.

> 分别是 Undefined、Null、Boolean、Number、String、Object、Symbol、BigInt。
>
> 其中 Symbol 和 BigInt 是 ES6 中新增的数据类型：
>
> - Symbol 代表创建后独一无二且不可变的数据类型，它主要是为了解决可能出现的全局变量冲突的问题。
> - BigInt 是一种数字类型的数据，它可以表示任意精度格式的整数，使用 BigInt 可以安全地存储和操作大整数，即使这个数已经超出了 Number 能够表示
>   的安全整数范围。

(2)有的数据存在堆区,有的存在栈区，什么是堆什么是栈？存在堆区栈区有什么不一样的？

> - 栈：原始数据类型（Undefined、Null、Boolean、Number、String）
> - 堆：引用数据类型（对象、数组和函数）
>
> 原始数据类型直接存储在栈（stack）中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储；
>
> 引用数据类型存储在堆（heap）中的对象，占据空间大、大小不固定。如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针
> 指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其在栈中的地址，取得地址后从堆中获得实体。
>
> 在数据结构中：
>
> - 在数据结构中，栈中数据的存取方式为先进后出。
> - 堆是一个优先队列，是按优先级来进行排序的，优先级可以按照大小来规定。
>
> 在操作系统中，内存被分为栈区和堆区：
>
> - 栈区内存由编译器自动分配释放，存放函数的参数值，局部变量的值等。其操作方式类似于数据结构中的栈。
> - 堆区内存一般由开发着分配释放，若开发者不释放，程序结束时可能由垃圾回收机制回收。

(3)使用`typeof`可以检测数据类型，但是会出现这样的情况

```javascript
console.log(typeof 2); // number
console.log(typeof true); // boolean
console.log(typeof "str"); // string
console.log(typeof []); // object
console.log(typeof function () {}); // function
console.log(typeof {}); // object
console.log(typeof undefined); // undefined
console.log(typeof null); // object
```

为什么数组,对象,null 最后显示的都是对象? 又该如何解决?

# 原型

### 对象中的原型

- JavaScript 当中每个对象都有一个特殊的内置属性[[prototype]]，这个特殊的属性可以指向另外一个对象(原型对象)。

- 那这个原型对象有什么用呢?

​ 当我们通过引用对象的属性 key 来获取一个 value 时，它会触发[[Get]]的操作;这个操作会首先检查该对象是否有对应的属性，如果有的话就使用它; 如果
对象中没有该属性，那么会访问对象[[prototype]]内置属性指向的对象上的属性;

**只要是对象都会有这样的内置属性**

- 获取的方式有两种: 方式一:通过对象的*proto*属性可以获取到（但是这个是早期浏览器自己添加的，存在一定的兼容性问题); `obj.__proto__`

  方式二:通过 Object.getPrototypeOf 方法可以获取到;

### 函数中的原型

隐式原型

显示原型
