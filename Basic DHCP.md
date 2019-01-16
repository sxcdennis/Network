# Basic DHCP

DHCP- Dynamic host configuration protocol is a network protocol that enables a server to automatically assign IP addresses. This means that each time a client boots up a *dynamtic* IP address vs *static* IP address that never changes. The IP address that is assigned by a **DHCP Server** to **DHCP Client** is on a **lease**. The lease time can vary depending on how long a client is to require a connection **or** is configured by the DHCP Server.
In this section we'll go over how a DHCP Works, Installing DHCP Server and Configuring DHCP Client.

# How DHCP works
To briefly explain how DHCP works there are 4 steps:
1. DHCP Discover
2. DHCP Offer
3. DHCP request
4. DHCP ACK

When a **Client** is connected to a network (with DHCP), it forwards a **DHCPDISCOVER** message to the **DHCP Server**.

After the **DHCP Server** receives the **DHCPDISCOVER** message, it replies with a **DHCPOFFER** message to the **Client**.

Then the **client** receives the **DHCPOFFER** message, and it sends a **DHCPREQUEST** message to the **server** indicating it's prepared to get the network configuration offered in the **DHCPOFFER** message.

Finally, the **DHCP Server** receives the **DHCPREQUEST** message from the **Client**, and sends the **DHCPACK** message showing that the client is now permitted to use the IP address assigned to it.

Image of DHCP ACK:

![dhcp](https://github.com/sxcdennis/Network/blob/master/images/dhcp.png?raw=true)



# Installing & Configuring DHCP Server

**1.** Install DHCP

```

yum install -y dhcp

```

**2.** Add specific interface to DHCPDRAGS on file **/etc/sysconfig/dhcpd/**

For example if your card is *eth0* then add:

```

DHCPDRAGS=eth0

```

**3.** Configure DHCP config file.

The config file for dhcp server is located at **/etc/dhcp/dhcpd.conf** . It is normally blank, but if you want to have an example file it's located at ```/usr/share/doc/dhcp*/dhcpd.conf.example``` file.

Start by copying that file.

```
cp /usr/share/doc/dhcp*/dhcpd.conf.example /etc/dhcp/dhcpd.conf

```

There are two types of statements defined in the configuration file.

**parameters:** - State how to carry out a task, weather to perform a task, or what network configuration options to send DHCP client.

**declarations:** - Specifies the network topology, defines the clients, offers addresses for the client, or apply a group of parameters to a group of declarations.

**4.** Open main config file and define DHCP server Options.

```

vi /etc/dhcp/dchcpd.conf

```

Set global parameters which will apply to all subnetworks (specify values that apply to your scenario) at the top of the file:

```

option domain-name "example.com";
option domain-name-servers ns1.example.com, ns2.example.com;

default-lease-time 600;
max-lease-time 7200;


```

**5.** Define subnetwork (For this example we'll use 192.168.101.0/24)

```
subnet 192.168.56.0 netmask 255.255.255.0 {
 range   192.168.101.2   192.168.101.200;
 option routers 192.168.101.1;

}

```
**Step 5.5: Assigning Static IPs to DHCP Client**

You can assign static IP to a computer on the network in **/etc/dhcp/dhcpd.conf** file by specifying its MAC address and the static ip.

Example:


```

host dennis {
  hardware ethernet 0:0:c0:5d:bd:95;
   fixed-address 192.168.101.69;  
}

host bob {
  hardware ethernet 08:00:07:26:c0:a5;
  fixed-address 192.168.101.105;
}


```

**6.** You can start DHCP service

```

systemctl start dhcp
systemctl enable dhcp


```

**7.** Permit DHCP service on firewall

```

firewall-cmd --add-service=dhcp --permanent
firewall-cmd --reload

```

# Configuring DHCP Client

On a client computer(s) you can configure your network to automatically receive addresses from the DHCP server. There are a number of options, you can use GUI option, you can edit configuration files directly or use nmtui.

The configuration files are located at /etc/sysconfig/network-scripts/ifcfg-inferfacename/

Example my interface name is ens33:

```
vi /etc/sysconfig/network-scripts/ifcfg-ens33/


```

Make sure to have the following:

```

BOOTPROTO=dhcp
TYPE=Ethernet
ONBOOT=yes

```

**Using nmtui:**

By default your connection should be using dhcp, but if it isn't you can use your network manager using ```nmtui```. Instead of choosing *manual*, choose *automatic*

![nmtui](https://github.com/sxcdennis/Network/blob/master/images/EditConnectionManual.png?raw=true)



Once you're done with configuring dhcp on the client you can reset network service.

```

systemctl restart network

```

[< Back: TCP/IP](https://github.com/sxcdennis/Network/blob/master/TCP%26IP.md "TCP/IP") || [Next: Subnetting >](https://github.com/sxcdennis/Network/blob/master/Subnetting.md " Subnetting")
