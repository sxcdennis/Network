# TCP/IP Model

The OSI Model gave birth to the TCP/IP Model. Which is actually used today for internet. Unlike the OSI model, the TCP/IP model consists of 4 layers: Application, Transport, Internet(or network) , Link layer/network access or Physical Layer.


# Application

Similar to the session and presentation layers of the OSI layer, the application layer translates and figures out how computer programs(internet browsers, mail) interact. Common protocols in this layer include: HTTP, FTP, SSH , DNS, DHCP, STMP

# Transport

Typically the  same as the OSI model- Responsible checking & transferring data and ports.  Common protocols include UDP and TCP.

**UDP (User Datagram Protocol):**

Typically not a reliable protocol. Doesn't check to see if you get all data. Useful for things like streaming media so it's faster. UDP does not send ACK (acknowledge) packets.

**TCP (Transmission Control Protocol):**

TCP Provides a reliable Connection. TCP enables a connection through handshake-(Three way handshake):

- The *client* sends a SYN flag to the *server* to request a connection
- The *server* sends a SYN-ACK flag to acknowledge the *client's* connection request
- The *client* sends an ACK to the server to acknowledge the *server's* connection request.

Once this connection is established, data can be exchanged through a TCP connection.

**EXAMPLE:**

![3_handshake](https://github.com/sxcdennis/Network/blob/master/images/threewayshake.jpg?raw=true)




# Network or Internet
This layer is similar to OSI model's Network layer. This layer specifies how packets are  moved between hosts.

This layer consists of IP and ICMP.

- IP stands for Internet Protocol: Responsible for routing packets from one host to another.
- ICMP stands for Internet Control Message Protocol: Responsible for telling hosts network problems.


# Link or Network Access Layer or Physical

This layer is similar to both the Data Link and Physical Layer of the OSI Model. It is responsible for defining hardware(MAC Addressing). This layer consists of a number of protocols which typically consists with ones that have to do with physical devices (cat5,cat6,NIC's).




[< Back: OSI](https://github.com/sxcdennis/Network/blob/master/OSI.md "OSI") || [Next: Basic DHCP >](https://github.com/sxcdennis/Network/blob/master/Basic%20DHCP.md "Basic DHCP")
