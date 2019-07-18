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

- [Overview](#overview)
- [Protocol Operation](#protocol-operation)
    - [Connection Establishment](#connection-establishment)
    - [Connection Termination](#connection-termination)

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
The <strong>Connection Termination Phase</strong> uses a <strong>Four-way Handshake</strong>, with each side of the connection terminating independently. When an endpoint wishes to stop its half of the connection, it transmits a <strong>FIN</strong> packet, which the other end acknowledges with an <strong>ACK</strong>. Therefore, a typical tear-down requires a pair of <strong>FIN</strong> and <strong>ACK</strong> segments from each <strong>TCP</strong> endpoint. After the side that sent the first <strong>FIN</strong> has responded with the final <strong>ACK</strong>, it waits for a timeout before finally closing the connection, during which time the local port is unavailable for new connections; this prevents confusion due to delayed packets being delivered during subsequent connections.
![ZOzXdO.png](https://s2.ax1x.com/2019/07/18/ZOzXdO.png)

A connection can be "half-open", in which case one side has terminated its end, but the other has not. The side that has terminated can no longer send any data into the connection, but the other side can. The terminating side should continue reading the data until the other side terminates as well.

It is also possible to terminate the connection by a <strong>3-way Handshake</strong>, when <ins>host A</ins> sends a <strong>FIN</strong> and <ins>host B</ins> replies with a <strong>FIN</strong> & <strong>ACK</strong> (merely combines 2 steps into one) and <ins>host A</ins> replies with an <strong>ACK</strong>.

Some host <strong>TCP stacks</strong> may implement a half-duplex close sequence, as `Linux` or `HP-UX` do. If such a host actively closes a connection but still has not read all the incoming data the stack already received from the link, this host sends a <strong>RST</strong> instead of a <strong>FIN</strong>. This allows a <strong>TCP</strong> application to be sure the remote application has read all the data the former sent—waiting the <strong>FIN</strong> from the remote side, when it actively closes the connection. But the remote <strong>TCP stack</strong> cannot distinguish between a <ins>Connection Aborting RST</ins> and <ins>Data Loss RST</ins>. Both cause the remote stack to lose all the data received.

Some application protocols using the <strong>TCP open/close handshaking</strong> for the application protocol open/close handshaking may find the <strong>RST</strong> problem on active close. As an example:
![ZOzqL6.png](https://s2.ax1x.com/2019/07/18/ZOzqL6.png)
For a program flow like above, a <strong>TCP/IP</strong> stack like that described above does not guarantee that all the data arrives to the other application if unread data has arrived at this end.
