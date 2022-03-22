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

This separates the network into 2 separate networks. PC1 and PC2 ave their own IP address calssification now which is different from PC3 and PC4, which are on the other side of the router. We can see that the first 3 groups of numbers in the IP address represent the network itself and only the last group changes to represent host devices. The 24 at the end is telling us about which part of the IP address is to be used to represent the network. '24' means the first 3 groups are representing the network and the last is being used for the end host devices. Before we dive deep into the details of IP addresses, there is something missing from this network diagram. An IP address for the router. As it is connected to 2 LANs, it should get an IP address for each LAN:

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

As the binary way of representing numbers is quite difficult for humans, we use the dotted decimal system to identify IP Addresses. 