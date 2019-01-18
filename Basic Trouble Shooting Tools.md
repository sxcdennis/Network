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

traceroute command is used to see how packets are getting rotued. This works by sending packets with increasing TTL values, starting with 1. So the first router gets the packet and then it reduces the TTL values by one, then dropping the packet.  So basically traceroutes works by sending and dropping packets.

![traceroute](https://raw.githubusercontent.com/sxcdennis/Network/master/images/traceroute.png)

Each line is a machine that is between me and the target. Since there's only one router, it just has one line.

You can use the -m option to change count.


# netstat
netstat displays information such as network connections, routing tables, information about interfaces and more.
 A **socket** is an interface that allows programs to send and receive data. A **port** is used to identify which application should send or receive data.
The **socket address** is a combination of the IP address and port.
Every connection between a host and destination requires a unquie socket. For example, HTTP Is a service that runs on port 80, however we can have many HTTP connections and to maintain each connection a socket gets created per connection.

![netstat](https://raw.githubusercontent.com/sxcdennis/Network/master/images/netstat.png)

The netstat -a command shows the listening and non-listening sockets for network connections, the -t option shows only tcp connections.

Proto: Protocol used, TCP or UDP
Recv-Q: Data that is queued to be recieved
Send-Q: Data that is queued to be sent
Local Address: Locally connected host
Foreign Address: Remotely Connected host
State: The state of socket


# Basic Packet Analysis

There are two extremely popular packet analyzers- Wireshark and tcpdump
These tools can scan your network interfaces, capture the packet activity, parse the packages and output the information for us.

I'll go over some of the basics of tcpdump

**Install**

```
yum -y install tcpdump

```

**Capture a packet on an interface**

```

tcpdump -i ens33

```

![tcpdump1](https://raw.githubusercontent.com/sxcdennis/Network/master/images/tcpdump1.png)


**Understanding Output**

1. The first field is a timestamp of the network activity: 08:47:05.636898
2. IP, this contains the protocol information: Ip6 or IP followed by IP adddress. Or gateway or localhost.
3. Source and destination address: localhost.localdomain.33636 > gateway.domain

**Writing tcpdump to a file**

You can write the dumps to a file with the -w option.

```

tcpdump -w /my/file.txt

```



[< Back: Basic Network Config](https://github.com/sxcdennis/Network/blob/master/Basic%20Network%20Config.md "Basic Network Config") || [Next: DNS >](https://github.com/sxcdennis/Network/blob/master/DNS.md "DNS")
