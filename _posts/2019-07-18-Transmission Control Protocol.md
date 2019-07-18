---
layout: post
title: (Transport Layer)Transmission Control Protocol
subtitle: Computer Network
date: 2019-07-18
author: Jalever
header-img: img/network_bg_simple.png
catalog: true
tags:
  - Computer Network
---

## Overview
The <strong>Transmission Control Protocol</strong>(TCP) is one of the main protocols of the <strong>Internet Protocol Suite</strong>. It originated in the initial network implementation in which it complemented the <strong>Internet Protocol</strong>(IP). Therefore, the entire suite is commonly referred to as <strong>TCP/IP</strong>. <strong>TCP</strong> provides <ins>reliable</ins>, <ins>ordered</ins>, and <ins>error-checked delivery</ins> of a stream of octets(bytes) between applications running on hosts communicating via an IP network. Major internet applications such as the <strong>World Wide Web</strong>, <strong>Email</strong>, <strong>Remote Administration</strong>, and <strong>File Transfer</strong> rely on <strong>TCP</strong>. Applications that do not require reliable data stream service may use the <strong>User Datagram Protocol</strong>(UDP), which provides a connectionless datagram service that emphasizes reduced latency over reliability.

## Protocol Operation
#### Connection Establishment
To establish a connection, <strong>TCP</strong> uses a <strong>Three-way Handshake</strong>. Before a <strong>Client</strong> attempts to connect with a <strong>Server</strong>, the <strong>Server</strong> must first bind to and listen at a port to open it up for connections: this is called a <strong>Passive Open</strong>. Once the passive open is established, a <strong>Client</strong> may initiate an <strong>Active Open</strong>. To establish a connection, the Three-way(or 3-step) Handshake occurs:

1.<strong>SYN</strong>:The <strong>Active Open</strong> is performed by the <strong>Client</strong> sending a <strong>SYN</strong> to the <strong>Server</strong>. The <strong>Client</strong> sets the segment's <ins>Sequence Number</ins> to a random value <strong>A</strong>.<br/>
2.<strong>SYN-ACK</strong>: In response, the <strong>Server</strong> replies with a <strong>SYN-ACK</strong>. The <ins>Acknowledgment Number</ins> is set to one more than the received <ins>Sequence Number</ins> i.e. <strong>A+1</strong>, and the <ins>Sequence Number</ins> that the <strong>Server</strong> chooses for the packet is another random number, <strong>B</strong>.<br/>
3.<strong>ACK</strong>: Finally, the <strong>Client</strong> sends an <strong>ACK</strong> back to the <strong>Server</strong>. The <ins>Sequence Number</ins> is set to the received acknowledgement value i.e. <strong>A+1</strong>, and the <ins>Acknowledgement Number</ins> is set to one more than the received <ins>Sequence Number</ins> i.e. <strong>B+1</strong>.

At this point, both the <strong>Client</strong> and <strong>Server</strong> have received an acknowledgment of the connection. The `steps 1, 2` establish the connection parameter(<ins>Sequence Number</ins>) for one direction and it is acknowledged. The `steps 2, 3` establish the connection parameter(<ins>Sequence Number</ins>) for the other direction and it is acknowledged. With these, a full-duplex communication is established.

#### Connection Termination
