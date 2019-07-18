---
layout: post
title: Network Devices
subtitle: Network Devices
date: 2019-06-20
author: Jalever
header-img: img/computer_network_bg_simple.png
catalog: true
tags:
  - Computer Network
---

## Devices in Different Layers

![VjAeGn.png](https://s2.ax1x.com/2019/06/20/VjAeGn.png)

## Physical Layer

#### Repeater

Its job is to regenerate the signal over the same network before the signal becomes too weak or corrupted so as to extend the length to which the signal can be transmitted over the same network.

An important point to be noted about repeaters is that they do not amplify the signal. When the signal becomes weak, they copy the signal bit by bit and regenerate it at the original strength.

It is a 2 port device.

#### Hub

A hub is basically a multiport repeater.

A hub connects multiple wires coming from different branches, for example, the connector in star topology which connects different stations.

Hubs cannot filter data, so data packets are sent to all connected devices.  In other words, collision domain of all hosts connected through Hub remains one.  

Also, they do not have intelligence to find out best path for data packets which leads to inefficiencies and wastage.

###### Types of Hubs

- Active Hub
1.These are the hubs which have their own power supply and can clean , boost and relay the signal along the network.
2.It serves both as a repeater as well as wiring center.
3.These are used to extend maximum distance between nodes.

- Passive Hub
1.These are the hubs which collect wiring from nodes and power supply from active hub.
2.These hubs relay signals onto the network without cleaning and boosting them and can’t be used to extend distance between nodes.

## Data Link Layer

#### Bridge

A bridge operates at data link layer.

A bridge is a repeater, with add on functionality of filtering content by reading the MAC addresses of source and destination.

It is also used for interconnecting two LANs working on the same protocol.

It has a single input and single output port, thus making it a 2 port device.

###### Types of Bridges
- Transparent Bridges
1.These are the bridge in which the stations are completely unaware of the bridge’s existence i.e. whether or not a bridge is added or deleted from the network , reconfiguration of the stations is unnecessary.
2.These bridges makes use of two processes i.e. bridge forwarding and bridge learning.

- Source Routing Bridges
In these bridges, routing operation is performed by source station and the frame specifies which route to follow. The hot can discover frame by sending a specical frame called discovery frame, which spreads through the entire network using all possible paths to destination.

#### Switch
A switch is a multi port bridge with a buffer and a design that can boost its efficiency(large number of  ports imply less traffic) and performance.

Switch is data link layer device.

Switch can perform error checking before forwarding data, that makes it very efficient as it does not forward packets that have errors and  forward good packets selectively to correct port only.  

In other words, switch divides collision domain of hosts, but broadcast domain remains same.

## Network Layer

#### Rouer
A router is a device like a switch that routes data packets based on their IP addresses.

Router is mainly a Network Layer device.

Routers normally connect LANs and WANs together and have a dynamically updating routing table based on which they make decisions on routing the data packets.

Router divide broadcast domains of hosts connected through it.

#### Gateway
A gateway, as the name suggests, is a passage to connect two networks together that may work upon different networking models.

They basically works as the messenger agents that take data from one system, interpret it, and transfer it to another system.

Gateways are also called protocol converters and can operate at any network layer.

Gateways are generally more complex than switch or router.
