---
layout: "@layouts/MarkdownPost.astro"
title: "Position百分数问题"
pubDate: 2022-11-01
description: "笔记总结"
author: "XMeng"
cover:
  url: "https://i0.wp.com/tw.alphacamp.co/wp-content/uploads/2022/12/60e82825f9d9a8248dc6d7c1_5ec7b9f386cd2e35473558d8_CSS20logo.jpeg?resize=1024%2C536&ssl=1"
  alt: "cover"
tags: ["CSS"]
theme: "light"
featured: true
---

## **百分数是一个相对单位，它的基准是什么呢？是相对于谁的百分比呢？**

![image-20220815180938930](https://cugdemo.oss-cn-hangzhou.aliyuncs.com/image-20220815180938930.png)

**position 为 absolute 的子元素**：

(1) 如果.father 是一个 static 的元素，则.son 的宽 100%是基于 body 说的。跟 body 的宽度一样大。

(2) 但是如果.father 也是一个定位的元素，设置了 relative 或 absolut 或 fixed，则.son 的 width100%就是相对于.father 而言的。否则就是相对于离其
最近的一个拥有定位元素的父元素而言。

**position 为 fixed 的子元素：**

其 width 的 100%是相对于 body 而言。\*\* \*\*

**position 为 relative 的子元素：**

不管直接其父元素是否为定位元素，其 width100%始终是相对于其直接父元素而言的。

**1.当符合 css 默认“继承”的情况下（子元素必须是块级元素且无定位或浮动），是不需要写 width 属性，就可以默认“继承”的。**

**否则就要特殊声明一下 width 属性。**

**2.当使用 width:100%的时候 也要注意其基准点到底是谁：**

（1）对于使用 position:relative 的子元素或浮动的子元素,其基准点始终是基于其直接父元素而言的，跟其父元素是否有定位无关。

（2）对于绝对定位 position:absolute 的子元素，其基准点是相对于离其最近的一层定位父元素而言。如果其所有父级元素均无定位，则是相对于 body 而言
。

（3）对于使用 position:fixed 的子元素，其基准点就是 body。跟父元素无关。
