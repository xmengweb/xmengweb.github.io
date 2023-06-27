---
layout: "@layouts/MarkdownPost.astro"
title: "Vue的Bug总结"
pubDate: 2022-12-01
description: "BUG总结"
author: "XMeng"
cover:
  url: "https://positivethinking.tech/wp-content/uploads/2021/01/Logo-Vuejs.png"
  alt: "cover"
tags: ["Vue"]
theme: "light"
featured: true
---

# Vue 的 Bugs 总结

## 解决 Vue 中 keyup.enter 和 blur 绑定同一事件，触发多次以及可能出现死循环的问题

我现在有一个需求就是有一个 input 框,里面输入一些数据之后既可以通过鼠标点击失去焦点来保存,也可以通过回车来保存
.![动画](https://cugdemo.oss-cn-hangzhou.aliyuncs.com/%E5%8A%A8%E7%94%BB.gif)

遇到了一些问题:

1. 首先是当我使用回车键之后,blur 事件也会调用一次,代表着我回车之后执行了两次,不过这个似乎对用户没有什么影响但是会导致一个更严重的 bug
2. 当用户输入为空,会弹窗提示,所以当用户回车确定之后,首先调用 keyup 对应的事件,弹窗提醒一次,然后 blur 事件也会调用再去提醒一次,此时点击确定之
   后,再次会调用 blur 事件,导致输入框一直为空,一直提示,这就严重了!

解决方法:

`@keyup.enter.native="$event.target.blur"`

​ 将 keyup 事件设置为触发 blur，这样：如果 blur 了，执行 handleblur 函数；如果 keyup 了，执行 blur，blur 会执行 handleblur。

![img](https://www.programminghunter.com/images/520/b9/b9343eb69c85d46a3b9196d2674b4c18.png)

这样所然我按得是回车键,但是即使就是 blur,实现了同样的功能而且只调用一次.

注意:

若报错:![在这里插入图片描述](https://img-blog.csdnimg.cn/e81609c60e2a4facbce9201d6e4ef6c4.png)

需要修改为`$event.target.blur()
