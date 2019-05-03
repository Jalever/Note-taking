---
layout: post
title: Pulling future actions
subtitle: React Saga学习笔记系列 6
date: 2019-04-24
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - React Saga
---

`take` creates another command object that tells the middleware to wait for a specific action.

`call` Effect is the same as when the middleware suspends the Generator until a `Promise` resolves.

In the `take` case, it'll suspend the `Generator` until a matching action is dispatched.