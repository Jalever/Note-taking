---
layout: post
title: 优化概览Introduction to Optimization
subtitle: 项目优化总结
date: 2020-07-22
author: Jalever
header-img: img/vue_bg.jpeg
catalog: true
tags:
  - Optimization
---

- [通用General](#通用general)
    - [vFor和vIf不要一起使用](#vfor和vif不要一起使用)
    - [vFor key避免使用index作为标识](#vfor-key避免使用index作为标识)
    - [释放组件资源](#释放组件资源)
    - [长列表](#长列表)
    - [图片合理的优化方式](#图片合理的优化方式)
    - [路由器按需加载](#路由器按需加载)
    - [UI框架使用方式](#ui框架使用方式)
    - [首屏优化](#首屏优化)
- [Webpack](#webpack)
    - [最小化JS文件](#最小化js文件)
    - [依赖库CDN加速](#依赖库cdn加速)
    - [GZIP](#gzip)


## 通用General
#### vFor和vIf不要一起使用

#### vFor key避免使用index作为标识

#### 释放组件资源
什么是资源? 每创建出一个事物都需要消耗资源，资源不是凭空产生的，是分配出来的。所以说，当组件销毁后，尽量把我们开辟出来的资源块给销毁掉，比如 setInterval , addEventListener等，如果你不去手动给释放掉，那么它们依旧会占用一部分资源。这就导致了没有必要的资源浪费。多来几次后，可以想象下资源占用率肯定是上升的

添加的事件
```js
created() {
  addEventListener('click', Function, false)
},
beforeDestroy() {
  removeEventListener('click', Function false)
}
```

定时器
```js
created() {
  this.currentInterVal = setInterval(code,millisec,lang)
},
beforeDestroy() {
  clearInterval(this.currentInterVal)
}
```
#### 长列表
项目当中，会涉及到非常多的长列表场景，区别于普通的分页来说，大部分的前端在做这种 无限列表 的时候，大部分新手前端都是通过一个 vFor 将数据遍历出来，想的多一点的就是做一个分页。滚动到底部的时候就继续请求 API 。其实这也是未思考妥当的。随着数据的加载，DOM会越来越多，这样就导致了性能开销的问题产生了，当页面上的DOM太多的时候，难免给我的客户端造成一定的压力，所以对于长列表渲染的时候，建议将DOM移除掉，类似于图片懒加载的模式，只有出现在视图上的DOM才是重要的DOM。网络上有一些很好的解决方案，如 `vue-virtual-scroller` 库等等，大家可以理性的选择

#### 图片合理的优化方式
图片应该都不陌生吧，在网页中，往往存在大量的图片资源，这些资源或大或小。当我们页面中DOM中存在大量的图片时，难免不会碰到一些加载缓慢的问题，导致图片出现加载失败的问题。网络上大部分都在使用 懒加载 的使用方式，只有当 存在图片的DOM 出现在页面上才会进行图片的加载，无形中起到了分流的作用，下面就说一套实践的方案吧

- 小图标使用 `SVG` 或者字体图标
- 通过 `base64` 和 `webp`  的方式加载小型图片
- 能通过`cdn`加速的大图尽量用cdn
- 大部分框架都带有懒加载的图片，不要嫌麻烦，多花点时间使用它

#### 路由器按需加载
对于路由的懒加载，如果还不会的话，那么就真该好好的重新去学习一下了。路由懒加载的方式有两种，一种是require 另一种是 import 。当路由按需加载后，那么Vue服务在第一次加载时的压力就能够相应的小一些，不会出现 超长白屏P0问题 。下面是两种路由懒加载的写法：

```js
// require法
component: resolve=>(require(['@/components/HelloWorld'],resolve))

// import
component: () => import('@/components/HelloWorld')
```

#### UI框架使用方式
确保在使用UI框架如， `Element` ， `And Design` 等UI框架的时候，都使用官方给暴露出来的按需加载组件。只有真正用到它的时候时候才会加载当前UI框架的组件，而不是一开始就将整个组件库给加载出来，我们都知道，一个UI框架其实很大，相对比其他的东西来说。因此，它在方便我们开发者的同时，也无形中产生了多余的开销。但是项目周期开发的时候，不得不依赖它。所以建议尽量的使用按需加载。合理的对项目进行止损，如果你不在意，非常嫌麻烦，那么可以进行全局引入
```js
import { Button } from 'xxxx
```

#### 首屏优化
众所周知，第一次打开Vue的时候，如果你的项目够大，那么首次加载资源时，会非常的久。由于资源没有加载完毕，界面的DOM也不会渲染，会造成白屏的问题。用户此时并不知道是加载的问题，所以会带来一个不好的体验。因此通常会在public下写一个加载动画，告诉用户，网页在加载中这个提示。当页面加载成功后，页面渲染出来的这一个体验比白屏等开机要好太多了。因此，推荐大家都设计一个自家公司的loading加载方式放入`index.html`中吧

## Webpack
#### 最小化JS文件
可以通过webpack处理打包的JavaScript文件，让其更加的精简。在配置中，你可以这么做
```js
config.optimization.minimize(true);
```

#### 依赖库CDN加速
使用CDN的方式引入一些依赖包，觉得非常的 Nice ，然后我也开始使用了。我将 `Vue` `Axios` `Echarts` 等等都分离了出来，在正式环境下，通过CDN，确实有了一些明显的提升，所以说大家可以进行尝试
```js
// 在html引入script标签后。在vue的配置中，进行声明

configureWebpack: {
  externals: {
    'echarts': 'echarts' // 配置使用CDN
  }
}
```

#### GZIP
这个东西需要后端进行配置，当然，如果你有操作 Nginx 的权限的话，那么可以自己开启，反正我认为，这个东西提升还是很大的。具体的可以看这篇文章。这里不过多赘述这个东西




