---
layout:     post
title:      React Fiber初步了解
subtitle:   React学习笔记系列
date:       2019-03-26
author:     Jalever
header-img: img/post_2019_react_reactFiber_bg.jpeg
catalog: true
tags:
    - React
---


- [为什么要用React Fiber？](#%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E7%94%A8react-fiber)
- [React Fiber的运行方式](#react-fiber%E7%9A%84%E8%BF%90%E8%A1%8C%E6%96%B9%E5%BC%8F)
- [React Fiber的对现行代码的影响](#react-fiber%E7%9A%84%E5%AF%B9%E7%8E%B0%E8%A1%8C%E4%BB%A3%E7%A0%81%E7%9A%84%E5%BD%B1%E5%93%8D)

## 为什么要用React Fiber？
当React决定要加载或更新组件树时，会做很多事情，比如调用各个组件的生命周期函数，计算和比对`Virtual DOM`，最后更新DOM树，这整个过程是同步进行的，也就是说只要加载一个或者更新过程开始，那`React`就会运行知道完成为止<br>
当组件树庞大时，会十分耗时<br>
现有的React版本，当组件树很大的时候就会出现这种问题，因为更新过程是同步地一层组件套一层组件，逐渐深入的过程，在更新完所有组件之前不停止，函数的调用栈就像下图这样，调用得很深，而且很长时间不会返回<br>
![component_tree](https://github.com/Jalever/jalever.github.io/blob/master/img/post_2019_react_reactFiber_component_tree.png)
因为`JavaScript`单线程的特点，每个同步任务不能耗时太长，不然就会让程序不会对其他输入作出响应，而React Fiber就是要改变这个现状<br>

## React Fiber的运行方式
`React Fiber`解决`JavaScript`同步操作时间过长的方法-***分片***<br>
把一个耗时长的任务分成很多小片，每一个小片的运行时间很短，虽然总时间依然很长，但是在每个小片执行完之后，都给其他任务一个执行的机会，这样唯一的线程就不会被独占，其他任务依然有运行的机会<br>
`React Fiber`把更新过程碎片化，执行过程如下面的图所示，每执行完一段更新过程，就把控制权交还给React负责任务协调的模块，看看有没有其他紧急任务要做，如果没有就继续去更新，如果有紧急任务，那就去做紧急任务<br>
维护每一个分片的数据结构，就是`Fiber`<br>
有了分片之后，更新过程的调用栈如下图所示，中间每一个波谷代表深入某个分片的执行过程，每个波峰就是一个分片执行结束交还控制权的时机<br>
![fiber_call_stack](https://github.com/Jalever/jalever.github.io/blob/master/img/post_2019_react_reactFiber_fiber_call_stack.png)


## React Fiber的对现行代码的影响
在`React Fiber`中，一次更新过程会分成多个分片完成，所以完全有可能一个更新任务还没有完成，就被另一个更高优先级的更新过程打断，这时候，优先级高的更新任务会优先处理完，而低优先级更新任务所做的工作则会`完全作废，然后等待机会重头再来`<br>
比如说，一个低优先级的任务A正在执行，已经调用了某个组件的componentWillUpdate函数，接下来发现自己的时间分片已经用完了，于是冒出水面，看看有没有紧急任务，哎呀，真的有一个紧急任务B，接下来React Fiber就会去执行这个紧急任务B，任务A虽然进行了一半，但是没办法，只能完全放弃，等到任务B全搞定之后，任务A重头来一遍，注意，是重头来一遍，不是从刚才中段的部分开始，也就是说，componentWillUpdate函数会被再调用一次

`React Fiber`一个更新过程被分为两个阶段(Phase)
- 第一个阶段***Reconciliation Phase***
    - `React Fiber`会找出需要更新哪些DOM，这个阶段是可以被打断的
    - 可能会调用的生命周期函数
      - componentWillMount
      - componentWillReceiveProps
      - shouldComponentUpdate
      - componentWillUpdate
- 第二阶段***Commit Phase***
    - `React Fiber`会把DOM更新完，不会被打断
    - 可能会调用的生命周期函数
      - componentDidMount
      - componentDidUpdate
      - componentWillUnmount








