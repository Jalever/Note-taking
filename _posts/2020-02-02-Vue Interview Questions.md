---
layout: post
title: Vue Interview Questions
subtitle: Advanced Vue Interview Questions
date: 2020-02-02
author: Jalever
header-img: img/post_bg_fancyCrave.jpg
catalog: true
tags:
  - Interview Questions
---

- [`v-show` 与 `v-if` 有什么区别?](#v-show-%e4%b8%8e-v-if-%e6%9c%89%e4%bb%80%e4%b9%88%e5%8c%ba%e5%88%ab)
- [说说你对 SPA 单页面的理解，它的优缺点分别是什么?](#%e8%af%b4%e8%af%b4%e4%bd%a0%e5%af%b9-spa-%e5%8d%95%e9%a1%b5%e9%9d%a2%e7%9a%84%e7%90%86%e8%a7%a3%e5%ae%83%e7%9a%84%e4%bc%98%e7%bc%ba%e7%82%b9%e5%88%86%e5%88%ab%e6%98%af%e4%bb%80%e4%b9%88)
- [`Class` 与 `Style` 如何动态绑定?](#class-%e4%b8%8e-style-%e5%a6%82%e4%bd%95%e5%8a%a8%e6%80%81%e7%bb%91%e5%ae%9a)
- [computed 和 watch 的区别和运用的场景](#computed-%e5%92%8c-watch-%e7%9a%84%e5%8c%ba%e5%88%ab%e5%92%8c%e8%bf%90%e7%94%a8%e7%9a%84%e5%9c%ba%e6%99%af)

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

#### `computed` 和 `watch` 的区别和运用的场景

`computed`: 是计算属性，依赖其它属性值，并且 `computed` 的值有缓存，只有它依赖的属性值发生改变，下一次获取 `computed` 的值时才会重新计算 `computed` 的值;

`watch`: 更多的是「观察」的作用，类似于某些数据的监听回调 ，每当监听的数据变化时都会执行回调进行后续操作;

运用场景：

- 当我们需要进行数值计算，并且依赖于其它数据时，应该使用 `computed`，因为可以利用 `computed` 的缓存特性，避免每次获取值时，都要重新计算;

- 当我们需要在数据变化时执行异步或开销较大的操作时，应该使用 `watch`，使用  `watch`  选项允许我们执行异步操作 ( 访问一个 `API` )，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的

#### 怎样理解 Vue 的单向数据流?

所有的 `prop` 都使得其父子 `prop` 之间形成了一个单向下行绑定：父级 `prop` 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外改变父级组件的状态，从而导致你的应用的数据流向难以理解。
额外的，每次父级组件发生更新时，子组件中所有的 `prop` 都将会刷新为最新的值。这意味着你不应该在一个子组件内部改变 `prop`。如果你这样做了，Vue 会在浏览器的控制台中发出警告。子组件想修改时，只能通过 \$emit 派发一个自定义事件，父组件接收到后，由父组件修改。
有两种常见的试图改变一个 `prop` 的情形

- 这个 `prop` 用来传递一个初始值；这个子组件接下来希望将其作为一个本地的 `prop` 数据来使用。 在这种情况下，最好定义一个本地的 `data` 属性并将这个 `prop` 用作其初始值:

```js
props: ['initialCounter'],
data: function () {
  return {
    counter: this.initialCounter
  }
}
```

- 这个 prop 以一种原始的值传入且需要进行转换。 在这种情况下，最好使用这个 prop 的值来定义一个计算属性

```js
props: ['size'],
computed: {
  normalizedSize: function () {
    return this.size.trim().toLowerCase()
  }
}
```

#### 直接给一个数组项赋值，Vue 能检测到变化吗?

由于 `JavaScript` 的限制, Vue 不能检测到以下数组的变动:

- 当你利用索引直接设置一个数组项时, 例如: `vm.items[indexOfItem] = newValue`
- 当你修改数组的长度时，例如: `vm.items.length = newLength`

为了解决第一个问题, Vue 提供了以下操作方法:

```js
// Vue.set
Vue.set(vm.items, indexOfItem, newValue);
// vm.$set，Vue.set的一个别名
vm.$set(vm.items, indexOfItem, newValue);
// Array.prototype.splice
vm.items.splice(indexOfItem, 1, newValue);
```

为了解决第二个问题，Vue 提供了以下操作方法:

```js
// Array.prototype.splice
vm.items.splice(newLength);
```

#### 谈谈你对 Vue 生命周期的理解?

1. 生命周期是什么?
`Vue` 实例有一个完整的生命周期，也就是从开始创建、初始化数据、编译模版、挂载Dom -> 渲染、更新 -> 渲染、卸载等一系列过程，我们称这是 Vue 的生命周期

2. 各个生命周期的作用
   | 生命周期      |                                 描述                                  |
   | ------------- | :-------------------------------------------------------------------: |
   | beforeCreate  |                组件实例被创建之初，组件的属性生效之前                 |
   | created       | 组件实例已经完全创建，属性也绑定，但真实 dom 还没有生成，$el 还不可用 |
   | beforeMount   |          在挂载开始之前被调用：相关的 render 函数首次被调用           |
   | mounted       |       el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子       |
   | beforeUpdate  |            组件数据更新之前调用，发生在虚拟 DOM 打补丁之前            |
   | update        |                           组件数据更新之后                            |
   | activited     |                   keep-alive 专属，组件被激活时调用                   |
   | deactivated   |                   keep-alive 专属，组件被销毁时调用                   |
   | beforeDestory |                            组件销毁前调用                             |
   | destoryed     |                            组件销毁后调用                             |

3) 生命周期示意图
[![1NHiSe.md.png](https://s2.ax1x.com/2020/02/03/1NHiSe.md.png)](https://imgchr.com/i/1NHiSe)

## 参考

- 我是你的超级英雄.[30 道 Vue 面试题，内含详细讲解](https://juejin.im/post/5d59f2a451882549be53b170#heading-4)
