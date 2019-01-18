# Basic Trouble Shooting Tools


# ICMP

Internet Control Message Protocol (ICMP) is part of the TCP/IP model. It is used to send updates and error messages and is used for debugging network issues such as failed packet delivery.

Each ICMP message contains a code, type and checksum field. The type field is the tpye of ICMP message, the code is a sub-type and describes mroe information about the message and the checksum is used to detect any issues with the integrity of message.

Some common ICMP Types:

Type 0 - Echo Reply
Type 3 - Destination Unreachable
Type 8 - Echo Request
Type 11 - Time Exceeded

When a packet cannot get to a destination, Type 3 message is generated, within type 3 there are 16 codew values that will further describe why it can't get to its destination. It'll say something like:

Code 0: Network Unreachable
Code 1: Host Unreachable

# Ping

One of the most simplest networking tools is ping. It is used to test whether or not a packet can reach a host. It works by sending ICMP echo request (Type 8) packets to the destination host and waits for an ICMP echo reply (Type 0). Ping is sucessful when a host sends out the request packet and receives a response from the target.

![ping](https://raw.githubusercontent.com/sxcdennis/Network/master/images/ping.png)

In this example we are using ping to see if we can reach www.google.com.

**icmp_seq**
The icmp_seq indicates the number of packets sent, so in this case we sent out 5 packets. You can see it numbered in order.


**ttl**

Time to Live (ttl) field is used as a hop counter, as you make hops, it reduces the counter by one every time until you reach 0, then the packet dies. That means the packet is given a lifespan.


**time**

The roundtrip time it took from you sending echo request packet to getting an echo reply back.

# Traceroute



# netstat


# Packet Analysis






[< Back: Basic Network Config](https://github.com/sxcdennis/Network/blob/master/Basic%20Network%20Config.md "Basic Network Config") || [Next: DNS >](https://github.com/sxcdennis/Network/blob/master/DNS.md "DNS")
