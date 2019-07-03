---
layout: post
title: Nodejs Getting Started
subtitle: Nodejs Tutorial
date: 2019-07-03
author: Jalever
header-img: img/post_light_bulb_bg.png
catalog: true
tags:
  - Node.js
---

- [Introduction](#introduction)
    - [Features](#features)
    - [Function](#Function)
    - [Nodejs File](#nodejs-file)
- [Sample Code](#sample-code)
- [Modules](#modules)
    - [Built-in Modules](#built-in-modules)
    - [Customized Modules](#customized-modules)


## Introduction
1. Node.js is an open source server environment
2. Node.js is free
3. Node.js runs on various platforms (Windows, Linux, Unix, Mac OS X, etc.)
4. Node.js uses JavaScript on the server

#### Features
A common task for a web server can be to open a file on the server and return the content to the client.

Here is how PHP or ASP handles a file request:

1. Sends the task to the computer's file system.
2. Waits while the file system opens and reads the file.
3. Returns the content to the client.
4. Ready to handle the next request.

Here is how Node.js handles a file request:

1. Sends the task to the computer's file system.
2. Ready to handle the next request.
3. When the file system has opened and read the file, the server returns the content to the client.
4. Node.js eliminates the waiting, and simply continues with the next request.

Node.js runs `single-threaded`, `non-blocking`, `asynchronously programming`, which is very memory efficient.

#### Function
1. Node.js can generate dynamic page content
2. Node.js can create, open, read, write, delete, and close files on the server
3. Node.js can collect form data
4. Node.js can add, delete, modify data in your database

#### Nodejs File
1. Node.js files contain tasks that will be executed on certain events
2. A typical event is someone trying to access a port on the server
3. Node.js files must be initiated on the server before having any effect
4. Node.js files have extension ".js"

## Sample Code
```js
var express = require("express");
var app = express();
const server = require("http").createServer(app);
const port = process.env.PORT || 3000;

server.listen(port, () => {
	console.log("The server is listening on http://47.106.132.253:%d", port);
});

app.get("/hello", (req, res) => {
	res.send("Hello World!");
});
```

## Modules
Consider modules to be the same as JavaScript libraries.

A set of functions you want to include in your application.

#### Built-in Modules
Node.js has a set of built-in modules which you can use without any further installation.

![ZtRYHe.png](https://s2.ax1x.com/2019/07/03/ZtRYHe.png)
![ZtRUNd.png](https://s2.ax1x.com/2019/07/03/ZtRUNd.png)

To include a module, use the `require()` function with the name of the module:

```js
var http = require('http');
```

Now your application has access to the HTTP module, and is able to create a server:

```js
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/html'});
  res.end('Hello World!');
}).listen(8080);
```

#### Customized Modules
You can create your own modules, and easily include them in your applications.

The following example creates a module that returns a date and time object:
```js
exports.myDateTime = function () {
  return Date();
};
```

Use the exports keyword to make properties and methods available outside the module file.

Save the code above in a file called "myfirstmodule.js"

Now you can include and use the module in any of your Node.js files.Use the module "myfirstmodule" in a Node.js file:

```js
var http = require('http');
var dt = require('./myfirstmodule');

http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/html'});
  res.write("The date and time are currently: " + dt.myDateTime());
  res.end();
}).listen(8080);
```
