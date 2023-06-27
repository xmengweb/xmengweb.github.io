---
layout: "@layouts/MarkdownPost.astro"
title: "在 Node.js 中 选择 CommonjS 还是 ES modules"
pubDate: 2023-06-01
author: "XMeng"
cover:
  url: "https://developers.redhat.com/sites/default/files/styles/article_feature/public/blog/2015/04/node-js.jpg?itok=cdmkPTqM"
  alt: "cover"
tags: ["NodeJs"]
theme: "light"
featured: true
---

# 在 Node.js 中 选择 CommonjS 还是 ES modules ?

在浏览器 JavaScript 生态系统中，JavaScript 模块的使用依赖于`import`and`export`语句；

ES 模块格式是打包 JavaScript 代码以供重用的官方标准格式，大多数现代 Web 浏览器都原生支持这些模块。

然而，Node.js 默认支持 CommonJS 模块格式。

ES 模块格式
在[Node.js v8.5.0 中被引入。](https://link.juejin.cn?target=https%3A%2F%2Fgithub.com%2Fnodejs%2Fnode%2Fblob%2Fmaster%2Fdoc%2Fchangelogs%2FCHANGELOG_V8.md%238.5.0)作
为一个实验模块，但是，2020 年 5 月，Node.js
[v12.17.0](https://link.juejin.cn?target=https%3A%2F%2Fgithub.com%2Fnodejs%2Fnode%2Fblob%2Fmaster%2Fdoc%2Fchangelogs%2FCHANGELOG_V12.md%232020-05-26-version-12170-erbium-lts-targos)为
所有 Node.js 应用程序提供了 ESM 支持，Node.js 已经稳定支持 ES 模块。

## 在 Node.js 中使用 ES 模块和 CommonJS 模块的优缺点

**ES 模块是 JavaScript 的标准，而 CommonJS 是 Node.js 中的默认** CommonJS 模块系统内置于 Node.js 中。在 Node.js 中引入 ES 模块之前，CommonJS
是 Node.js 模块的标准。因此，有大量使用 CommonJS 编写的 Node.js 库和模块。

**旧的 Node.js 版本不支持 ES 模块** 使用 ES 模块会导致应用程序与仅支持 CommonJS 模块的早期版本的 Node.js 不兼容

**CommonJS 提供模块导入的灵活性** ESModule 只能在顶级作用域中*导入*相比于*CommonJS*失去了更大的自由度和*灵活性*

**CommonJS 加载模块是同步的，ES 模块是异步的**

**在所有的 ES 模块导入中，需要明确地将文件扩展名添加到所有文件导入中** 这对于 ES 模块是强制性的,就是
说`require('./')必须写为import .. from './index.js'`(在 typescript 中也必须这样写！)

**CommonJS 导入在运行时动态解析** `require()`函数只是在我们的代码执行时运行。因此可以在代码中的任何地方调用它。

**对于 ES 模块，导入是静态的，这意味着它们在解析时执行** 静态导入可以提高程序的执行效率,出现问题也能第一时间知道

## 现象

### 一些著名的库作者开始讨论将他们的包迁移到*仅*支持 ESM

随着 Node.js v10 在 2021 年 4 月接近其生命周期结束日期,一些著名的库作者开始讨论将他们的包迁移到*仅*支持 ESM,比如拥有 17.9k star 的命令行交互
工具 inquirer，在去年六月已经完全迁入到 esm 甚至要求必须使用 typescript 时必须编译为 ESM

![，](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f7725ac2ea1646d683d70b0c9effc1b3~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0ee0558dd0b144438c42da255ad06b0d~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)
**拥有 8.7k star 的 ora 库也转为 ESM，并给出了十分详细的所有情况下
的[使用方法](https://link.juejin.cn?target=https%3A%2F%2Fgist.github.com%2Fsindresorhus%2Fa39789f98801d908bbc7ff3ecc99d99c)**
![image-20230506195652846](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/96ea873e73fb474fb97325c5e7dc6d00~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

### 但是@tsconfig/node20 针对 Node.js 20 的项目提供的推荐编译器选项仍是 commonjs

![image-20230506192330185](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5759065e2aef460eafe5f73e2b917582~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp)

## 思考

对于仍在使用旧版本 Node.js 的开发人员来说，使用新的 ES 模块是不切实际的。

由于粗略的支持，将现有项目转换为 ES 模块会使应用程序与仅支持 CommonJS 模块的早期版本的 Node.js 不兼容。``

因此，将项目迁移到使用 ES 模块可能不是特别有益。

对于新的 Node.js 项目，ES 模块提供了 CommonJS 的替代方案。ES 模块格式确实提供了一种编写同构 JavaScript 的更简单途径，它可以在浏览器或服务器
上运行。是完全可以选择使用 ES 模块替代 CommonJS

**如果要开始一个新项目，请使用 ES 模块**。它已经标准化多年了。自 2020 年 4 月发布的第 14 版以来，NodeJS 对其提供了稳定的支持。您可以在那里找
到很多文档和示例。许多包维护者已经发布了支持 ES 模块的库。没有理由不使用它。

**如果正在维护一个使用 CommonJS 的现有 NodeJS 项目，情况可能会有所不同**。最重要的事实是，目前没有迁移现有代码的压力。CommonJS 仍然是 NodeJS
的默认模块系统，并且没有迹象表明这会很快改变。但是，您可能会在底层使用 CommonJS 时迁移到 ES 模块语法。这可以通过 Babel 或 TypeScript 等工具
来完成，并允许您决定在以后的某个时间点更轻松地切换到 ES 模块。

## 参考文章

[官方 ESM 指南](https://link.juejin.cn?target=https%3A%2F%2Fwww.typescriptlang.org%2Fdocs%2Fhandbook%2Fesm-node.html)

[Getting Started with (and Surviving) Node.js ESM](https://link.juejin.cn?target=https%3A%2F%2Fformidable.com%2Fblog%2F2021%2Fnode-esm-and-exports%2F)

[@tsconfig/node20](https://link.juejin.cn?target=https%3A%2F%2Fwww.npmjs.com%2Fpackage%2F%40tsconfig%2Fnode20)

[CommonJS vs. ES modules in Node.js](https://link.juejin.cn?target=https%3A%2F%2Fblog.logrocket.com%2Fcommonjs-vs-es-modules-node-js%2F)

[How to Setup a TypeScript + Node.js Project ](https://link.juejin.cn?target=https%3A%2F%2Fkhalilstemmler.com%2Fblogs%2Ftypescript%2Fnode-starter-project%2F)

[Using ECMAScript modules (ESM) with Node.js](https://link.juejin.cn?target=https%3A%2F%2Fblog.logrocket.com%2Fhow-to-use-ecmascript-modules-with-node-js%2F)

[CommonJS vs. ES Modules: Modules and Imports in NodeJS](https://link.juejin.cn?target=https%3A%2F%2Freflectoring.io%2Fnodejs-modules-imports%2F)
