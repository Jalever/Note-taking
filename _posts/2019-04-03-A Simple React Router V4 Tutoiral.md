---
layout: post
title: A Simple React Router V4 Tutorial
subtitle: React-Router学习笔记系列
date: 2019-04-03
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React-Router
---

## Installation
`React Router` has been broken into three packages: 
- `react-router`
That package provides the core routing components and functions for `React Router` applications.
- `react-router-dom`
This provides environment specific `browser` components, but it also re-export all of `react-router`'s exports.
- `react-router-native`
This  provide environment specific `React Native` components, but it also re-export all of `react-router`'s exports.

## Determining which type of router to use
`<BrowserRouter>` should be used when you have a server that will handle dynamic requests (knows how to respond to any possible `URI`)<br>
`<HashRouter>` should be used for static websites (where the server can only respond to requests for files that it knows about)


