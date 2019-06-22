---
layout: post
title: Complete Guide to Cross Origin Resource Sharing(CORS)
subtitle: Web Development学习笔记系列
date: 2019-03-29
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Web Development
---

- [Introduction](#introduction)
- [Simple CORS Example](#simple-cors-example)
- [CORS and JSONP](#cors-and-jsonp)
- [CORS Enabled](#cors-enabled)
    - [`webpack-dev-server`实现跨域](#webpack-dev-server%E5%AE%9E%E7%8E%B0%E8%B7%A8%E5%9F%9F)
    - [通过`jsonp`跨域](#%E9%80%9A%E8%BF%87jsonp%E8%B7%A8%E5%9F%9F)
    - [通过`document.domain` + `iframe`跨域](#%E9%80%9A%E8%BF%87documentdomain--iframe%E8%B7%A8%E5%9F%9F)
    - [通过`location.hash` + `iframe`跨域](#%E9%80%9A%E8%BF%87locationhash--iframe%E8%B7%A8%E5%9F%9F)
    - [通过`window.name` + `iframe`跨域](#%E9%80%9A%E8%BF%87windowname--iframe%E8%B7%A8%E5%9F%9F)
    - [`postMessage`跨域](#postmessage%E8%B7%A8%E5%9F%9F)
    - [`nginx`代理跨域](#nginx%E4%BB%A3%E7%90%86%E8%B7%A8%E5%9F%9F)
    - [`nodejs`中间件代理跨域](#nodejs%E4%B8%AD%E9%97%B4%E4%BB%B6%E4%BB%A3%E7%90%86%E8%B7%A8%E5%9F%9F)
        - [1.`cors`包](#1cors%E5%8C%85)
        - [2.`res.header`](#2resheader)

## Introduction
`Cross-Origin Resource Sharing (CORS)` is a mechanism that uses additional HTTP headers to tell a browser to let a web application running at one origin (domain) have permission to access selected resources from a server at a different origin.

A web application executes a cross-origin HTTP request when it requests a resource that has a different origin (<strong>domain</strong>, <strong>protocol</strong>, and <strong>port</strong>) than its own origin.

For security reasons, browsers restrict cross-origin `HTTP` requests initiated from within scripts. For example, `XMLHttpRequest` and the `Fetch API` follow the same-origin policy. This means that a web application using those APIs can only request HTTP resources from the same origin the application was loaded from, unless the response from the other origin includes the right `CORS` headers.

[![ZSrkkt.md.png](https://s2.ax1x.com/2019/06/21/ZSrkkt.md.png)](https://imgchr.com/i/ZSrkkt)


## Simple CORS Example

Here is a simple CORS example of when a browser requests a resource from another domain. Let’s say DomainX makes a request to DomainY for a particular resource. CORS uses HTTP headers to determine whether or not DomainX should have access to that resource. The browser automatically sends a request header to DomainY with

```bash
Origin: http://domainx.com
```

DomainY receives that request and will respond back with either:

1.Access-Control-Allow-Origin: http://domainx.com
2.Access-Control-Allow-Origin: * (meaning all domains are allowed)
3.An error if the cross-origin requests are not allowed

## CORS and JSONP
`CORS` can be used as a modern alternative to the `JSONP` pattern. While `JSONP` supports only the `GET` request method, `CORS` also supports other types of `HTTP` requests. Using `CORS` enables a web programmer to use regular `XMLHttpRequest`, which supports better error handling than `JSONP`. On the other hand, `JSONP` works on legacy browsers which predate `CORS` support. `CORS` is supported by most modern web browsers. Also, while `JSONP` can cause `cross-site scripting (XSS)` issues when the external site is compromised, `CORS` allows websites to manually parse responses to increase security

## CORS Enabled

#### `webpack-dev-server`实现跨域

在`index.jsx`中发出 AJAX 请求

```javascript
function LoadDoc() {
  let xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState === 4 && this.status === 200) {
      Clipboard(this.responseText);
    }
  };

  xhttp.open("GET", "api/user", true);
  xhttp.send();
}
```

在`webpack.config.js`中`devServer`实现跨域:

```javascript
devServer: {
		contentBase: "./dist",
		hot: true,
		proxy: {
			"*": {
				target: "http://47.106.132.253:8081",//我的服务器地址:端口
				changeOrigin: true,//是否变域
				secure: false//是否支持https协议
			}
		}
	},
```

#### 通过`jsonp`跨域

#### 通过`document.domain` + `iframe`跨域

#### 通过`location.hash` + `iframe`跨域

#### 通过`window.name` + `iframe`跨域

#### `postMessage`跨域

#### `nginx`代理跨域
```js
server {
  listen        80;
  server_name   api.test.com;


  location / {

    # Simple requests
    if ($request_method ~* "(GET|POST)") {
      add_header "Access-Control-Allow-Origin"  *;
    }

    # Preflighted requests
    if ($request_method = OPTIONS ) {
      add_header "Access-Control-Allow-Origin"  *;
      add_header "Access-Control-Allow-Methods" "GET, POST, OPTIONS, HEAD";
      add_header "Access-Control-Allow-Headers" "Authorization, Origin, X-Requested-With, Content-Type, Accept";
      return 200;
    }

    ....
    # Handle request
    ....
  }
}
```

#### `nodejs`中间件代理跨域

###### 1.`cors`包

- Simple Usage

```javascript
var express = require("express");
var cors = require("cors");
var app = express();

app.use(cors());

app.get("/products/:id", function(req, res, next) {
  res.json({ msg: "This is CORS-enabled for all origins!" });
});

app.listen(80, function() {
  console.log("CORS-enabled web server listening on port 80");
});
```

###### 2.`res.header`

```javascript
app.use(function(req, res, next) {
  res.header("Access-Control-Allow-Origin", "*");
  res.header("Access-Control-Allow-Headers","Origin, X-Requested-With, Content-Type, Accept");
  next();
});
```
