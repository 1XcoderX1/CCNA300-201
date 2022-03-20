# Ethernet LAN Switching (Part 2)
We will continue talking about sendibng data locally. 
We talked about [[Day 5#Ethernet Frame | ethernet frames]] in the last session.

![[eth_frame_header_length.png]]

* The Preamble + SFD is not usually not considered part of the Ethernet header. Therefore the size of the Ethernet header + trailer is 18 bytes (6+6+2+4). 
* There is also a minimum size for the Ethernet frame (Header + Payload [Packet] + Trailer), 64 bytes.
* 64 bytes - 18 bytes (header + trailer size) = 46 bytes
* Therefore the minimum payload [Packet] size is 46 bytes
* If it is smaller than 46 bytes, padding bytes (0s) are added, e.g., 34 byte packet + 12 byte padding = 46 bytes.

Going back to the network we had in the last session, this time we are gonna use the same one but with some key changes:

* The interfaces have been changed from fast ethernet to gigabit ethernet
* The MAC addresses are more realistic than the ones used in the last session
* Notice that the OUI is same again for all PCs, so they are made by the same manufacturer

![[ethernet_LAN_switching_network2.png]]
 
Now, lets add another thing to this network topology, IP addresses. We will need them to explain other stuff in this session.

![[ethernet_LAN_switching_network2_IP.png]]

When a device sends some data to another device, it does not just include the source and destination MAC address. Encapsulated within the data frame is another protocol called the IP packet and that packet contains the source and destination IP addresses. 
When the device sends data to another device, it sends the data to a specific IP address, which it knows already. But, the device has to discover the MAC address of the destination PC itself. Remember, the switches are Layer 2 devices, so they need to use MAC addresses and not IP addresses. 
So, if PC1 wants to send data to PC3 then it needs to learn PC3s MAC address. For this, it uses something called **ARP (Address Resolution Protocol**.

## ARP (Address Resolution Protocol)
* Used to discover the Layer 2 (MAC) address of a known Layer 3 (IP) address
* Consists of two messages:
	* ARP request
	* ARP reply
* ARP request is broadcast  = sent to all hosts on the network
* ARP reply is unicast = sent to only one host (the host that sent the ARP request)

### ARP Request

![[ARP_request.png]]

When an ARP request is sent out of PC1, it follows the same route as the unicast dataframe we talked about in the last session. Along the way, switches learn the MAC address of PC1 dynamically. When the ARP request reaches PC3, it recognises that the destination IP address matches its own IP, so it replies with an ARP reply packet.

### ARP Reply

![[ARP_reply.png]]

PC3 knows the MAC address of PC1 so it can send it directly to it without broadcasting it. Along the way, switches learn PC3s MAC address. After the packet reaches PC1, it adds the entry for PC3 in its ARP Data table, which associates its IP with a MAC address.

### ARP Table
![[ARP_table.png]]

* Use arp -a to view the ARP table (Windows, MAC, Linux)
* Internet Address = IP Address (Layer 3 Address)
* Physical Address = MAC Address (Layer 2 Address)
* Type static = default entry
* Type dynamic = learned via ARP

## MAC Address tables on Switches
Let us take a look at the MAC address tables which are kept on switches. Here is the network topology we have in a network emulator software, GNS3. GNS3 is similar to the Cisco packet tracer, but it is different in some ways. Packet tracer is a network simulator, while GNS3 runs actual cisco ios software, so these are real cisco switches running virtually. But, the purchase of Ciso IOS is required to use it with GNS3.

![[GNS3_ethernetSwitching2.png]]

![[GNS3_ethernetSwitching2_1.png]]

Notice the magnifying glass in the picture above. GNS3 can be used with wireshark to analyze the traffic between any two components in the network. Here, lets see what traffic is sent between PC1 and SW1, when a ping is sent from PC1 to PC3. We have the same scenario as discussed earlier.

### Ping
* A network utility that is used to test reachability
* Measures round-trip time
* Uses two messages:
	* ICMP echo request
	* ICMP echo reply
* ICMP requets is not broadcast, but sent to a specific address. So ARP is run before ping to locate the PC the ping is to be sent to
* command: `ping (ip-address)`

![[ping_1.png]]
 Ping from PC1 to PC3. 
 By default the ping command sends 5 ICMP echos each a 100-byte long. The period indicates a failed ping and the exclamation marks indicate a successful ping. As it says here, success here is 80%. It also shows the round-trip time. Now, why did the forst ping fail? That is because of ARP. When the first ping was sent PC1 did not know the address of PC1, so it failed. But by the time the second ICMP echo request was sent ARP was already sent and received, so all ICMP request after the first succeeded.

In the Cisco ios, the arp command is `show arp` from privileged EXEC mode. 

![[Arp_ciscoios.png]]

Below is a screenshot from wireshar of the oing requests:

![[ARP_wireshark.png]]

Notice the ARP request sent from the MAC address of PC1. The ARP requests resolve the MAC address of PC3. All ICMP requests have the IP address of PC1 and PC3. 

Now finally, let us take a look at the MAC address table on a Ciso switch:

![[MAC_table_SW1.png]]

The command to view it is `show mac address-table`, old versions of cisco ios use `show mac -address-table`.

* VLAN: Virtual area network, the default is 1
* MAC Address: MAC addresses of know devices
* Type: Dynamic or static
* Ports: On what ports are the devices

We know that dynamic MAC addresses are deleted from the table after 5 inutes of inactivity. This is known as **ageing**. We can also manually remove these addresses with 
`clear mac address-table dynamic`. 
We can also select individual addresses like this: 
`clear mac address-table dynamic address MACADDRESS`. 
Can also use:
`clear mac adderss-table dynamic interface INTERFACENAME`.



































#day 