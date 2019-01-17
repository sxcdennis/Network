# Basic Subnet

Subnet is short for subnetwork. Subnetworking is the process of breaking a network down into different pieces. There are three main reasons for subnetting: Security, Organization (can split by departments) and performance. A router allows different subnetworks to communicate with each other.

Example:

![subnet](https://github.com/sxcdennis/Network/blob/master/images/subnet.png?raw=true)


# IPv4 & Addressing

An IP address is separated into *octets* followed by periods. So there are 4 octets in an IPv4 address. Each octet is 8 bits and 8 bits is equal to 1 byte, so we refer to an IPv4 address as 4 bytes. We use bits to subnet.


This address contains two parts: Network ID and Host ID.  The default point that separates the Network ID and Host ID depends on weather the address is Class A, Class B or Class C address.

**Ranges:**

Class A: 1.0.0.0-126.255.255.255
Class B: 128.0.0.0-191.255.255.255
Class C: 192.0.0.0-223.255.255.255

**Private IP Ranges:**

Class A: 10.0.0.0 - 10.255.255.255
Class B: 172.16.0.0 - 172.31.255.255
Class C: 192.168.0.0 - 192.168.255.255

**Example of Network ID and Host ID:**

Class A: 10.20.30.40
Class B: 172.16.32.5
Class C. 192.168.1.251

Class A- The Network ID is the 10. The HostID is 20.30.40
Class B - The Network ID is 172.16 and the HOSTID is 32.5
Class C- The Network ID is 192.168 and the HostID is 1.251


# Subnet Masks

A subnet mask is a number that defines a range of IP addresses that can be used in a network. They are used to designate subnetworks, which are typically LANs that are connected to the internet. As stated earlier, systems that are in different subnets cannot communicate with each other without a router.

Subnet mask hides, or "masks", the network part of a system's IP address and leaves only the host part of the host ID. A common Class C IP subnet mask is - 255.255.255.0

So a subnet mask shows the difference between HOST ID and Network ID.

Example:
IP: 192.168.1.1
Subnet Mask: 255.255.255.0

This subnet mask represents that the first 3 octet are the host ID and the last octet is the Network ID.

Typical Subnet Masks:

A: 255.0.0.0
B: 255.255.0.0
C: 255.255.255.0


# Subnet Maths

So we know that subnet masks help figure out how many hosts we can have in a subnetwork. We want to know how many that can be exactly.

So lets say we have an ip address **192.168.1.0** and a subnetmask of **255.255.255.0** and we convert these to binary form.

```

192.168.1.165  = 11000000.10101000.00000001.10100101

255.255.255.0  = 11111111.11111111.11111111.00000000

```
So every time there's a 1 in the subnet mask it is masked, meaning we cant see/use it for the ip. That means we're left with IPs from 0-255, thus leaving us 256 available IP addresses - because the range is from 00000000-11111111 in binary which is 0-255. But we have to subtract 2 hosts because we have to account for the broadcast addresses and subnet address leaving us with 254 addresses. So the range of IPs is 192.168.1.1-192.168.254

# Subnetting Rules/Steps

This set of rules/steps help you find your subnet and subnet range. Typical questions would include finding number of hosts, the network address and broadcast address.

**1.**  Determine IP Class (A , B , C)
**2.** Identify Network ID & Host ID
**3.**  Apply Default Network Mask (Ex Class C: 255.255.255.0)
**4.** Convert Subnet Mask to Binary (Example Class C: 11111111.11111111.11111111.00000000)
**5.**  Use (2^n)-2 to determine custom subnet mask
**6.**  Determine Least significant Bit to give 1st subnet + range

Lets go over these steps 1 by 1 in an example.

Lets say our IP is **172.16.0.0**
We also need 11 networks.

**Step 1.**

This is a class B


**Step 2.**

The network ID is 172.16 and the HostID will be the last 0.


**Step 3.**

The Default Network mask is **255.255.0.0**


**Step 4.**

Subnet mask is: **11111111.11111111.00000000.00000000**

**Step 5.**

So we need (2^n)-2 to be greater than or equal to 11. So that n can equal anything above 4. We will just use 4 as an example here.
(2^4)-2=14.
Now we need to do some conversions. First take the 4 and add that to the number of 1's we add to the binary number.
So our new custom subnet mask is **11111111.11111111.11110000.00000000** now convert that back to decimal. To convert it we use a trick- We used 2^4 so we need to add the numbers from 2^4 to 2^7. In this case- (2^4)+(2^5)+(2^6)+(2^7)=240. This is our new subnet mask: **255.255.240.0**

**Step 6.**

Our least significant bit is 2^n = 2^4 =16. This tells us that our subnets will be 16 x n . So we put this number to the third octet.
Our first subnet is **172.16.16.0**  Then our next subnet can be **172.16.32.0**, and we can keep going on.
So our range of the first subnet is **172.16.16.0-172.16.31.255**
Our range of the second subnet is: **172.16.32.0-172.16.47.255**


Lets try another example.
Lets say we see an IP of: 172.16.0.0/20
To convert this to binary it is: 20: 1's and rest 12: 0's
**11111111.11111111.11110000.00000000**
To convert this to decimal. We look at the 2^7 chart

```

128|64|32|16|8|4|2|1

```

All we need to do is convert this by adding the numbers of 1's. So since we have 4 1's we add the first 4 numbers from 2^7 to 2^4
128+64+32+16= 240
So our number is 255.255.240.0

Another trick is to convert decimals to binary. To convert decimals to binary we simply look at the 2^7 chart again.

```

128|64|32|16|8|4|2|1

```

Lets say for example we're converting 172 to binary. You want to keep subtracting 172 from the left to right until you get 0's and the remainder numbers will be 0s.
For example lets convert 172.

1. You can subtract 172 by 128 so that's a 1. (172-128=44)
2. Now use the remaining number 44. But 44 cannot subtract by 64 so that's a 0.
3. Next 44 can subtract by 32 so that's a 1. (44-32=12).
4. Next 12 cannot subtract by 16 so that's a 0.
5. Now you can subtract 12 by 8, so that's a 1. (12-8=4)
6. Finally you can subtract 4 by 4 so that's a 1. (4-4=0)
7. Rest is 0
8. Rest is 0

So the binary for 172 number is: 10101100


## Subnet Example

Now we know how to convert binary to decimal and decimal to binary. We can do an example.

So lets say we have an IP & Subnetmask : **192.168.2.64/26**

We want to find 3 things:

1. What is the network address? (First address)
2. What is the broadcast address? (Last address)
3. How many hosts are there?


Alright first, we convert everything to binary.

Binary Subnetmask:
This was given to us so it's a bit easier the 26 means there's 26 1's and 6 0's

**11111111.11111111.11111111.11000000**

Binary IP:

**192.168.2.64**

This we go back to our 2^7 chart

```

128|64|32|16|8|4|2|1

```

First we convert 192 to binary. Followed by 168, then 2 and then 64.

```

1. 192-128=64 : 1
2. 64-64=0 : 1
3. 0
4. 0
5. 0
6. 0
7. 0
8. 0

1. 168-128=40 : 1
2. 40-64=Neg : 0
3. 40-32=8 : 1
4. 8-16=Neg : 0
5. 8-8=0 : 1
6. 0
7. 0
8. 0

1. 2-128=Neg : 0
2. 2-64=Neg: 0
3. 2-32=Neg: 0
4. 2-16=Neg: 0
5. 2-8=Neg: 0
6. 2-4=Neg: 0
7. 2-2=0 : 1
8. 0

1. 64-128=Neg : 0
2. 64-64=0 : 1
3. 0
4. 0
5. 0
6. 0
7. 0
8. 0

```

Now we have our binary number. **11000000.10101000.00000010.01000000**


Now we know our binary numbers:

Subnetmask: **11111111.11111111.11111111.11000000**
IP Address: **11000000.10101000.00000010.01000000**

So the Network Address is the first number which is - **11000000.10101000.00000010.01000000** converted to decimal.
Which is **192.168.2.64** (shown from beginning)

Broadcast Address which is the last number: **11000000.10101000.00000010.01111111** converted to decimal:

Again, go back to the 2^7 chart to convert *01111111*

```

128|64|32|16|8|4|2|1

```
We need to add all the numbers that have the 1's. So 0+64+32+16+8+4+2+1=127
So our IP is: **192.168.2.127**

Our Host range is all the numbers in-between: **192.168.2.64 - 192.168.2.126**

So our final answers:
1. 192.168.2.64
2. 192.168.2.127
3. 192.168.2.64 - 192.168.2.126


# CIDR

CIDR stands for classless inter-domain routing. CIDR is used for simplifying subnetmask in a more compact way. You often can see subnets noted in CIDR. For example: 192.168.1.0/255.255.255.0 is written as 192.168.1.0/24

Remember that IP addresses are 4 bytes or 32 bits? CIDR shows how many bits are used in the prefix. So 192.168.1.0/24 means there are 24 bits used. This shows us how many hosts are there. You simply have to subtract the IP addresses by the max amount. (32) and the CIDR Address (24), so that's 8 bits. So 2^8=256, but we have to remove 2 address (broadcast and network address) so we have a total of 254 addresses to be used as hosts.

# NAT

NAT stands for Network Address Translation. NAT makes a device like our router and acts as a link between the Internet and Private network. This makes it so a single unique IP is required to represent your entire group of computers.

Basically NAT helps your entire network use one public IP address. (Which you can google and see it).














[< Back: Basic DHCP](https://github.com/sxcdennis/Network/blob/master/Basic%20DHCP.md "Basic DHCP") || [Next: Basic Routing >](https://github.com/sxcdennis/Network/blob/master/Basic%20Routing.md "Basic Routing")
