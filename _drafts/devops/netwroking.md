---
layout: post
title: "Networking"
category: jekyll update
---

### TCP/IP 5 Layer Model

|Layer|Protocol|Protocol Data Unit|Addressing|
|-----|--------|------------------|----------|
|Application|HTTP, HTTPS, SMTP |message|n/a|
|Transport|TCP, UDP|segment|port|
|Network|IP|datagram|IP address|
|Data Link|Ethernet, WiFi|frame|MAC address|
|Physical|10 Base T, 802.11|bits|n/a|

### Physical Network
#### Cables
Cables provide point to point connection to two devices and allow communication signal to transmit.

- Copper: use electrical signal. Different type of copper cables - Cat5, Cat5e, Cat6 etc.
- Fiber: use light signal.

#### Hub
Hub is also a physical layer device but allows connection from multiple computers/devices. But a message to Hub is transmitted to all the devices in the network and it is upto each device to recognize if the message is meant for it or not.

#### Collision Domain
The nature of Hub communication creates a scenario which is called collision domain. Collision domain is a part of network where shared connection created collision among the messages sent over the connection. Then each device need to wait a random amount time before sending message again.

### Data Link Layer
#### Switch
Switch is also a device that allows multiple computers/devices to connect with it. But it is a data link layer device and can inspect the data link layer data to identify which device in the network a message is intended for and send the message to that device only.