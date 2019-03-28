---
layout: post
title: 2019 March Web前端高频面试题
subtitle: Web前端面试题系列
date: 2019-03-28
author: Jalever
header-img: img/post_bg_fancyCrave.jpg
catalog: true
tags:
  - Interview Questions
---

- [说说浏览器和 Node 事件循环的区别](#%E8%AF%B4%E8%AF%B4%E6%B5%8F%E8%A7%88%E5%99%A8%E5%92%8C-node-%E4%BA%8B%E4%BB%B6%E5%BE%AA%E7%8E%AF%E7%9A%84%E5%8C%BA%E5%88%AB)
- [介绍模块化发展历程](#%E4%BB%8B%E7%BB%8D%E6%A8%A1%E5%9D%97%E5%8C%96%E5%8F%91%E5%B1%95%E5%8E%86%E7%A8%8B)
    - [IIFE](#iife)
    - [AMD](#amd)
    - [CMD](#cmd)
    - [CommonJS](#commonjs)
    - [UMD](#umd)
    - [ES Modules](#es-modules)
- [全局作用域中，用 const 和 let 声明的变量不在 window 上，那到底在哪里？如何去获取？](#%E5%85%A8%E5%B1%80%E4%BD%9C%E7%94%A8%E5%9F%9F%E4%B8%AD%E7%94%A8-const-%E5%92%8C-let-%E5%A3%B0%E6%98%8E%E7%9A%84%E5%8F%98%E9%87%8F%E4%B8%8D%E5%9C%A8-window-%E4%B8%8A%E9%82%A3%E5%88%B0%E5%BA%95%E5%9C%A8%E5%93%AA%E9%87%8C%E5%A6%82%E4%BD%95%E5%8E%BB%E8%8E%B7%E5%8F%96)
- [cookie 和 token 都存放在 header 中，为什么不会劫持 token？](#cookie-%E5%92%8C-token-%E9%83%BD%E5%AD%98%E6%94%BE%E5%9C%A8-header-%E4%B8%AD%E4%B8%BA%E4%BB%80%E4%B9%88%E4%B8%8D%E4%BC%9A%E5%8A%AB%E6%8C%81-token)
- [聊聊 Vue 的双向数据绑定，Model 如何改变 View，View 又是如何改变 Model 的](#%E8%81%8A%E8%81%8A-vue-%E7%9A%84%E5%8F%8C%E5%90%91%E6%95%B0%E6%8D%AE%E7%BB%91%E5%AE%9Amodel-%E5%A6%82%E4%BD%95%E6%94%B9%E5%8F%98-viewview-%E5%8F%88%E6%98%AF%E5%A6%82%E4%BD%95%E6%94%B9%E5%8F%98-model-%E7%9A%84)
- [两个数组合并成一个数组](#%E4%B8%A4%E4%B8%AA%E6%95%B0%E7%BB%84%E5%90%88%E5%B9%B6%E6%88%90%E4%B8%80%E4%B8%AA%E6%95%B0%E7%BB%84)
- [改造下面的代码，使之输出0 - 9，写出你能想到的所有解法](#%E6%94%B9%E9%80%A0%E4%B8%8B%E9%9D%A2%E7%9A%84%E4%BB%A3%E7%A0%81%E4%BD%BF%E4%B9%8B%E8%BE%93%E5%87%BA0---9%E5%86%99%E5%87%BA%E4%BD%A0%E8%83%BD%E6%83%B3%E5%88%B0%E7%9A%84%E6%89%80%E6%9C%89%E8%A7%A3%E6%B3%95)
- [Virtual DOM 真的比操作原生 DOM 快吗？谈谈你的想法](#virtual-dom-%E7%9C%9F%E7%9A%84%E6%AF%94%E6%93%8D%E4%BD%9C%E5%8E%9F%E7%94%9F-dom-%E5%BF%AB%E5%90%97%E8%B0%88%E8%B0%88%E4%BD%A0%E7%9A%84%E6%83%B3%E6%B3%95)
- [下面的代码打印什么内容，为什么？](#%E4%B8%8B%E9%9D%A2%E7%9A%84%E4%BB%A3%E7%A0%81%E6%89%93%E5%8D%B0%E4%BB%80%E4%B9%88%E5%86%85%E5%AE%B9%E4%B8%BA%E4%BB%80%E4%B9%88)
- [简单改造下面的代码，使之分别打印 10 和 20](#%E7%AE%80%E5%8D%95%E6%94%B9%E9%80%A0%E4%B8%8B%E9%9D%A2%E7%9A%84%E4%BB%A3%E7%A0%81%E4%BD%BF%E4%B9%8B%E5%88%86%E5%88%AB%E6%89%93%E5%8D%B0-10-%E5%92%8C-20)
- [浏览器缓存读取规则](#%E6%B5%8F%E8%A7%88%E5%99%A8%E7%BC%93%E5%AD%98%E8%AF%BB%E5%8F%96%E8%A7%84%E5%88%99)
- [使用迭代的方式实现 `flatten` 函数](#%E4%BD%BF%E7%94%A8%E8%BF%AD%E4%BB%A3%E7%9A%84%E6%96%B9%E5%BC%8F%E5%AE%9E%E7%8E%B0-flatten-%E5%87%BD%E6%95%B0)
- [为什么 `Vuex` 的 `mutation` 和 `Redux` 的 `reducer` 中不能做异步操作？](#%E4%B8%BA%E4%BB%80%E4%B9%88-vuex-%E7%9A%84-mutation-%E5%92%8C-redux-%E7%9A%84-reducer-%E4%B8%AD%E4%B8%8D%E8%83%BD%E5%81%9A%E5%BC%82%E6%AD%A5%E6%93%8D%E4%BD%9C)
- [下面代码中 a 在什么情况下会打印 1？](#%E4%B8%8B%E9%9D%A2%E4%BB%A3%E7%A0%81%E4%B8%AD-a-%E5%9C%A8%E4%BB%80%E4%B9%88%E6%83%85%E5%86%B5%E4%B8%8B%E4%BC%9A%E6%89%93%E5%8D%B0-1)
- [介绍下 BFC 及其应用](#%E4%BB%8B%E7%BB%8D%E4%B8%8B-bfc-%E5%8F%8A%E5%85%B6%E5%BA%94%E7%94%A8)

## 说说浏览器和 Node 事件循环的区别
## 介绍模块化发展历程
模块化主要是用来***抽离公共代码***，***隔离作用域***，***避免变量冲突***等
#### IIFE
使用自执行函数来编写模块化<br>
特点：在一个单独的函数作用域中执行代码，避免变量冲突
```javascript
(function(){
  return {
	data:[]
  }
})()
```
#### AMD
使用`requireJS`来编写模块化<br>
特点：依赖必须提前声明好
```javascript
define('./index.js',function(code){
	// code 就是index.js 返回的内容
})
```
#### CMD
使用`seaJS`来编写模块化<br>
特点：支持动态引入依赖文件
```javascript
define(function(require, exports, module) {  
  var indexCode = require('./index.js');
});
```
#### CommonJS
nodejs 中自带的模块化<br>
```javascript
var fs = require('fs');
```
#### UMD
兼容`AMD`，`CommonJS` 模块化语法<br>

#### ES Modules
`ES6`引入的模块化，支持`import`来引入另一个`JavaScript`<br>
```javascript
import a from 'a';
```
## 全局作用域中，用 const 和 let 声明的变量不在 window 上，那到底在哪里？如何去获取？
## cookie 和 token 都存放在 header 中，为什么不会劫持 token？
## 聊聊 Vue 的双向数据绑定，Model 如何改变 View，View 又是如何改变 Model 的
## 两个数组合并成一个数组
请把两个数组 ['A1', 'A2', 'B1', 'B2', 'C1', 'C2', 'D1', 'D2'] 和 ['A', 'B', 'C', 'D']，合并为 ['A1', 'A2', 'A', 'B1', 'B2', 'B', 'C1', 'C2', 'C', 'D1', 'D2', 'D']
## 改造下面的代码，使之输出0 - 9，写出你能想到的所有解法
```javascript
for (var i = 0; i< 10; i++){
	setTimeout(() => {
		console.log(i);
    }, 1000)
}

```
## Virtual DOM 真的比操作原生 DOM 快吗？谈谈你的想法
## 下面的代码打印什么内容，为什么？
```javascript
var b = 10;
(function b(){
    b = 20;
    console.log(b); 
})();
```
## 简单改造下面的代码，使之分别打印 10 和 20
```javascript
var b = 10;
(function b(){
    b = 20;
    console.log(b); 
})();
```
## 浏览器缓存读取规则
可以分成 `Service Worker`、`Memory Cache`、`Disk Cache` 和 `Push Cache`，那请求的时候 `from memory cache` 和 `from disk cache` 的依据是什么，哪些数据什么时候存放在 `Memory Cache` 和 `Disk Cache`中？

## 使用迭代的方式实现 `flatten` 函数
## 为什么 `Vuex` 的 `mutation` 和 `Redux` 的 `reducer` 中不能做异步操作？
## 下面代码中 a 在什么情况下会打印 1？
```javascript
var a = ?;
if(a == 1 && a == 2 && a == 3){
 	console.log(1);
}
```
## 介绍下 BFC 及其应用
