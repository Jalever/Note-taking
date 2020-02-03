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

- [Common Interview Questions](#common-interview-questions)
    - [`Vue` 与 `React` 的区别?](#vue-%e4%b8%8e-react-%e7%9a%84%e5%8c%ba%e5%88%ab)
    - [`v-show` 与 `v-if` 有什么区别?](#v-show-%e4%b8%8e-v-if-%e6%9c%89%e4%bb%80%e4%b9%88%e5%8c%ba%e5%88%ab)
    - [说说你对 SPA 单页面的理解，它的优缺点分别是什么?](#%e8%af%b4%e8%af%b4%e4%bd%a0%e5%af%b9-spa-%e5%8d%95%e9%a1%b5%e9%9d%a2%e7%9a%84%e7%90%86%e8%a7%a3%e5%ae%83%e7%9a%84%e4%bc%98%e7%bc%ba%e7%82%b9%e5%88%86%e5%88%ab%e6%98%af%e4%bb%80%e4%b9%88)
    - [`Class` 与 `Style` 如何动态绑定?](#class-%e4%b8%8e-style-%e5%a6%82%e4%bd%95%e5%8a%a8%e6%80%81%e7%bb%91%e5%ae%9a)
    - [`computed` 和 `watch` 的区别和运用的场景](#computed-%e5%92%8c-watch-%e7%9a%84%e5%8c%ba%e5%88%ab%e5%92%8c%e8%bf%90%e7%94%a8%e7%9a%84%e5%9c%ba%e6%99%af)
    - [怎样理解 Vue 的单向数据流?](#%e6%80%8e%e6%a0%b7%e7%90%86%e8%a7%a3-vue-%e7%9a%84%e5%8d%95%e5%90%91%e6%95%b0%e6%8d%ae%e6%b5%81)
    - [直接给一个数组项赋值，Vue 能检测到变化吗?](#%e7%9b%b4%e6%8e%a5%e7%bb%99%e4%b8%80%e4%b8%aa%e6%95%b0%e7%bb%84%e9%a1%b9%e8%b5%8b%e5%80%bcvue-%e8%83%bd%e6%a3%80%e6%b5%8b%e5%88%b0%e5%8f%98%e5%8c%96%e5%90%97)
    - [谈谈你对 Vue 生命周期的理解?](#%e8%b0%88%e8%b0%88%e4%bd%a0%e5%af%b9-vue-%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f%e7%9a%84%e7%90%86%e8%a7%a3)
    - [在哪个生命周期内调用异步请求?](#%e5%9c%a8%e5%93%aa%e4%b8%aa%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f%e5%86%85%e8%b0%83%e7%94%a8%e5%bc%82%e6%ad%a5%e8%af%b7%e6%b1%82)
    - [Vue 的父组件和子组件生命周期钩子函数执行顺序?](#vue-%e7%9a%84%e7%88%b6%e7%bb%84%e4%bb%b6%e5%92%8c%e5%ad%90%e7%bb%84%e4%bb%b6%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f%e9%92%a9%e5%ad%90%e5%87%bd%e6%95%b0%e6%89%a7%e8%a1%8c%e9%a1%ba%e5%ba%8f)
    - [在什么阶段才能访问操作DOM?](#%e5%9c%a8%e4%bb%80%e4%b9%88%e9%98%b6%e6%ae%b5%e6%89%8d%e8%83%bd%e8%ae%bf%e9%97%ae%e6%93%8d%e4%bd%9cdom)
    - [父组件可以监听到子组件的生命周期吗?](#%e7%88%b6%e7%bb%84%e4%bb%b6%e5%8f%af%e4%bb%a5%e7%9b%91%e5%90%ac%e5%88%b0%e5%ad%90%e7%bb%84%e4%bb%b6%e7%9a%84%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f%e5%90%97)
    - [谈谈你对 `keep-alive` 的了解?](#%e8%b0%88%e8%b0%88%e4%bd%a0%e5%af%b9-keep-alive-%e7%9a%84%e4%ba%86%e8%a7%a3)
    - [组件中 `data` 为什么是一个函数?](#%e7%bb%84%e4%bb%b6%e4%b8%ad-data-%e4%b8%ba%e4%bb%80%e4%b9%88%e6%98%af%e4%b8%80%e4%b8%aa%e5%87%bd%e6%95%b0)
    - [`v-model` 的原理?](#v-model-%e7%9a%84%e5%8e%9f%e7%90%86)
    - [`Vue` 组件间通信有哪几种方式?](#vue-%e7%bb%84%e4%bb%b6%e9%97%b4%e9%80%9a%e4%bf%a1%e6%9c%89%e5%93%aa%e5%87%a0%e7%a7%8d%e6%96%b9%e5%bc%8f)
        - [1.`props` / `$emit` 适用于父子组件通信](#1props--emit-%e9%80%82%e7%94%a8%e4%ba%8e%e7%88%b6%e5%ad%90%e7%bb%84%e4%bb%b6%e9%80%9a%e4%bf%a1)
        - [2.`$parent / $children` 适用 父子组件通信](#2parent--children-%e9%80%82%e7%94%a8-%e7%88%b6%e5%ad%90%e7%bb%84%e4%bb%b6%e9%80%9a%e4%bf%a1)
        - [3.EventBus(`$emit` / `$on`) 适用于 父子、隔代、兄弟组件通信](#3eventbusemit--on-%e9%80%82%e7%94%a8%e4%ba%8e-%e7%88%b6%e5%ad%90%e9%9a%94%e4%bb%a3%e5%85%84%e5%bc%9f%e7%bb%84%e4%bb%b6%e9%80%9a%e4%bf%a1)
        - [4.`$attrs` / `$listeners` 适用于 隔代组件通信](#4attrs--listeners-%e9%80%82%e7%94%a8%e4%ba%8e-%e9%9a%94%e4%bb%a3%e7%bb%84%e4%bb%b6%e9%80%9a%e4%bf%a1)
        - [5.`provide` / `inject` 适用于 隔代组件通信](#5provide--inject-%e9%80%82%e7%94%a8%e4%ba%8e-%e9%9a%94%e4%bb%a3%e7%bb%84%e4%bb%b6%e9%80%9a%e4%bf%a1)
        - [6.`Vuex` 适用于 父子、隔代、兄弟组件通信](#6vuex-%e9%80%82%e7%94%a8%e4%ba%8e-%e7%88%b6%e5%ad%90%e9%9a%94%e4%bb%a3%e5%85%84%e5%bc%9f%e7%bb%84%e4%bb%b6%e9%80%9a%e4%bf%a1)
- [参考](#%e5%8f%82%e8%80%83)

## Common Interview Questions
#### `Vue` 与 `React` 的区别?

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
   `Vue` 实例有一个完整的生命周期，也就是从开始创建、初始化数据、编译模版、挂载 Dom -> 渲染、更新 -> 渲染、卸载等一系列过程，我们称这是 `Vue` 的生命周期

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

3. 生命周期示意图
   [![1NHiSe.md.png](https://s2.ax1x.com/2020/02/03/1NHiSe.md.png)](https://imgchr.com/i/1NHiSe)

#### 在哪个生命周期内调用异步请求?
可以在钩子函数 `created`、`beforeMount`、`mounted` 中进行调用，因为在这三个钩子函数中，`data` 已经创建，可以将服务端端返回的数据进行赋值。但是本人推荐在 `created` 钩子函数中调用异步请求，因为在 `created` 钩子函数中调用异步请求有以下优点:
- 能更快获取到服务端数据，减少页面 loading 时间；
- `ssr` 不支持 `beforeMount` 、`mounted` 钩子函数，所以放在 `created` 中有助于一致性

#### Vue 的父组件和子组件生命周期钩子函数执行顺序?
Vue 的父组件和子组件生命周期钩子函数执行顺序可以归类为以下 4 部分:
- 加载渲染过程
父 beforeCreate -> 父 created -> 父 beforeMount -> 子 beforeCreate -> 子 created -> 子 beforeMount -> 子 mounted -> 父 mounted

- 子组件更新过程
父 beforeUpdate -> 子 beforeUpdate -> 子 updated -> 父 updated

- 父组件更新过程
父 beforeUpdate -> 父 updated

- 销毁过程
父 beforeDestroy -> 子 beforeDestroy -> 子 destroyed -> 父 destroyed

#### 在什么阶段才能访问操作DOM?
在钩子函数 `mounted` 被调用前，`Vue` 已经将编译好的模板挂载到页面上，所以在 `mounted` 中可以访问操作 `DOM`

#### 父组件可以监听到子组件的生命周期吗?
比如有父组件 Parent 和子组件 Child，如果父组件监听到子组件挂载 mounted 就做一些逻辑处理，可以通过以下写法实现:
```js
// Parent.vue
<Child @mounted="doSomething"/>
    
// Child.vue
mounted() {
  this.$emit("mounted");
}
```

以上需要手动通过 `$emit` 触发父组件的事件，更简单的方式可以在父组件引用子组件时通过 `@hook` 来监听即可，如下所示:
```js
//  Parent.vue
<Child @hook:mounted="doSomething" ></Child>

doSomething() {
   console.log('父组件监听到 mounted 钩子函数 ...');
},
    
//  Child.vue
mounted(){
   console.log('子组件触发 mounted 钩子函数 ...');
},    
    
// 以上输出顺序为：
// 子组件触发 mounted 钩子函数 ...
// 父组件监听到 mounted 钩子函数 ...     
```

当然 `@hook` 方法不仅仅是可以监听 `mounted`，其它的生命周期事件，例如：`created`，`updated` 等都可以监听


#### 谈谈你对 `keep-alive` 的了解?
`keep-alive` 是 `Vue` 内置的一个组件，可以使被包含的组件保留状态，避免重新渲染 ，其有以下特性:
- 一般结合路由和动态组件一起使用，用于缓存组件;
- 提供 `include` 和 `exclude` 属性，两者都支持字符串或正则表达式， `include` 表示只有名称匹配的组件会被缓存，`exclude` 表示任何名称匹配的组件都不会被缓存 ，其中 `exclude` 的优先级比 `include` 高;
- 对应两个钩子函数 `activated` 和 `deactivated` ，当组件被激活时，触发钩子函数 `activated`，当组件被移除时，触发钩子函数 `deactivated`;

#### 组件中 `data` 为什么是一个函数?
> 为什么组件中的 data 必须是一个函数，然后 return 一个对象，而 new Vue 实例里，data 可以直接是一个对象?

```js
// data
data() {
  return {
	message: "子组件",
	childName:this.name
  }
}

// new Vue
new Vue({
  el: '#app',
  router,
  template: '<App/>',
  components: {App}
})
```

因为组件是用来复用的，且 JS 里对象是引用关系，如果组件中 data 是一个对象，那么这样作用域没有隔离，子组件中的 data 属性值会相互影响，如果组件中 data 选项是一个函数，那么每个实例可以维护一份被返回对象的独立的拷贝，组件实例之间的 data 属性值不会互相影响；而 new Vue 的实例，是不会被复用的，因此不存在引用对象的问题

#### `v-model` 的原理?
我们在 `vue` 项目中主要使用 `v-model` 指令在表单 `input`、`textarea`、`select` 等元素上创建双向数据绑定，我们知道 `v-model` 本质上不过是语法糖，`v-model` 在内部为不同的输入元素使用不同的属性并抛出不同的事件：

- `text` 和 `textarea` 元素使用 `value` 属性和 `input` 事件；
- `checkbox` 和 `radio` 使用 `checked` 属性和 `change` 事件；
- `select` 字段将 `value` 作为 `prop` 并将 `change` 作为事件

以 `input` 表单元素为例:
```js
<input v-model='something'>
    
相当于

<input v-bind:value="something" v-on:input="something = $event.target.value">
```

如果在自定义组件中，`v-model` 默认会利用名为 `value` 的 `prop` 和名为 `input` 的事件，如下所示:
```js
父组件：
<ModelChild v-model="message"></ModelChild>

子组件：
<div>{{value}}</div>

props:{
    value: String
},
methods: {
  test1(){
     this.$emit('input', '小红')
  },
},
```

#### `Vue` 组件间通信有哪几种方式?
`Vue` 组件间通信只要指以下 3 类通信: 父子组件通信、隔代组件通信、兄弟组件通信

1. `props` / `$emit` 适用于父子组件通信
2. `$parent / $children` 适用 父子组件通信
3. EventBus(`$emit` / `$on`) 适用于 父子、隔代、兄弟组件通信
4. `$attrs` / `$listeners` 适用于 隔代组件通信
5. `provide` / `inject` 适用于 隔代组件通信
6. `Vuex` 适用于 父子、隔代、兄弟组件通信


###### 1.`props` / `$emit` 适用于父子组件通信
用过 `Vue` 技术栈开发项目过的开发者对这样一个组合肯定不会陌生，这种组件通信的方式是我们运用的非常多的一种。`props` 以单向数据流的形式可以很好的完成父子组件的通信

所谓单向数据流：就是数据只能通过 `props` 由父组件流向子组件，而子组件并不能通过修改 `props` 传过来的数据修改父组件的相应状态。至于为什么这样做，`Vue` 官网做出了解释：

> 所有的 `prop` 都使得其父子 `prop` 之间形成了一个单向下行绑定：父级 `prop` 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外改变父级组件的状态，从而导致你的应用的数据流向难以理解

额外的，每次父级组件发生更新时，子组件中所有的 `prop` 都将会刷新为最新的值。这意味着你不应该在一个子组件内部改变 `prop`。如果你这样做了，`Vue` 会在浏览器的控制台中发出警告

正因为这个特性，于是就有了对应的 `$emit`。`$emit` 用来触发当前实例上的事件。对此，我们可以在父组件自定义一个处理接受变化状态的逻辑，然后在子组件中如若相关的状态改变时，就触发父组件的逻辑处理事件

```jsx
// 父组件
Vue.component('parent', {
  template:`
    <div>
      <p>this is parent component!</p>
      <child :message="message" v-on:getChildData="getChildData"></child>
    </div>
  `,
  data() {
    return {
      message: 'hello'
    }
  },
  methods:{
    // 执行子组件触发的事件
    getChildData(val) {
      console.log(val);
    }
  }
});

// 子组件
Vue.component('child', {
  template:`
    <div>
      <input type="text" v-model="myMessage" @input="passData(myMessage)">
    </div>
  `,
  /**
   * 得到父组件传递过来的数据
   * 这里的定义最好是写成数据校验的形式，免得得到的数据是我们意料之外的
   *
   * props: {
   *   message: {
   *     type: String,
   *     default: ''
   *   }
   * }
   *
  */
  props:['message'], 
  data() {
    return {
      // 这里是必要的，因为你不能直接修改 props 的值
      myMessage: this.message
    }
  },
  methods:{
    passData(val) {
      // 数据状态变化时触发父组件中的事件
      this.$emit('getChildData', val);
    }
  }
});
    
var app = new Vue({
  el: '#app',
  template: `
    <div>
      <parent />
    </div>
  `
});

```

###### 2.`$parent / $children` 适用 父子组件通信
这里要说的这种方式就比较直观了，直接操作父子组件的实例。`$parent` 就是父组件的实例对象，而 `$children` 就是当前实例的直接子组件实例了，不过这个属性值是数组类型的，且并不保证顺序，也不是响应式的

```jsx
// 定义 parent 组件
Vue.component('parent', {
  template: `
    <div>
      <p>this is parent component!</p>
      <button @click="changeChildValue">test</button>
      <child />
    </div>
  `,
  data() {
    return {
      message: 'hello'
    }
  },
  methods: {
    changeChildValue(){
      this.$children[0].mymessage = 'hello';
    }
  },
});

// 定义 child 组件
Vue.component('child', {
  template:`
    <div>
      <input type="text" v-model="mymessage" @change="changeValue" /> 
    </div>
  `,
  data() {
    return {
      mymessage: this.$parent.message
    }
  },
  methods: {
    changeValue(){
      this.$parent.message = this.mymessage;//通过如此调用可以改变父组件的值
    }
  },
});
    
const app = new Vue({
  el: '#app',
  template: `
    <div>
      <parent />
    </div>
  `
});
```

###### 3.EventBus(`$emit` / `$on`) 适用于 父子、隔代、兄弟组件通信
`EventBus` 通过新建一个 `Vue` 事件 `bus` 对象，然后通过 `bus.$emit` 触发事件，`bus.$on` 监听触发的事件

```jsx
// 组件 A
Vue.component('A', {
  template: `
    <div>
      <p>this is A component!</p>
      <input type="text" v-model="mymessage" @input="passData(mymessage)"> 
    </div>
  `,
  data() {
    return {
      mymessage: 'hello brother1'
    }
  },
  methods: {
    passData(val) {
      //触发全局事件globalEvent
      this.$EventBus.$emit('globalEvent', val)
    }
  }
});

// 组件 B
Vue.component('B', {
  template:`
    <div>
      <p>this is B component!</p>
      <p>组件A 传递过来的数据：{{brothermessage}}</p>
    </div>
  `,
  data() {
    return {
      mymessage: 'hello brother2',
      brothermessage: ''
    }
  },
  mounted() {
    //绑定全局事件globalEvent
    this.$EventBus.$on('globalEvent', (val) => {
      this.brothermessage = val;
    });
  }
});

//定义中央事件总线
const EventBus = new Vue();

// 将中央事件总线赋值到 Vue.prototype 上，这样所有组件都能访问到了
Vue.prototype.$EventBus = EventBus;

const app = new Vue({
  el: '#app',
  template: `
    <div>
      <A />
      <B />
    </div>
  `
});
```

###### 4.`$attrs` / `$listeners` 适用于 隔代组件通信
如果父组件A下面有子组件B，组件B下面有组件C，这时如果组件A直接想传递数据给组件C那就行不通了！ 只能是组件A通过 `props` 将数据传给组件B，然后组件B获取到组件A 传递过来的数据后再通过 `props` 将数据传给组件C。当然这种方式是非常复杂的，无关组件中的逻辑业务一种增多了，代码维护也没变得困难，再加上如果嵌套的层级越多逻辑也复杂，无关代码越多

`Vue 2.4` 提供了`$attrs` 和 `$listeners` 来实现能够直接让组件A传递消息给组件C

```jsx
// 组件A
Vue.component('A', {
  template: `
    <div>
      <p>this is parent component!</p>
      <B :messagec="messagec" :message="message" v-on:getCData="getCData" v-on:getChildData="getChildData(message)"></B>
    </div>
  `,
  data() {
    return {
      message: 'hello',
      messagec: 'hello c' //传递给c组件的数据
    }
  },
  methods: {
    // 执行B子组件触发的事件
    getChildData(val) {
      console.log(`这是来自B组件的数据：${val}`);
    },
    
    // 执行C子组件触发的事件
    getCData(val) {
      console.log(`这是来自C组件的数据：${val}`);
    }
  }
});

// 组件B
Vue.component('B', {
  template: `
    <div>
      <input type="text" v-model="mymessage" @input="passData(mymessage)"> 
      <!-- C组件中能直接触发 getCData 的原因在于：B组件调用 C组件时，使用 v-on 绑定了 $listeners 属性 -->
      <!-- 通过v-bind 绑定 $attrs 属性，C组件可以直接获取到 A组件中传递下来的 props（除了 B组件中 props声明的） -->
      <C v-bind="$attrs" v-on="$listeners"></C>
    </div>
  `,
  /**
   * 得到父组件传递过来的数据
   * 这里的定义最好是写成数据校验的形式，免得得到的数据是我们意料之外的
   *
   * props: {
   *   message: {
   *     type: String,
   *     default: ''
   *   }
   * }
   *
  */
  props: ['message'],
  data(){
    return {
      mymessage: this.message
    }
  },
  methods: {
    passData(val){
      //触发父组件中的事件
      this.$emit('getChildData', val)
    }
  }
});

// 组件C
Vue.component('C', {
  template: `
    <div>
      <input type="text" v-model="$attrs.messagec" @input="passCData($attrs.messagec)">
    </div>
  `,
  methods: {
    passCData(val) {
      // 触发父组件A中的事件
      this.$emit('getCData',val)
    }
  }
});
    
var app=new Vue({
  el:'#app',
  template: `
    <div>
      <A />
    </div>
  `
});
```

在上面的例子中，我们定义了 `A`，`B`，`C` 三个组件，其中组件`B` 是组件 `A` 的子组件，组件`C` 是组件`B` 的子组件。

1). 在组件 `A` 里面为组件 `B` 和组件 `C` 分别定义了一个属性值（`message`，`messagec`）和监听事件（`getChildData`，`getCData`），并将这些通过 `props` 传递给了组件 `A` 的直接子组件 `B`；
2). 在组件 `B` 中通过 `props` 只获取了与自身直接相关的属性（`message`），并将属性值缓存在了 `data` 中，以便后续的变化监听处理，然后当属性值变化时触发父组件 `A` 定义的数据逻辑处理事件（`getChildData`）。关于组件 `B` 的直接子组件 `C`，传递了属性 `$attrs` 和绑定了事件 `$listeners`；
3). 在组件 `C` 中直接在 v-model 上绑定了 `$attrs` 属性，通过 `v-on` 绑定了 `$listeners`；

最后就将 `$attrs` 和 `$listeners` 单独拿出来说说吧！


`$attrs`：包含了父作用域中不被 `prop` 所识别 (且获取) 的特性绑定 (`class` 和 `style` 除外)。当一个组件没有声明任何 `prop` 时，这里会包含所有父作用域的绑定属性 (`class`和 `style` 除外)，并且可以通过 `v-bind="$attrs"` 传入内部组件。


`$listeners`：包含了父作用域中的 (不含 `.native` 修饰器的) `v-on` 事件监听器。它可以通过 `v-on="$listeners"` 传入内部组件

###### 5.`provide` / `inject` 适用于 隔代组件通信
在父组件中通过 provider 来提供属性，然后在子组件中通过 inject 来注入变量。不论子组件有多深，只要调用了 inject 那么就可以注入在 provider 中提供的数据，而不是局限于只能从当前父组件的 prop 属性来获取数据，只要在父组件的生命周期内，子组件都可以调用

```jsx
// 定义 parent 组件
Vue.component('parent', {
  template: `
    <div>
      <p>this is parent component!</p>
      <child></child>
    </div>
  `,
  provide: {
    for:'test'
  },
  data() {
    return {
      message: 'hello'
    }
  }
});

// 定义 child 组件
Vue.component('child', {
  template: `
    <div>
      <input type="tet" v-model="mymessage"> 
    </div>
  `,
  inject: ['for'],	// 得到父组件传递过来的数据
  data(){
    return {
      mymessage: this.for
    }
  },
});

const app = new Vue({
  el: '#app',
  template: `
    <div>
      <parent />
    </div>
  `
});
```

在上面的实例中，我们定义了组件 `parent` 和组件 `child`，组件 `parent` 和组件 `child` 是父子关系

1. 在 `parent` 组件中，通过 `provide` 属性，以对象的形式向子孙组件暴露了一些属性
2. 在 `child` 组件中，通过 `inject` 属性注入了 `parent` 组件提供的数据，实际这些通过 `inject` 注入的属性是挂载到 `Vue` 实例上的，所以在组件内部可以通过 `this` 来访问

> 注意：官网文档提及 `provide` 和 `inject` 主要为高阶插件/组件库提供用例，并不推荐直接用于应用程序代码中

###### 6.`Vuex` 适用于 父子、隔代、兄弟组件通信
`Vuex` 是一个专为 `Vue.js` 应用程序开发的状态管理模式。每一个 `Vuex` 应用的核心就是 `store`（仓库）。`“store”` 基本上就是一个容器，它包含着你的应用中大部分的状态 ( `state` )


## 参考

- 我是你的超级英雄.[30 道 Vue 面试题，内含详细讲解](https://juejin.im/post/5d59f2a451882549be53b170#heading-4)
