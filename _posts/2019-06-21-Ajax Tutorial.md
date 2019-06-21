---
layout: post
title: AJAX Tutorial
subtitle: AJAX学习笔记系列
date: 2019-06-21
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - AJAX
---

## Overview
`AJAX` is an acronym for Asynchronous JavaScript and XML. It is a group of inter-related technologies like `JavaScript`, `DOM`, `XML`, `HTML/XHTML`, `CSS`, `XMLHttpRequest` etc.

`AJAX` allows you to send and receive data asynchronously without reloading the web page. So it is fast.

`AJAX` allows you to send only important information to the server not the entire page. So only valuable data from the client side is routed to the server side. It makes your application interactive and faster.

## Understanding Synchronous and Asynchronous

#### Synchronous
A synchronous request blocks the client until operation completes i.e. browser is unresponsive. In such case, javascript engine of the browser is blocked.

<p align="center"><img src="https://s2.ax1x.com/2019/06/21/ZS9wIH.gif" alt="ZS9wIH.gif" border="0" /></p>

As you can see in the above image, full page is refreshed at request time and user is blocked until request completes.

Let's understand it another way.

<p align="center"><img src="https://s2.ax1x.com/2019/06/21/ZS9Wdg.jpg" alt="ZS9Wdg.jpg" border="0" /></p>


#### Asynchronous
