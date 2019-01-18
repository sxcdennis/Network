# Basic Routing
On a typical router, you'll have LAN ports that allow your machine to connect to the same local area network. You will also have a Internet port that connects you to the Internet, sometimes it'll say WAN- because it basically connects you to a wider network. A router decides where our network packets go and which ones comes in. It routes packets between multiple networks from source & destination.

**Hops**
Hops help measure the distance a packet must travel to get from one place to another.
 Let's say to I have two routers connecting host A to host B, so therefore we say there are two hops between host A and host B. Each hop is a intermediate device like the routers that we must pass through.

**Difference between Routing, Switching and Flooding**
ROUTING is the process of creating the routing table, so we can do receiving, processing, and forwarding better than SWITCHING.
Packet SWITCHING is receiving, processing and forwarding data to destination.
FLOODING is when a router doesn't know which way to send a packet then every incoming packet is sent through every outgoing link except the one it arrived on

# Routing Table

Use ```route -n``` to show routing table.

![OSI](https://raw.githubusercontent.com/sxcdennis/Network/master/images/routetable.png)

**Destination**

In the first field we have the destination IP address of 192.168.101.0, this says that any packet that tries to go to this network, will go through (ens33). If I was 192.168.101.4 and wanted to get to 192.168.101.8, I would just use the network  interface ens33.

There's also an **0.0.0.0** address which means there's no specified address or it's unknown. For example, I want to send a packet to 125.117.43.5, our routing table doesn't know where that goes - so it denotes it to 0.0.0.0 and therefore routes our packet to the Gateway.


**Gateway**

If we are sending a packet that is not on the same network, it will be sent to this Gateway address.

**Genmask**

This is our subnet mask, if you remebmer from the subnet section.

**Flags**

**UG**- Network is Up and is a Gateway
**U**- Network is Up

**Iface**

This is the interface that our packet is going out of.


# Path of a Packet

**How Packet is traveled through LAN**

1. Local machine will compare destination IP to see if the same subnet by looking at subnetmask
2. When packets are sent they need source MAC address, destination MAC address, source IP and destination IP.
3. To get to destination host, we use ARP to broadcast a request on the local network to find the MAC address of the detination host.
4. Now the packet can be successfully sent

**How Packet is traveled outside of Network**

1. First, the local machine will compare destination IP since it's outside the network. You dont know MAC address since its not in the same network and we cant use ARP because ARP request is local only.

2. Packets now look into routing table, it doesn't know the address of destination IP, so it sends it out to the default gateway (another rotuer). Now our packet contains source IP, destination IP and source MAC Address, but no destination MAC address.

3. The router looks at the packet and confirms the destination MAC address, but it's not the final destination IP address, so it keeps looking at the routing table to forward the packet to another IP address that can help the packet move to its destination. Every time the packet moves, it strips the old source and destination MAC address and updates the packet with new source and destination MAC address.

4. Once the packet gets forwarded to the same network, we use ARP to find the final destination MAC address.

5. During this process, our packet doesn't change the source or destination IP address.




# Routing Protocols

There are three main routing protocols. Distance Vector Protocols , Link State Protocols, and Border Gateway Protocol. These help us configure routing tables so we don't have to manually do them.

**Convergence**
When using routing protocols, routers communicate with each other to exchange information about the network- this is called *converging*. Basically showing the whole network topology, how routing tables are mapped etc. When something occurs in the network topology, the convergence will temporarily break until the routers are aware of the change.




# Distance Vector Protocols

Using the hop count a packet takes to get across the network, Distance Vector protocols determine the path of other networks. For example: If a network named A was 4 hops away and Network B was next to Network A, then we must be 5 hops away. In DVP, the next route would be the one with the least amount of hops.

DHP is good for small networks, but when in larger networks its not as great. Another downside is it chooses routers that are closer in hops, but it may not be the most efficient route.

One of the common protocols within DHP is RIP ( Routing Information Protocol), it broadcasts the routing table to every router in the network ever 30 seconds. For bigger networks, RIP can be bad because the limit is 15 hops.


# Link State Protocols

Link state protocols are great for larger networks. Instead of using RIP, Link state protocols send routing tables only to neighboring routes. They use a different algorithm to calculate shortest path.

A common protocol within Link State protocols is OSPF ( OPen shortest path first), it only updates routing tables if there was a network change. Also there's no hop limit.


# Border Gateway Protocol

Border Gateway Protocol is basically how the Internet runs. It's used to collect and exchange routing information between systems.

Lets say you were on your home network and I'm at a Coffee shop. I want to communicate with you through email so I send an email through the coffee shop's network. It bounces throughout all the routing tables until it finally reaches the Broader Gateway router. Then this router contains information to leave the coffee shop's network and transverse to other networks.


[< Back: Subnetting](https://github.com/sxcdennis/Network/blob/master/Subnetting.md "Subnetting") || [Next: Basic Network Config >](https://github.com/sxcdennis/Network/blob/master/Basic%20Network%20Config.md "Basic Network Config")
