# Ethernet LAN Switching (Part 1)
Let us review the Physical and Data Link layers of the OSI Model:

[[OSI Model Layers#Physical Layer 1 | Physical Layer]]
[[OSI Model Layers#Data Link Layer 2 | Data Link Layer]]

In this session we are going to look at ethernet LAN switching, which involves the Physical & Data Link laters of the OSI model. Since we have already talked about various Layer 1 standards such as UTP cables, we should focus more on Layer 2.

## Local Area Network (LANs)

![[LAN_graphic.png]]

There are different ways of defining a LAN. Basically, it is a network covering a small area like an office floor or a home network. Routers are used to connect separate LANs. In the above diagram there are 3 diffferent LANs connecnted to each other via routers and tne Internet. In the red LAN, there are two switches in the network. Remember, switches do not separate LANs, they are parts of the same network. On the contrary, in the blue network, two switches are NOT connected to each other but connect directly to a router, so they are 2 different LANs. 

![[LAN_graphic1.png]]

In this session, we will look at how the network works in different LANs. We will leave the networking between two separate LANs for later.

Let us review the OSI Model PDUs once again as we will need them for this *segment*:

![[PDUs.png]]

We are going to focus on how switches receive and forward Frames, specifically ethernet frames as they are virtually used in every LAN existing today. 

## Ethernet Frame
### Ethernet Header
![[ethernet_Frame.png]]

The header has 5 fields:
* Preamble & Start Frame Delimiter (SFD)
	These are used for syncronization which tells the device to prepare for the rest of the fields.
	#### Preamble:
	* Length: It is 7 bytes long
	* Alternating 1's and 0's
	* 10101010 * 7
	* Allows devices to synchronize their receiver clocks
	#### SFD
	* 'Start Frame Delimiter'
	* Length: 1 byte (8 bits)
	* 10101101
	* Marks the end of the preamble, and the beginning of the rest of the frame
* Destination & Source
	* Indicate the devices sending and receiving the frame
	* Consist of the destination and source 'MAC address'
	* MAC = Media Access Control
	* = 6 byte (48 bit) address of the physical device
* Type or Length
	It indicates the Layer 3 protocol used in the Packet, which is always IPv4 or IPv6. Sometimes can be length field, indicating the length of the ethernet data.
	* 2 byte (16 bits) field
	* A value of 1500 or less in this field indicatesthe LENGTH of the encapsulated packet (in bytes)
	* A value of 1536 or greater in this field indicates the TYPE of the encapsulated packet (usually Pv4 or IPv6), and the length is determined via other methods
	* For e.g., IPv4 = 0x0800 (hexadecimal) = 2048 in decimal > 1536, so packet is IPv4

### Ethernet Trailer
The trailer has only 1 field:
* Frame Check Sequence (FCS)
	It is used by the receiving device to detect if any errors have occured during transmission.
	* 4 bytes (32 bits) in length
	* Detects corrupted data by a 'CRC' algorithm over the received data
	* CRC = 'Cyclic Redundancy Check'

Try to remember the lengths of each field:

![[eth_frame_header_length.png]]

= 26 bytes (header + trailer)

## MAC Address
* 6-byte (48 bit) physical address assigned to the device when it is made
* A.K.A. 'Burned-In Address' (BIA)
* Is globally unique
* The first 3 bytes are the OUI (Organizationally Unique Identifier), which is assigned to the company making the device
* The last 3 bytes are unique to the device itself
* Written as 12 hexadecimal characters

If you would like to learn about hexadecimal, please go here: [[Decimals & Hexadecimals]]

![[MAC1.png]]

In the diagram there are 3 PCs connected to a switch. Each PC has a MAC Address with 12 characters. The first part of the MAC address (the first 4 characters), is the OUI. As it is the same for all 3 PCs, they are manufactured by the same manufacturer.
The rest of the 8 characters identify the device itself. 
Let us suppose that PC1 wants to send some data to PC2, this kind of frame which is destined for a single target is called a **Unicast** frame.
PC1 sends the frame thorugh its NIC which is connected to the Switch SW1. After SW1 receives the frame, it notes the source MAC address in the packet and adds it to its MAC Address table. 

![[MACTable1.png]]

This is called a dynamic MAC Address as the switch learned it on  the go and it was not added to it while it was set up. Every switch cerates a MAC address table like this and it adds addresses to it by this process. This is a very important concept. This is how they learn where each device in the network is.

But now, the switch does not know where PC2 is, this kind of frame is called a **Unknown Unicast** Frame.
A frame for which the switch does not know how tho reach the destination. So the switch has only one way to send the frame, that is to **FLOOD** thr frame. This means it will send the packet down every port except the one from where it received the frame. it copies the frame and sends it to FO/2 and FO/3 interfaces. 

PC3 receives and drops the frame because the destination does not match its MAC Address. PC2 receives the frame and processes it up its OSI stack  to decode the data. However, unless PC2 sends a frame back to PC1, the switch never learns where PC2 is.

Lets say that PC1 sends another packet to PC2. This time the switch already knows the MAC of PC1, so it does not store it again. But, it still does not know where PC2 is, so it once again floods the frame.  Now, lets say that PC2 wants to send a reply to PC1. It sends the frame out of its NIC and to the switch. The switch reads the source MAC and adds it to its MAC Address Table associating it with interface F0/2.

![[MAC2.png]]

However, this time the switch knows the destination and it forwards this frame to interface F0/1 so that it can reach PC1, this type of frame is called as a **Known Unicast** frame as the switch knows how to reach the destination. PC1 processes the frame up the OSI stack. 

On Cisco switches, MAC addresses are removed after 5 minutes of inactivity. 

Let us look at another example with 2 switches this time:

![[MAC3.png]]

Notice the MAC address tables of the switches, they are empty. So, PC1 wants to send some data to PC3. It sends it to switch 1. SW1, learns the address of PC1. But it has no idea where PC3 is, so it floods the network. PC2 drops the frame. Switch 2 add the source address with its F0/3 interface in its MAC address table. Then it floods its ports as well. PC3 receives the frame an runs it up its OSI stack. This is how the MAC tables look like after this transaction:

![[MAC4.png]]

Now, let us say PC3 wants to reply back to PC1. It sends the frame to SW2. SW2 learns PC3's MAC address and adds it to its table. Then it sends the fram down FO/3 as it knows the address already. At SW1, the source address is added to SW1's table and then it forwards the frame to PC1 as it knows which port is is connected because of the last transaction. The frame reaches PC1 and is decoded by it. 












#day 