---
layout: post
title: WebSocket的用法
subtitle: WebSocket用法
date: 2020-04-01
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - JavaScript
---
The WebSocket protocol, described in the specification RFC 6455 provides a way to exchange data between browser and server via a persistent connection. The data can be passed in both directions as “packets”, without breaking the connection and additional HTTP-requests.

WebSocket is especially great for services that require continuous data exchange, e.g. online games, real-time trading systems and so on.

WebSocket is a modern way to have persistent browser-server connections.

- WebSockets don’t have cross-origin limitations.
- They are well-supported in browsers.
- Can send/receive strings and binary data.

The API is simple.

Methods:
- socket.send(data),
- socket.close([code], [reason]).
  
Events:
- open,
- message,
- error,
- close.

Once the socket is created, we should listen to events on it. There are totally 4 events:

- open – connection established,
- message – data received,
- error – websocket error,
- close – connection closed.


## Connection state
To get connection state, additionally there’s socket.readyState property with values:

0 – “CONNECTING”: the connection has not yet been established,
1 – “OPEN”: communicating,
2 – “CLOSING”: the connection is closing,
3 – “CLOSED”: the connection is closed.

