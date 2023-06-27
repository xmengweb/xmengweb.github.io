---
layout: "@layouts/MarkdownPost.astro"
title: "在 nodejs 中结合 ts 使用 esm"
pubDate: 2023-5-12
description: "笔记总结"
author: "XMeng"
cover:
  url: "https://developers.redhat.com/sites/default/files/styles/article_feature/public/blog/2015/04/node-js.jpg?itok=cdmkPTqM"
  alt: "cover"
tags: ["NodeJs"]
theme: "light"
featured: true
---

## 在 nodejs 中结合 ts 使用 esm

- nodejs 中使用 esm 必须要有后缀,所以在 ts 中需要指明为 js, `import { createCommand } from "./core/create.js";` 否则 ts 编译后没有后缀, 这在
  nodejs 中的 esm 中是不支持的.
- 添加`"type": "module"`到您的 package.json。
- "node": ">=14.16"
- 将所有`require()`/替换`module.export`为`import`/ `export`

使用 ts-node: `npx ts-node-esm index.ts `

或者`tsc index.ts --watch` `node index.js`
