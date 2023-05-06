---

layout: post
title:  "Computer networking"
date:   2023-05-02 13:05:18 +0700
categories: computer-networking
---
We will talk a lot about computer networking in this post.
# Introduction to computer networking
## The TCP/IP five layers network model
5 layers from bottom to top:
1. Physical: represent the physical devices that interconnect computers, including cables, connectors.
2. Data link layer: responsible for defining a common way of interpreting these signals so network devices can communicate. One protocol exists at this layer is Ethernet. The ethernet specifies physical layer attributes, it also defines a protocol responsible for getting data to nodes on the same network or link. 
3. Network layer, also called the internet layer: Allow different networks to communicate with each other through devices known as routers. A collection of networks connect to each other via routers is called inter-network. One of these is the internet. The most common protocol used at this layer is called IP or internet protocol. IP is the heart of the internet and most smaller network around the world. This layer deliver data between two individual nodes/computer.
4. Transport layer, relating to TCP/UDP. This layer deliver data received from the network layer to specific program in a node. The most commonly used protocol in this layer is TCP, or transmission control protocol. We usually heard TCP/IP, but they are two different protocols serve at two different layers. Another protocol at this layer is UDP or user dataframe protocol. TCP provides mechanisms for data to reliably deliver, while UDP does not.
5. Application layer, relating to HTTP, SMTP.
There are other models such as the 7-layers OSI model. The difference between this model and the TCP/IP model is that the OSI model abstracts the application layer into 3 layers.

## Basics of networking devices
### Cables
Connect different devices to each other, allowing data to be transmitted over them. Two categories: Copper and fiber. 
1. Copper: computer on one end transfer binary data to another end by changing the voltages between two ranges. The receiver can interpret the changing of voltages and translates them to 1 and zero, then to the final data. There are different types of copper wires, cat3, cat5, cat5e, cat6e,... are just short name for category 3, 5, 5e,... They are similar under the normal eyes, but different in how the internal wires are arranged. Just the arrange of inside wires can decide how fast and how resistent are the signal to outside event. 
   1. Crosstalk is when an electrical pulse on one wire is accidentally detected on another wire. So the receiving end can not interpret the data. Cat6 cable can transfer more and reliable data compare to previous cat cables, but they have a shorter maximum distance compare to other cats!
2. Fiber: Contain individual optical fibers, which are tiny tube made out of glass about the width of a human hair. Fiber transfer pulse of light to represent 1 and 0 instead of electric pulse! Fiber of course transfer data much faster and over longer distance without potential data loss than copper

### Hubs ad Switches
1. A Hub is a physical device that allows for connections from many computers at once. All devices talking to a hub will talk to all other devices connect to that hub, like when you talk in a silent room and everyone can hear you. It's up to other devices to decide if it is the one that is being talked to. Apparently too many noise for participants in the network and cause something called a collision domain.
   1. Collision domain is a network segment where only one device can communicate at a time. If multiple systems try sending data at the same time, the electrical pulse sent across the cable can interfere with each other -> cause slow data transfer. This thing should be on the museum nowadays.
2. Switch is similar to a Hub in a sense that it also connects multiple devices together, however a switch is a data link layer device while a hub is a physical layer device. A switch can inspect the data being sent to it and determines which participant in the network is intended to receive this data. This can completely eliminate data collision in a segment of the network because devices joining the network won't receive data that was not intended for them.
Hubs and switches are the primary devices used to connect computers on a single network, usually referred to as a LAN or local area network.
### Routers
Router is a device that knows how to forward data between independent networks. Routers are layer 3: network layer devices. Routers can inspect IP data to determine where to send data. Routers used in homes and offices receive requests from devices, then forward that requests to ISP or internet service provider, where most of the sophisticated stuffs happened. Routers share data with each other via a protocol called Border Gateway Protocol or BGP, which lets them learn about the most optimal paths to forward traffic. Data requested by your device may travel through a bunch of routers over the internet before it arrived at your device.

### Servers and clients
We call all any device that connects to the internet a node. A server is something provides data to something that is requesting that data. Individual programs run on the same node can be client and servers of each others. Most nodes are both a server and a client, such as an email server is also a client of a DNS server
## The Physical layer
1. Everything go from the internet to your devices can be broken down to bits. Bit is the smallest information unit that computers work with. The process of varying the voltage of the charge moving across a copper cable is called Modulation. 
2. Twisted pair cables are the most common type of cable, it features pairs of coppers wires that are twisted together. The twisted nature help it prevent electron-magnetic interference and crosstalk from neighboring pairs.
3. Duplex communication is the concept that information can flow in both directions across the cable. But doesn't mean that they can communicate at the same time.
4. Full-duplex mean both ends can communicate at the same time.
5. Simplex communication is unidirectional. Only one end can communicate with the other.
6. Half-duplex means can communicate both directions but can not at the same time.
7. Network ports: the end of a physical cable is a plug. It need to be plugged into a port. The most common plug is the RJ45 or register jack 45. It's one of many cable plug specification but by far is the most common. Of course a RJ45 plug can connect to a RJ45 port. Switches will have many network ports because it connects many devices together. Network ports usually have 2 LED lights for "debugging" the network status. One of them is the `link` light, it will be lit when the cable properly connected to two devices that are both powered on. Another is the `activity` light, which will flash when there is data actively transmitted across the cable.