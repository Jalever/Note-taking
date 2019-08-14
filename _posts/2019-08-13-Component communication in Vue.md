---
layout: post
title: Component Communication in Vue
subtitle: Vue Tutorial Takeaway
date: 2019-08-13
author: Jalever
header-img: img/post_2019_web_development_bg.png
catalog: true
tags:
    - Vue
---
- [Overview](#overview)
    - [Parent to child communication](#parent-to-child-communication)
    - [Child to parent communication](#child-to-parent-communication)
    - [Communication between any component](#communication-between-any-component)

## Overview
In modern front-end frameworks, the entire page is divided into small pieces of components. Each component has its own functionality & UI. Component-based architecture makes it easy to develop & maintain an application. During development, you may come across a situation where you need to share data between with other components. In this post, we are going to learn about many possible ways of achieving communication between components.

Vue.js allows component communication in the following ways:
1. Parent to child communication (Using Props).
2. Child to parent communication (Using Events).
3. Communication between any component (Using Event Bus).

#### Parent to child communication
![m9v6oT.png](https://s2.ax1x.com/2019/08/13/m9v6oT.png)
In this type of communication, a parent passes the data to child by adding an argument in the component declaration.
![m9xWAf.png](https://s2.ax1x.com/2019/08/13/m9xWAf.png)
![m9xxCF.png](https://s2.ax1x.com/2019/08/13/m9xxCF.png)

#### Child to parent communication
![mCpp01.png](https://s2.ax1x.com/2019/08/13/mCpp01.png)
In this type of communication, Events ensures communication from child to parent.

![mCSXpF.png](https://s2.ax1x.com/2019/08/13/mCSXpF.png)
![mCSjl4.png](https://s2.ax1x.com/2019/08/13/mCSjl4.png)

#### Communication between any component
Event Bus is not limited to a parent-child relation. You can share information between any components.
![mC9wqA.png](https://s2.ax1x.com/2019/08/13/mC9wqA.png)
![mC9fqs.png](https://s2.ax1x.com/2019/08/13/mC9fqs.png)
