---
layout: post
title: Vue SSR Overview
subtitle: Vuejs基础使用
date: 2020-07-22
author: Jalever
header-img: img/vue_bg.jpeg
catalog: true
tags:
  - Vue
---

- [基础了解](#基础了解)
    - [什么是服务器端渲染(SSR)](#什么是服务器端渲染ssr)
    - [为什么使用服务器端渲染(SSR)](#为什么使用服务器端渲染ssr)

## 基础了解
#### 什么是服务器端渲染(SSR)
`Vue.js` 是构建客户端应用程序的框架。默认情况下，可以在浏览器中输出 `Vue` 组件，进行生成 `DOM` 和操作 `DOM`。然而，也可以将同一个组件渲染为服务器端的 `HTML` 字符串，将它们直接发送到浏览器，最后将这些静态标记"激活"为客户端上完全可交互的应用程序

服务器渲染的 `Vue.js` 应用程序也可以被认为是"同构"或"通用"，因为应用程序的大部分代码都可以在服务器和客户端上运行

#### 为什么使用服务器端渲染(SSR)
与传统 SPA（Single-Page Application - 单页应用程序）相比，服务器端渲染(SSR)的优势主要在于：

- 更好的 SEO，由于搜索引擎爬虫抓取工具可以直接查看完全渲染的页面。
- 更快的内容到达时间(time-to-content)，特别是对于缓慢的网络情况或运行缓慢的设备


