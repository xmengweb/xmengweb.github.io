---
layout: "@layouts/MarkdownPost.astro"
title: Js常见问题"
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

# JS 常见问题

### 运算符优先级

```JavaScript
 var val = 'smtg';
console.log('Value is ' + (val === 'smtg') ? 'Something' : 'Nothing');
```

在这个例子中，+ 运算符的优先级高于 ? : (三元条件运算符)。所以，表达式会按照以下顺序进行计算：

1. 'Value is ' + (val === 'smtg')，结果为 'Value is true'。
2. 然后计算 'Value is true' ? 'Something' : 'Nothing'，结果为 'Something'。(注意空字符串是 false)

为了得到预期的结果，可以使用括号来改变计算顺序
