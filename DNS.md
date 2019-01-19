# DNS

Domain Name System allows us humans to keep track of websites and hosts by name instead of an IP address. For example, instead of google.com you would have to type 172.217.10.46 every time.

DNS is just basically a distributed database of hostnames to IP addresses. Each domain aare able to talk to each other and build massive contact lists of the internet.


# DNS Components

The DNS database of the Internet relies on sites and organizations providing part of that database. In order to do that they need- Name Servers, Zone Files and Resource Records.

**Name Server**

We set up DNS via name servers. The name servers load up our DNS settings and configs and answer any questions from clients or other servers that want to  know things like "Who is google.com". If the nameserver doesn't have an answer to the question, it will redirect the request to other name servers. Name servers can be "authoriaative" meaning they have real DNS records that you're looking for. Recursive means they would ask servers and those servers would ask other servers until they find an authoritive server that contains DNS records. Recursive servers can also have information cached instead of reaching authoritive servers.

**Zone Files**

Inside a name server lives something called zone files. Zone files are how name servers store information about the domain or how to get the domain if it doesn't know.


**Resource Records**
A zone file is made of entries of resource records. Each line is a record and contains information about hosts, nameservers, and more.

The fields of resource records contain:

Record name

TTL - The time after which we discard the record and obtain a new one, in DNS TTL is denoted by time, so records could have a TTL of one hour. The reason we do this is because the Internet is constantly changing, one minute a host can be mapped to X IP address then next it can be at Y IP address

Class - Namespace of the record information, most commonly IN is used for Internet

Type - Type of information stored in the record data. We won't get into record types, but you've probably seen common ones like A for address, MX or mail exchanger, etc.

Data - This field can contain an IP address if it's an A record or something else depending on the record type.



# DNS Process

In order to find domains there needs to be a process. It starts with Local DNS servers, root servers, top level domains , and then authrotiavie DNS servers.

Lets use coolstuff.com as an example

**Local DNS Server**

First our hosts asks Where is coolstuff.com?, our local DNS server doens't know so it goes start from the top of the funnel and asks the Root servers.

**Root Servers**

There are 13 Root Servers for the Internet, they are mirrored and distributed across the globe to handle DNS requests for the internet. There are hundreds of servers hat are working and controlled by different organizations and they contain informations about Top-Level Domains. Top-leveled doamins are known as .com,.org,.net etc.. So Root Server does't know where coolstuff.com is so it tells us that .com is Top-Level Domain DNS server at an IP address given to us.


**Top-Level Domain**

So now we send another request to the name server that knows about .com to ask where coolstuff.com is.  The TLD doesn't have coolstuff.com in their zone files, but does see a record for the nameserver of coolstuff.com. It then gives us the IP address of that name server and tells us to look there.

**Authoritative DNS Server**

Now we send final request to the DNS server that actually has the record we want. The name server see thats it has a zone file for coolstuff.com and there's a resource record for 'www' for this host. It then gives us the IP address of this host so we can finally see some calls on the Internet.c




# /etc/hosts


Typically you would see your lcoalhost and ip address in this file. If you change the host name it could cause some issues. For example if you changed your host to www.google.com it never reaches the DNS because the address is wrong.

**/etc/resolv.conf**

/etc/resolv.conf has been traditionally edited, but now people don't use it. Infact it even states to not edit because the changes will be overwirtten.

# DNS Setup

We won't go through the whole DNS server installation but we'll list some popular DNS servers to use with Linux.

**BIND**

The most popular DNS for the internet is bind. It's the standard used for Linux. BIND stands for Berkeley Internet Name Domain.


**DNSmasq**

DNSmasq is lightweight and easier to configure than BIND. It works well for small networks.



**PowerDNS**

Full-Featured and similar to BIND, it offers you a little more flexibility with options. It reads information from datbases such as SQL.

# DNS Tools

**nslookup**

The "Name Server Lookup" tool is used to see nameservers information and records.

Example:

![nslookup](https://raw.githubusercontent.com/sxcdennis/Network/master/images/nslookup.png)


**dig**
Domain information groper is a powerful tool that can also get information on DNS. This tool gives more information than nslookup.

![dig](https://raw.githubusercontent.com/sxcdennis/Network/master/images/dig.png)

[< Back: Basic Troubleshooting Tools](https://github.com/sxcdennis/Network/blob/master/Basic%20Trouble%20Shooting%20Tools.md "Basic Troubleshooting Tools") || [Next: SSH >](https://github.com/sxcdennis/Network/blob/master/SSH.md "SSH")
