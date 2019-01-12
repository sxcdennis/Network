# OSI Model

The OSI Model represents how data is transfered from one device to another over a network. OSI stands for Open Systems Interconnection. The OSI Model consists of 7 layers: Application, Presentation, Session, Transport, Network, Data Link, and Physical. The OSI model starts from layer 7 as the Sender and layer 1 as the Receiver.

As the data is sent through each layer, they are sent with an envelope also known as Protocol Data Units. Then once it reaches layer 1, the PDU is then removed going up from layer 1 to 7.  


**Example:**

![OSI](https://raw.githubusercontent.com/sxcdennis/Network/master/images/OSI.jpg)


# Application

The application layer is the interface that people use to interact with sending and  receiving data. This could be games, email, online, file transfer etc.



# Presentation

The presentation layer translates how the data will be formatted. Example: jpeg, pdf, png etc..


# session

The session layer allows communications between two devices.


# Transport

The transport layer is similar to a firewall control layer. Checks to see if there's any errors.


# Network

Provides routing finding the best route for delivery. Examples: IP address, Router, Subnet.


# Data Link

This layer makes sure that transmission occurs without any errors.  This layer consists of two sub layers: MAC (Media Access Control) and LLC (Logical Link Control).

MAC Layer is  the layer responsible for addressing.
LLC layer is responsible for framing the MAC addresses and checking for errors.

Example: NIC Cards


# Physical

Provides hardware used to send and receive data.
Example: Cat5,Cat6, FcoE cables, Modems


[< Back: Network Sharing](https://github.com/sxcdennis/Network/blob/master/Network%20Sharing.md "Network Sharing") || [Next: TCP/IP >](https://github.com/sxcdennis/Network/blob/master/TCP%26IP.md "TCP/IP")
