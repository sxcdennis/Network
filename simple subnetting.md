# Simple subnetting

Subnet is a subnetwork. There can be several subnetworks within an entire network. For subnetworks to talk to each other you need a router.
To calculate a subnetwork IP you need to know a few things: Subnet Mask, Converting Binary to Decimal, and Converting Decimal to Binary.  Typical things to know in a subnetwork is - Network address (The first IP), Broadcast Address(The Last IP), and Range (The IP's between Network and Broadcast)

# Subnetmask

A subnet mask is basically a binary number that helps find out your Network Address, Broadcast Address and Range of your subnet.
There are two ways to see a subnet mask number:

Example 1:

```

192.168.1.101/24

```
This means the subnetmask is 24 1's and 8 0's

**11111111.11111111.11111111.00000000**

Example 2:
You can see the entire binary by itself:

**11111111.11111111.11111111.11000000**

You use this binary number later to find your Network Address and Broadcast Address by covering up/masking their IP. Will discuss later.


# Converting Binary To Decimal

To convert Binary to Decimal- we use a method by using 2^0 to 2^7

```

128 64 32 16 8 4 2 1

```
Each number from 128-1 is a spot. Each spot is then added depending on your binary 1's and 0's. Your 0's will not add anything.

For example- Lets say your binary number is 11001111
You will have to add: 128+64+0+0+8+4+2+1 = 208 = Your Decimal number.


# Converting Decimal to Binary

To convert the Decimal to Binary - we also use a method by using  the 2^0 to 2^7

```

128 64 32 16 8 4 2 1

```

To convert this, you need to subtract the Decimal number from left to right and keep using the remaining numbers from left to right until you get 0. If you subtract successfully without getting a negative number it will count that number as a 1. If you subtract and get a negative number it will count as a 0. If you reach 0 before getting to the 8th spot, the remaining binary numbers are 0. To get your final binary number you put your 1's and 0's from 1-8 together.

Example if your decimal number is 18:

1. 18-128=NEG : 0
2. 18- 64= NEG : 0
3. 18- 32= NEG : 0
4. 18- 16 = 2 : 1
5. 2 - 8 = NEG : 0
6. 2 - 4= NEG  : 0
7. 2 - 2 = 0 : 1
8. 0

So your Binary number is 00010010


# Example

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
3. 192.168.2.65 - 192.168.2.126

# Easy Subnetting

Now that we know the normal way to do subnetting lets learn the easy way.
We now have to use a new table

```

128|192|224|240|248|252|254|255
8|16|24

```


Here's the formulas

```
256 - NetMaskNum= MagicNum

OrignalIP/MagicNum= NewNum(rounded down)

NewNum x MagicNum=NetAddr

BroadcastID= (NetAddr + MagicNum) - 1

```

Now you might be wondering how to use these. I'll give a few examples:

In the following examples find the:
1. Subnet Mask
2. Network Address
3. Broadcast Address
4. Range  

**Example 1**

You are given the following IP Address:

IP Address: **180. 126. 108. 234/ 30**

1. To find the subnet mask we use the 1st chart

```

128|192|224|240|248|252|254|255

8|16|24

```

Take the 2nd row number and see which one is closest to *30*. Which is 24.

Subtract 30 from 24. ( 30-24=6 )
Use the remainder number on the top row from left to right ( 252 ).
That is our number.
So we know that we had to use 3 255's because we used the *24* (each number on the 2nd row represents an octet)

NetmaskNum= 252
So our subnet mask = 255.255.255.252

Next we use the forumla:

256- NetMaskNum= MagicNum
256 -252 = 4

OriginalIP/MagicNum= New Num (rouned down)
So we know the first 3 otects are masked.
That means 234 is our Orignal  IP
234/4=58.5(rounded down)= 58


NewNum x MagicNum=NetAddr
58 x 4 =232
Now we know our Network address
180.126.108.232

BroadcastID= (NetAddr + MagicNum) - 1
( 232 + 4 ) - 1= 235
Now we know our Broadcastaddress
180.126.108.235

Range = Network Address - Last Number

180.126.108.232-180.126.108.234

1. Subnet Mask : 255.255.255.252
2. Network Address: 180.126.108.232
3. Broadcast Address: 180.126.108.235
4. Range: 180.126.108.232-180.126.108.234

**Example 2**

IP Address: 170.232.1.73/24



```

128|192|224|240|248|252|254|255
8|16|24

```

So in this example if it hits either 8/16/24 we don't need to use the forumlas since it's easy to remember.
Network Mask would be 255.255.255.0
Network Address would be: 170.232.1.0 (since first 3 otects are masked)
Broadcast Address= 170.232.1.255
Range= 170.232.1.0-170.232.1.255


**Example 3**

IP ADDRESS: 43.180.18.231/22

```

128|192|224|240|248|252|254|255
8|16|24

```
First finding the subnetmask we use the 2nd row.
22-16= 6
252 is our NetmaskNum
255.255.252.0 is our Netmask


256 - NetMaskNum= MagicNum
256-252=4

OrignalIP/MagicNum= NewNum(rounded down)
18/4=4.5(roundeddown)=4

NewNum x MagicNum=NetAddr
NetADDR= 4 x 4 =16
NetAddress43.180.16.0

BroadcastID= (NetAddr + MagicNum) - 1
(16 + 4)- 1= 19
Broadcast Address: 43.180.19.255

1. Subnet Mask: 255.255.252.0
2. Network Address: 43.180.16.0
3. Broadcast Address: 43.180.19.255
4. Range: 43.180.16.0-43.180.19.255
