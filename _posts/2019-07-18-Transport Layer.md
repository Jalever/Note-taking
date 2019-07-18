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

- [Overview](#overview)
- [Services](#services)
    - [Connection-oriented communication](#connectionoriented-communication)
    - [Same order delivery](#same-order-delivery)
    - [Reliability](#reliability)
    - [Flow control](#flow-control)
    - [Congestion avoidance](#congestion-avoidance)
    - [Multiplexing](#multiplexing)

## Overview
In <strong>Computer Networking</strong>, the <strong>Transport Layer</strong> is a conceptual division of methods in the layered architecture of protocols in the network stack in the Internet Protocol Suite and the OSI model. The protocols of this layer provide host-to-host communication services for applications. It provides services such as <ins>connection-oriented communication</ins>, <ins>reliability</ins>, <ins>flow control</ins>, and <ins>multiplexing</ins>.

The details of implementation and semantics of the Transport Layer of the <strong>TCP/IP model</strong>, which is the foundation of the Internet, and the OSI model of general networking are different. The protocols in use today in this layer for the Internet all originated in the development of <strong>TCP/IP</strong>. In the OSI model the Transport Layer is often referred to as <strong>Layer 4</strong>, or <strong>L4</strong>, while numbered layers are not used in <strong>TCP/IP</strong>.
![ZjuXy6.png](https://s2.ax1x.com/2019/07/18/ZjuXy6.png)

The best-known transport protocol of TCP/IP is the <strong>Transmission Control Protocol</strong>(TCP), and lent its name to the title of the entire suite. It is used for <ins>connection-oriented transmissions</ins>, whereas the connectionless <strong>User Datagram Protocol</strong>(UDP) is used for simpler messaging transmissions. <strong>TCP</strong> is the more complex protocol, due to its stateful design <ins>incorporating reliable transmission</ins> and <ins>data stream services</ins>. Together, <strong>TCP</strong> and <strong>UDP</strong> comprise essentially all traffic on the internet and are the only protocols implemented in every major operating system. Additional transport layer protocols that have been defined and implemented include the <strong>Datagram Congestion Control Protocol</strong>(DCCP) and the <strong>Stream Control Transmission Protocol</strong>(SCTP).

## Services
Transport Layer services are conveyed to an application via a programming interface to the transport layer protocols. The services may include the following features:

#### Connection-oriented communication
It is normally easier for an application to interpret a connection as a <strong>Data Stream</strong> rather than having to deal with the underlying connection-less models, such as the <strong>Datagram</strong> model of the <strong>User Datagram Protocol</strong>(UDP) and of the <strong>Internet Protocol</strong>(IP).

#### Same order delivery
The Network Layer doesn't generally guarantee that packets of data will arrive in the same order that they were sent, but often this is a desirable feature. This is usually done through the use of segment numbering, with the receiver passing them to the application in order. This can cause <strong>Head-of-Line Blocking</strong>.

#### Reliability
<strong>Packet</strong>s may be lost during transport due to <strong>Network Congestion</strong> and Errors. By means of an <strong>Error Detection Code</strong>, such as a <strong>Checksum</strong>, the Transport Protocol may check that the data is not corrupted, and verify correct receipt by sending an <strong>ACK</strong> or <strong>NACK</strong> message to the sender. <strong>Automatic Repeat Request</strong> schemes may be used to retransmit lost or corrupted data.

#### Flow control
The rate of data transmission between two nodes must sometimes be managed to prevent a fast sender from transmitting more data than can be supported by the receiving Data Buffer, causing a <strong>Buffer Overrun</strong>. This can also be used to improve efficiency by reducing <strong>Buffer Underrun</strong>.

#### Congestion avoidance
<strong>Congestion Control</strong> can control traffic entry into a telecommunications network, so as to avoid <strong>Congestive Collapse</strong> by attempting to avoid oversubscription of any of the processing or link capabilities of the intermediate nodes and networks and taking resource reducing steps, such as reducing the rate of sending <strong>Packet</strong>s. For example, <strong>Automatic Repeat Requests</strong> may keep the network in a congested state; this situation can be avoided by adding congestion avoidance to the flow control, including <strong>Slow-Start</strong>. This keeps the bandwidth consumption at a low level in the beginning of the transmission, or after packet retransmission.

#### Multiplexing
Ports can provide multiple endpoints on a single node. For example, the name on a postal address is a kind of multiplexing, and distinguishes between different recipients of the same location. Computer applications will each listen for information on their own ports, which enables the use of more than one network service at the same time. It is part of the transport layer in the <strong>TCP/IP</strong> model, but of the <strong>Session Layer</strong> in the OSI model.
