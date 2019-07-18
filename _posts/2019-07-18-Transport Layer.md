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
    - [Connection-oriented communication](#connection-oriented-communication)
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

## Analysis
The <strong>Transport Layer</strong> is responsible for delivering data to the appropriate application process on the host computers. This involves <strong>Statistical Multiplexing</strong> of data from different application processes, i.e. forming data segments, and adding source and destination port numbers in the header of each transport layer data segment. Together with the source and destination IP address, the port numbers constitutes a <strong>Network Socket</strong>, i.e. an identification address of the <strong>Process-to-Process Communication</strong>. In the OSI model, this function is supported by the <strong>Session Layer</strong>.

Some <strong>Transport Layer Protocols</strong>, for example <strong>TCP</strong>, but not UDP, support <strong>Virtual Circuits</strong>, i.e. provide Connection-Oriented Communication over an underlying packet oriented Datagram network. A byte-stream is delivered while hiding the packet mode communication for the application processes. This involves connection establishment, dividing of the data stream into packets called Segments, Segment Numbering and Reordering of Out-of Order Data.

Finally, some Transport Layer Protocols, for example TCP, but not UDP, provide End-to-End Reliable communication, i.e. <strong>Error Recovery</strong> by means of <strong>Error Detecting Code</strong> and <strong>Automatic Repeat Request</strong>(ARQ) protocol. The <strong>ARQ</strong> protocol also provides <strong>Flow Control</strong>, which may be combined with <strong>Congestion Avoidance</strong>.

<strong>UDP</strong> is a very simple protocol, and does not provide Virtual Circuits, nor reliable communication, delegating these functions to the application program. UDP packets are called <strong>Datagram</strong>s, rather than segments.

<strong>TCP</strong> is used for many protocols, including HTTP web browsing and email transfer. UDP may be used for <ins>Multicasting</ins> and <ins>Broadcasting</ins>, since retransmissions are not possible to a large amount of hosts. UDP typically gives <ins>higher throughput</ins> and <ins>shorter latency</ins>, and is therefore often used for <ins>real-time multimedia communication</ins> where packet loss occasionally can be accepted, for example <ins>IP-TV</ins> and <ins>IP-telephony</ins>, and for <ins>online computer games</ins>.

Many non-IP-based networks, such as <ins>X.25</ins>, <ins>Frame Relay</ins> and <ins>ATM</ins>, implement the <strong>Connection-Oriented Communication</strong> at the network or <strong>Data Link Layer</strong> rather than the <strong>Transport Layer</strong>. In <ins>X.25</ins>, in telephone network modems and in wireless communication systems, reliable Node-to-Node Communication is implemented at lower protocol layers.

The OSI connection-mode transport layer protocol specification defines five classes of transport protocols: <strong>TP0</strong>, providing the least Error Recovery, to <strong>TP4</strong>, which is designed for less Reliable Networks.
