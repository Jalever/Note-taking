---
layout: post
title: Declarative Effects
subtitle: React Saga学习笔记系列 4
date: 2019-04-24
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - React Saga
---

In `redux-saga`, `Sagas` are implemented using `Generator` functions.<br>

To express the `Saga` logic, we yield plain `JavaScript Objects` from the `Generator`.<br>

We call those `Objects Effects`.<br>

An `Effect` is an object that contains some information to be interpreted by the middleware.<br>

You can view `Effects` like instructions to the middleware to perform some operation (e.g., invoke some asynchronous function, dispatch an action to the store, etc.).
