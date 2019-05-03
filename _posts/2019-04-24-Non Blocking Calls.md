---
layout: post
title: Non Blocking Calls
subtitle: React Saga学习笔记系列 7
date: 2019-04-24
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - React Saga
---




`call` is a blocking Effect, i.e. the `Generator` can't perform/handle anything else until the call terminates.<br>

`fork`<br/>
When we fork a task, the task is started in the background and the caller can continue its flow without waiting for the forked task to terminate.