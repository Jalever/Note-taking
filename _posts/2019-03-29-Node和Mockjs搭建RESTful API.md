---
layout: post
title: Node和Mockjs搭建RESTful接口
subtitle: Node.js学习笔记系列
date: 2019-03-29
author: Jalever
header-img: img/post_bg_2019_mountain.png
catalog: true
tags:
  - Node.js
  - Server
---

## `server.js` file

```javascript
const express = require("express");
const Mock = require("mockjs");
const app = express();

const port = process.env.PORT || 8081;

app.get("/data", function(req, res) {
	let data = Mock.mock({
		"userInfo|1-100": [{
			'id|1-2000': 10000,
			'name': '@cname',
			'province': '@province()',
			'phone': /^(13|14|15)[0-9]\d{8}$/,
			'birth': '@date()'
		}]
	});
	res.json(data);
});

app.listen(port, () => {
	console.log(`Server are listening http://47.106.132.253:${port}/data`);
});
```



## 浏览器验证 API

#### Chrome 插件
`postman`
#### Firefox 插件
`RESTClient`

## 跨域方法总结
[跨域方法总结](https://jalever.github.io/2019/03/29/%E8%B7%A8%E5%9F%9F%E6%80%BB%E7%BB%93/)
