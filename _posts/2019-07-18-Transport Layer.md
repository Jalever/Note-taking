---
layout: post
title: Introduction to Transport Layer
subtitle: Transport Layer
date: 2019-07-18
author: Jalever
header-img: img/network_bg_simple.png
catalog: true
tags:
  - Computer Network
---
## Overview
In <strong>Computer Networking</strong>, the <strong>Transport Layer</strong> is a conceptual division of methods in the layered architecture of protocols in the network stack in the Internet Protocol Suite and the OSI model. The protocols of this layer provide host-to-host communication services for applications. It provides services such as <ins>connection-oriented communication</ins>, <ins>reliability</ins>, <ins>flow control</ins>, and <ins>multiplexing</ins>.

The details of implementation and semantics of the Transport Layer of the <strong>TCP/IP model</strong>, which is the foundation of the Internet, and the OSI model of general networking are different. The protocols in use today in this layer for the Internet all originated in the development of <strong>TCP/IP</strong>. In the OSI model the Transport Layer is often referred to as <strong>Layer 4</strong>, or <strong>L4</strong>, while numbered layers are not used in <strong>TCP/IP</strong>.

The best-known transport protocol of TCP/IP is the <strong>Transmission Control Protocol</strong>(TCP), and lent its name to the title of the entire suite. It is used for <ins>connection-oriented transmissions</ins>, whereas the connectionless <strong>User Datagram Protocol</strong>(UDP) is used for simpler messaging transmissions. <strong>TCP</strong> is the more complex protocol, due to its stateful design incorporating reliable transmission and data stream services. Together, <strong>TCP</strong> and <strong>UDP</strong> comprise essentially all traffic on the internet and are the only protocols implemented in every major operating system. Additional transport layer protocols that have been defined and implemented include the <strong>Datagram Congestion Control Protocol</strong>(DCCP) and the <strong>Stream Control Transmission Protocol</strong>(SCTP).
