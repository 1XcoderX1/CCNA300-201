# IPv4 Addressing (Part 1)
We should start exploring out of LANs and see how traffic is between two LANs connected via routers and the Internet. We are going to look into Layer 3 for the same. Let's review some characteristics of Layer 3: 

* Provides connectivity between end hosts on different networks (i.e., outside of the LAN)
* Provides logical addressing (IP addresses)
* Provides path selection between source and destination
* Routers operate at Layer 3

We will talk more about logical addressing in this session. 

## Routing
In the diagram below two switches are connected to each other which have 2 computers each connected to them. Remember, switches do not separate the network, they connect devices to each other. If we add two more switches to this diagram, then they will connect the devices connected to them to the other switches, but not separate them. That is why, all devices in this network have IP addresses in the same Layer 3 network - 192.168.1.0/24.

![[routing.png]]

Now, what would happen if a router is put between SW1 and SW2?

![[routing1.png]]

This separates the network into 2 separate networks. PC1 and PC2 are their own IP address classification now which is different from PC3 and PC4, which are on the other side of the router. We can see that the first 3 groups of numbers in the IP address represent the network itself and only the last group changes to represent host devices. The 24 at the end is telling us about which part of the IP address is to be used to represent the network. '24' means the first 3 groups are representing the network and the last is being used for the end host devices. Before we dive deep into the details of IP addresses, there is something missing from this network diagram. An IP address for the router. As it is connected to 2 LANs, it should get an IP address for each LAN:

![[routing2.png]]

Now if PC1 sends a broadcast packet, it will reach PC2 and the router, but will not go firther than the router as the local network ends there. We will look into routing and layer forwarding in later sessions. 

## IPv4 Header
IP or Internet Protocol is the primary Layer 3 protocol in use today. And version 4 is the one used in most networks. We can see in the diagram below that the IPv4 header has way more fields than the ethernet header. We will look into the details of this header in another session. For now, let's focus on these two fields: 
* Source IP Address
* Destination IP Address
They both are 32 bits in length. So, IP addresses are 32 bits or 4 bytes in length. 

![[ipv4.png]]

## IPv4 Addresses
Let's look at this IP address: 192.168.1.254
An IP Address is 32 bits long. So, each of these groups is 8 bits long. The binary form of the IP address can be written as follows:

![[192.168.1.254.png]]

As the binary way of representing numbers is quite difficult for humans, we use the dotted decimal system to identify IP Addresses. There was also the /24 which tells us that the first 24 bits represent the network address and the rest 8 bits represent the end host device addresses.

![[routing3.png]]

For e.g., in the IP Address **154.78.111.32/16**, the first two groups represent the network portion and the last 2 groups represent the host portion. 

## IPv4 Address Classes
IPv4 addresses are classified into 5 different classes. The class of an IP address is determined by the first octet of the IP address:

![[IPv4Classes.png]]

### Class A
If the first octet of an IP address starts with a 0, then it belongs in Class A. This means the numeric range of the first octet ranges from 0-127. 

### Class B
If the first octet of an IP address starts with a 10, then it belongs in Class B. This means the numeric range of the first octet ranges from 128-191.

### Class C
If the first octet of an IP address starts with a 110, then it belongs in Class C. This means the numeric range of the first octet ranges from 192-223.

### Class D
If the first octet of an IP address starts with a 1110, then it belongs in Class D. This means the numeric range of the first octet ranges from 224-239.

### Class E
If the first octet of an IP address starts with a 1111, then it belongs in Class E. This means the numeric range of the first octet ranges from 240-255.

Class D addresses are reserved for multicast addresses and Class E addresses are reserved for experimental purposes. 

Let's look into details of Class A, Class B and Class C addresses. 

### Loopback Addresses: 
The end of the Class A range is usually considered to be 126 instead of 127. The 127 range is reserved for **Loopback Addresses**. 
* Address Range: 127.0.0.0 - 127.255.255.255
* Used to test the 'network stack' (think OSI, TCP/IP model) on the local device

![[127.0.0.0pingTest.png]]
The PC is simply pinging itself, that is why the round trip time is 0ms. 

### Classes A, B & C details
![[IPv4ABC.png]]

In Class A as only the first octet is used to represent the network, there are very few networks in this class. However, as the end hosts have 3 whole octets to be represented with, there can be a lot of end hosts in a single Class A network.
Class C is opposite, as there can be a lot of different networks, but the end hosts are limited to a few only. Let's take a look at the numbers:

![[IPv4classdetails.png]]

The leading bits column represents the first bit of the first first octet of the IP address. The 'Size of network number bit field' shows us how many bits represent the number of bits used to represent the networks that can exist in the class. The 'Size of rest bit field' indicates the remaining bits in the address, which is the host bit of the address. The 'Number of networks' column represents the number of networks which can exist in each class and 'Addresses per network' column shows the number of hosts each netwprk can have. As mentioned before, Class A can only have a few networks, but more hosts in the each network. Class C is the opposite. Class B sits in the middle.
However, in each network, one address is the network address, it cannot be assigned to hosts. Also the last address in a network is the broadcast address, the Layer 3 address used to send data to all hosts, so it cannot be used as a host address as well. 
There is another way of writing the prefix lengths, i.e., /8, /16, /24 etc.

## Netmask
The slash notation is a new way of writing prefixes. Cisco devices still use an older way of writing these, that is a **Dotted decimal Netmask**. This is how we can convert the dash notation to the netmask notation: 

Class A -> /8 -> 255.0.0.0
Class B -> /16 -> 255.255.0.0
Class C -> /24 -> 255.255.255.0

These are essentially the same binary numbers written in different ways to make the human brain make sense of them.

## Network Address
If the host portion of the address is all 0s, then it is the **Network Address**. E.g., 192.168.1.0/24 is a network address. This address cannot be assigned to a host. It is always the first address in a network. But the first *usable* address is one up the network address. In this case its, 192.168.1.1.

## Broadcast Address
If the host portion of the address is all 1s, then it is the **Broadcast Address**. E.g., 192.168.1.255/24 is a broadcast address. This address also cannot be assigned to a host. Although it is the last address in the network, the last *usable* address in the network is one before the broadcast address. This address is used to send a broadcast packet to all hosts in the network. So, if the destination IP of the packet is set to 192.168.1.255 then what do you think the MAC address would be of the encapsulated frame?  It will be FFFF.FFFF.FFFF. 










#day 