---
layout: post
title: HTTP Module
subtitle: Nodejs Built-in Module
date: 2019-07-03
author: Jalever
header-img: img/post_light_bulb_bg.png
catalog: true
tags:
  - Node.js
---

- [Introduction](#introduction)
    - [Definition](#definition)
    - [Syntax](#syntax)
    - [HTTP Properties and Methods](#http-properties-and-methods)
        - [Node.js http.createServer Method](#nodejs-httpcreateserver-method)
        - [Node.js requestListener Function](#nodejs-requestlistener-function)
        - [Node.js IncomingMessage Object](#nodejs-incomingmessage-object)
        - [Node.js HTTP ServerResponse Object](#nodejs-http-serverresponse-object)
- [Sample Code](#sample-code)
    - [HTTP Header](#http-header)

## Introduction
#### Definition
The HTTP module provides a way of making Node.js transfer data over HTTP (Hyper Text Transfer Protocol).

#### Syntax
The syntax for including the HTTP module in your application:
```js
var http = require('http');
```

#### HTTP Properties and Methods
![ZtfUSI.png](https://s2.ax1x.com/2019/07/03/ZtfUSI.png)

###### Node.js http.createServer Method
The `http.createServer()` method turns your computer into an HTTP server.

The `http.createServer()` method creates an HTTP Server object.

The HTTP Server object can listen to ports on your computer and execute a function, a `requestListener`, each time a request is made.

1.<strong>http.createServer() Syntax</strong>
```js
http.createServer(requestListener);
```

2.<strong>http.createServer() Parameter Values</strong>
<table>
    <thead>
        <tr>
            <td>Parameter</td>
            <td>Description</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>requestListener</td>
            <td>Optional. Specifies a function to be executed every time the server gets a request. This function is called a requestListener, and handles request from the user, as well as response back to the user.</td>
        </tr>
    </tbody>
</table>

###### Node.js requestListener Function

1.<strong>Definition and Usage</strong>
The `requestListener` is a function that is called each time the server gets a request.

The `requestListener` function is passed as a parameter to the `http.createServer()` method.

The `requestListener` function handles requests from the user, and also the response back to the user

2.<strong>Syntax</strong>
```js
function (request, response) {
}
```

3.<strong>Parameter Values</strong>
<table>
    <thead>
        <tr>
            <td>Parameter</td>
            <td>Description</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>request</td>
            <td>The first parameter, the Request object, represents an IncomingMessage object.</td>
        </tr>
        <tr>
            <td>response</td>
            <td>The second parameter represents a ServerResponse object, which has methods for handling the response stream back to the user</td>
        </tr>
    </tbody>
</table>

###### Node.js IncomingMessage Object
1.<strong>IncomingMessage Methods and Properties</strong>

The `IncomingMessage` object represents the request to the server.
![ZthgED.png](https://s2.ax1x.com/2019/07/03/ZthgED.png)

###### Node.js HTTP ServerResponse Object
1.<strong>ServerResponse Methods and Properties</strong>

The `ServerResponse` object is passed as the second parameter to the `requestListener` function.

The `ServerResponse` object represents the writable stream back to the client.
![Zt4nr6.png](https://s2.ax1x.com/2019/07/03/Zt4nr6.png)

## Sample Code
The HTTP module can create an HTTP server that listens to server ports and gives a response back to the client.

Use the `createServer()` method to create an HTTP server:

```js
var http = require('http');

//create a server object:
http.createServer(function (req, res) {
  res.write('Hello World!'); //write a response to the client
  res.end(); //end the response
}).listen(8080); //the server object listens on port 8080
```

The function passed into the http.createServer() method, will be executed when someone tries to access the computer on port 8080.

#### HTTP Header
If the response from the HTTP server is supposed to be displayed as HTML, you should include an HTTP header with the correct content type:

```js
var http = require('http');
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/html'});
  res.write('Hello World!');
  res.end();
}).listen(8080);
```

The first argument of the `res.writeHead()` method is the status code, 200 means that all is OK, the second argument is an object containing the response headers.
