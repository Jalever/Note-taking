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

- [Overview](#overview)
- [Understanding Synchronous and Asynchronous](#understanding-synchronous-and-asynchronous)
    - [Synchronous](#synchronous)
    - [Asynchronous](#asynchronous)
- [AJAX Technologies](#ajax-technologies)
- [Examples](#examples)


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
An asynchronous request doesn’t block the client i.e. browser is responsive. At that time, user can perform another operations also. In such case, javascript engine of the browser is not blocked.

<p align="center"><img src="https://s2.ax1x.com/2019/06/21/ZS9xY9.gif" alt="ZS9xY9.gif" border="0" /></p>

As you can see in the above image, full page is not refreshed at request time and user gets response from the ajax engine.

Let's try to understand asynchronous communication by the image given below.

<p align="center"><img src="https://s2.ax1x.com/2019/06/21/ZSC9Qx.jpg" alt="ZSC9Qx.jpg" border="0" /></p>

> every blocking operation is not synchronous and every unblocking operation is not asynchronous.

## AJAX Technologies
As describe earlier, `AJAX` is not a technology but group of inter-related technologies. `AJAX` technologies includes:
- HTML/XHTML and CSS
- DOM
- XML or JSON
- XMLHttpRequest
- JavaScript

## Understanding XMLHttpRequest
An object of XMLHttpRequest is used for asynchronous communication between client and server.

It performs following operations:
1.Sends data from the client in the background
2.Receives the data from the server
3.Updates the webpage without reloading it.

#### Properties of XMLHttpRequest object
The common properties of XMLHttpRequest object are as follows:

<table>
    <thead>
        <tr>
            <td>Property</td>
            <td>Description</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>onReadyStateChange</td>
            <td>It is called whenever readystate attribute changes. It must not be used with synchronous requests.</td>
        </tr>
        <tr>
            <td>readyState</td>
            <td>
                <p>0&nbsp;UNOPENED&nbsp;open() is not called.</p>
                <p>1&nbsp;OPENED&nbsp;open is called but send() is not called.</p>
                <p>2&nbsp;HEADERS_RECEIVED&nbsp;send() is called, and headers and status are available.</p>
                <p>3&nbsp;LOADING&nbsp;Downloading data; responseText holds the data.</p>
                <p>4&nbsp;DONE&nbsp;The operation is completed fully.</p>
            </td>
        </tr>
        <tr>
            <td>reponseText</td>
            <td>returns response as text</td>
        </tr>
        <tr>
            <td>responseXML</td>
            <td>returns response as XML</td>
        </tr>
    </tbody>
</table>

## Examples
```js
let xhr = new XMLHttpRequest();
xhr.onreadystatechange = function() {
    if(this.readyState === 4 && this.status === 200) {
        console.log(this.responseText);
    }
};
xhr.open("GET", "http://47.106.132.253:3000/hello", true);
xhr.send();
```
