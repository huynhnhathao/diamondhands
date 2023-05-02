---

layout: post
title:  "Học về mạng máy tính"
date:   2023-05-02 13:05:18 +0700
categories: computer-networking
---
Bài viết này sẽ đề cập tới rất nhiều vấn đề liên quan tới computer networking.
## The TCP/IP five layers network model
5 layers from bottom to top:
1. Physical: represent the physical devices that interconnect computers, including cables, connectors.
2. Data link layer: responsible for defining a common way of interpreting these signals so network devices can communicate. One protocol exists at this layer is Ethernet. The ethernet specifies physical layer attributes, it also defines a protocol responsible for getting data to nodes on the same network or link. 
3. Network layer, also called the internet layer: Allow different networks to communicate with each other through devices known as routers. A collection of networks connect to each other via routers is called inter-network. One of these is the internet. The most common protocol used at this layer is called IP or internet protocol. IP is the heart of the internet and most smaller network around the world. This layer deliver data between two individual nodes/computer.
4. Transport layer, relating to TCP/UDP. This layer deliver data received from the network layer to specific program in a node. The most commonly used protocol in this layer is TCP, or transmission control protocol. We usually heard TCP/IP, but they are two different protocols serve at two different layers. Another protocol at this layer is UDP or user dataframe protocol. TCP provides mechanisms for data to reliably deliver, while UDP does not.
5. Application layer, relating to HTTP, SMTP.
There are other models such as the 7-layers OSI model. The difference between this model and the TCP/IP model is that the OSI model abstracts the application layer into 3 layers.

## Basics of networking devices