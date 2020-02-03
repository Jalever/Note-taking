---
layout: post
title: Vue Interview Questions
subtitle: Advanced Vue Interview Questions
date: 2020-02-02
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Interview Questions
---

- [`v-show` 与 `v-if` 有什么区别?](#v-show-%e4%b8%8e-v-if-%e6%9c%89%e4%bb%80%e4%b9%88%e5%8c%ba%e5%88%ab)
- [说说你对 SPA 单页面的理解，它的优缺点分别是什么?](#%e8%af%b4%e8%af%b4%e4%bd%a0%e5%af%b9-spa-%e5%8d%95%e9%a1%b5%e9%9d%a2%e7%9a%84%e7%90%86%e8%a7%a3%e5%ae%83%e7%9a%84%e4%bc%98%e7%bc%ba%e7%82%b9%e5%88%86%e5%88%ab%e6%98%af%e4%bb%80%e4%b9%88)
- [`Class` 与 `Style` 如何动态绑定?](#class-%e4%b8%8e-style-%e5%a6%82%e4%bd%95%e5%8a%a8%e6%80%81%e7%bb%91%e5%ae%9a)

#### `v-show` 与 `v-if` 有什么区别?

`v-if` 是"真正"的条件渲染, 因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建

`v-if` 也是惰性的: 如果在初始渲染时条件为假, 则什么也不做——直到条件第一次变为真时, 才会开始渲染条件块

相比之下, `v-show` 就简单得多——不管初始条件是什么, 元素总是会被渲染, 并且只是简单地基于 `CSS` 进行切换

一般来说，`v-if` 有更高的切换开销, 而 `v-show` 有更高的初始渲染开销. 因此，如果需要非常频繁地切换, 则使用 `v-show` 较好; 如果在运行时条件很少改变，则使用 `v-if` 较好

#### 说说你对 SPA 单页面的理解，它的优缺点分别是什么?

SPA( Single-Page Application ) 仅在 `Web` 页面初始化时加载相应的 `HTML`、`JavaScript` 和 `CSS`。一旦页面加载完成，`SPA` 不会因为用户的操作而进行页面的重新加载或跳转；取而代之的是利用路由机制实现 `HTML` 内容的变换，`UI` 与用户的交互，避免页面的重新加载

优点:

- 用户体验好、快，内容的改变不需要重新加载整个页面，避免了不必要的跳转和重复渲染；
- 基于上面一点，`SPA` 相对对服务器压力小；
- 前后端职责分离，架构清晰，前端进行交互逻辑，后端负责数据处理

缺点:

- 初次加载耗时多：为实现单页 `Web` 应用功能及显示效果，需要在加载页面的时候将 `JavaScript`、`CSS` 统一加载，部分页面按需加载；
- 前进后退路由管理：由于单页应用在一个页面中显示所有的内容，所以不能使用浏览器的前进后退功能，所有的页面切换需要自己建立堆栈管理；
- `SEO` 难度较大：由于所有的内容都在一个页面中动态替换显示，所以在 `SEO` 上其有着天然的弱势

#### `Class` 与 `Style` 如何动态绑定?

`Class` 可以通过对象语法和数组语法进行动态绑定:

对象语法:

```js
<div v-bind:class="{ active: isActive, 'text-danger': hasError }"></div>

data: {
  isActive: true,
  hasError: false
}
```

数组语法:

```js
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>

data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}
```

`Style` 也可以通过对象语法和数组语法进行动态绑定:

对象语法:

```js
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>

data: {
  activeColor: 'red',
  fontSize: 30
}
```

数组语法:

```js
<div v-bind:style="[styleColor, styleSize]"></div>

data: {
  styleColor: {
     color: 'red'
   },
  styleSize:{
     fontSize:'23px'
  }
}
```
