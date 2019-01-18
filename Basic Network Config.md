# Basic Network Config


# Network Interfaces

A Network interface is how the kernel links up the software side of networking to hardware. You can see your network inferface by using ifconfig or even ip command. ifconfig has more options.


![ifconfig](https://raw.githubusercontent.com/sxcdennis/Network/master/images/ifconfig.png)

**ifconfig**
The ifconfig tool allows you to configure network interfaces specficially. Most common interfaces you'll see are eth0(ethernet), wlan0(wireless),lo(loopback interface). THe loopback is used to represent your computer, it just loops to yourself. lo is good for debugging or connecting to servers running locally.

You can bring up or down an interface- Also you can turn off your interface as well. HWAddr represents the MAC Address, inet  is the IPv4 adress, inet6 Ipv6 address. There is also subnetmask and broadcast address there as well..

**To creater an interface and bring it up using ifconfig**

```

ifconfig eth0 192.168.101.2 netmask 255.255.255.0 up

```

**Bring up or down interface**

```

ifup eth0
ifdown eth0

```

**ip**

As stated earlier the ip command also allows us to manipulate network stack.


**List interfaces**

```

ip a

```

**Show the stats of an interface**

```

ip -s link show ens33

```


**bring interfaces up and down**

```
ip link set ens33 up
ip link set ens33 down

```
**add an ip address to an interface**

```

ip address add 192.168.101.2/24 dev ens33

```


# Route

You can add or delete routes manually using the route command.

**Add new rotue**


```

route add -net 192.168.101.1/23 gw 190.10.22.3

```

**Delete a route**

```

route del -net 192.168.101.1/23


```


**Add a route to existing**

```

ip route add 192.168.101.1/23 via 190.10.22.3

```


**Delete a route to existing**

```

ip route delete 192.168.101.1/23 via 190.10.22.3

OR

ip route delete 192.168.101.1/23

```

# dhclient

most likely you'll be using dhclient instead of manually setting up ip addresses.


# Network Manager

This is one of my favorites personally..
The network manager puts all of the configurations together. There are
3 types of network managers- nmt-tool, nmtui and nmcli. They are all the same.
nm-tool is for GUI. nmtui and nmcli can work for a non-gui client.

# ARP

ARP stands for Address Resolution Protocol. It's a protocol for mapping Internet addresses to physical machines that are recognized by local networks.

A table called ARP cache is used to maintain a correlation between each MAC address and its corresponding IP address.

You can view the ARP cache by using the command *arp*
You can also see the ARP cache by using the command ```ip neighbour show```

![arp](https://raw.githubusercontent.com/sxcdennis/Network/master/images/arp.png)


The ARP cache is actually empty when a machine boots up, it gets populated as packets are being sent to other hosts. If we send a packet to a destination that isn't in the ARP cache, the following happens:

The source host creates the Ethernet frame with an ARP request packet

The source host broadcasts this frame to the entire network

If one of the hosts on the network knows the correct MAC address, it will send a reply packet and frame containing the MAC address

The source host adds the IP to MAC address mapping to the ARP cache and then proceeds with sending the packet.


[< Back: Basic Routing](https://github.com/sxcdennis/Network/blob/master/Basic%20Routing.md "Basic Routing") || [Next: Basic Troubleshooting Tools >](https://github.com/sxcdennis/Network/blob/master/Basic%20Trouble%20Shooting%20Tools.md "Basic Troubleshooting Tools")
