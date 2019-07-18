---
layout: post
title: TCP 3 ways Handshake Process
subtitle: Network Devices
date: 2019-06-20
author: Jalever
header-img: img/computer_network_bg_simple.png
catalog: true
tags:
  - Computer Network
---

TCP(Transmission Control Protocol)

UDP(User Datagram Protocol)

UDP is mostly used as querying the DNS server to get the binary equivalent of the Domain Name used for the website.

TCP provides reliable communication with something called Positive Acknowledgement with Re-transmission(PAR).

The Protocol Data Unit(PDU) of the transport layer is called `segment`.

## processes

![VjhuUs.png](https://s2.ax1x.com/2019/06/20/VjhuUs.png)

- Step 1 (SYN) : In the first step, client wants to establish a connection with server, so it sends a segment with SYN(Synchronize Sequence Number) which informs server that client is likely to start communication and with what sequence number it starts segments with
- Step 2 (SYN + ACK): Server responds to the client request with SYN-ACK signal bits set. Acknowledgement(ACK) signifies the response of segment it received and SYN signifies with what sequence number it is likely to start the segments with
- Step 3 (ACK) : In the final part client acknowledges the response of server and they both establish a reliable connection with which they will start eh actual data transfer
