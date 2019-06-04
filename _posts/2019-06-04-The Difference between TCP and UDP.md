---
layout: post
title: The Difference between TCP and UDP
subtitle: Computer Network学习笔记系列
date: 2019-06-04
author: Jalever
header-img: img/post-bg-algorithm.jpg
catalog: true
tags:
  - Computer Network
---

## TCP
TCP (Transmission Control Protocol) is connection oriented<br/>
TCP tracks all data sent, requiring acknowledgment for each octet (generally)<br/>
TCP is considered a reliable data transfer protocol. It ensures that no data is sent to the upper layer application that is out of order, duplicated, or has missing pieces.


## UDP
UDP (User Datagram Protocol) is connection-less<br/>
UDP does not use acknowledgments at all, and is usually used for protocols where a few lost datagrams do not matter.<br/>
UDP is used when speed is desirable and error correction is not necessary. For example, UDP is frequently used for live broadcasts and online games.

## Difference
| TCP                 | UDP            |
| ------------------- | -------------- |
| Reliable            | Unreliable     |
| Connection-oriented | Connectionless |
