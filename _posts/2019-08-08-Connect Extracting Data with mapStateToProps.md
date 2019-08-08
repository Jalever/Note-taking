---
layout: post
title: (React Redux)mapStateToProps
subtitle: Connect_Extracting Data with mapStateToProps
date: 2019-08-08
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---

As the first argument passed in to <strong>connect</strong>, <strong>mapStateToProps</strong> is used for selecting the part of the data from the store that the connected component needs. It’s frequently referred to as just <strong>mapState</strong> for short.

- It is called every time the store state changes.
- It receives the entire store state, and should return an object of data this component needs.
