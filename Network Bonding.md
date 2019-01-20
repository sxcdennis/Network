# Network Bonding

Network bonding is a method of combining two or more network interfaces together. Its main purpose is to provide high availability and redundancy.


![NetBond1](https://github.com/sxcdennis/Network/blob/master/images/NetBond1.png?raw=true)

Lets say you have bonded two ports and one goes down, you still have one port left- Therefore you have redundancy.

You take the two ports bonded both 1G each and now you have a 2G port, thus giving High Availability.




# Network Bonding Procedure

- modprobe bonding
- modinfo bonding
- Create /etc/sysconfig/network-scripts/ifcfg-bond0
- edit /etc/sysconfig/network-scripts/ethernet1
- edit /etc/sysconfig/network-scripts/ethernet2


**Step 1:** Enable modprobe
```

modprobe --first-time bonding

````

**Step 2:** Create bond0 file configuration file.

``vi /etc/sysconfig/network-scripts/ifcfg-bond0``

Add following lines:

```

DEVICE=bond0
NAME=bond0
TYPE=Bond
BONDING_MASTER=yes
BOOTPROTO=none
ONBOOT=yes
IPADDR=192.168.101.225
BONDING_OPTS="mode=1 miimon=100"

```
**Step 3:** Edit first NIC file. (ens33)

Add or edit the following lines

```
BOOTPROTO="none"
ONBOOT="yes"
MASTER=bond0
SLAVE=yes

```

**Step 4:** Edit second NIC file. (ens37)

Add or edit the following lines

```
BOOTPROTO="none"
ONBOOT="yes"
MASTER=bond0
SLAVE=yes

```

**Step 5** Restart network


```

systemctl restart network

```

**Step 6** Testing bonding

```

cat /proc/net/bonding/bond0

```
This will show the output depending on what mode you put for bond0 config. (in this case 5 = load balancing)

```

ip a

```
If the other cards were put to SALVE and you now  have bond0 with the correct IP address.. Then you should be good!



[< Back: SSL & TLS](https://github.com/sxcdennis/Network/blob/master/SSL%20%26%20TLS.md "SSL & TLS") || [Next: Installing NFS >](https://github.com/sxcdennis/Network/blob/master/Installing%20NFS.md "Installing NFS")
