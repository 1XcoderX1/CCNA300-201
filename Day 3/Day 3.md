# OSI Model & TCP/IP Suite
## What is a networking model?
Networkling models categorize and provide structure for networking protocols and standards.

![[networking_model.png]]

## Protocol
A set of rules defining how network devices and software should work.
Not physical standards; only lofical rules.

## Networks without Standardization
If we have a cluster of PCs from various makers, if there is no tandardization for communication then they won't be able to communicate with each other.

## OSI Model
* `Open Systems Interconnection` model
* A conceptual model that categorizes and standardizes the different functions in a network
* Created by the `International Organization for Standardization` (ISO)
* Functions are divided into 7 `Layers`
* These layers work together to make the network work

![[OSI_model.png]]

### Upper Layers (Host Layers) 
It is important to know the function of the three layers mentioned below. But, network engineers don't really work with the top 3 layers. 
* Application developers work with the top layers of the OSI model to connect their applications over networks

#### Application Layer (7)
* This layer is closest to the end user
* Interacts with spftware applications, for e.g., your web browser (Brave, Firefox, Chrome, etc)
* HTTP and HTTPS are Layer 7 protocols
* Keep in mind that layer 7 does not include the browser itself, but just the protocols they use.

Functions of Layer 7 include:
* Identifying communication partners
* Synchronizing communication

In the infographic below, there are 2 OSI model stacks  represening 2 computers which will communicate with each other. The browser on the application laeyer on blue side wants to send some data to the aplication layer on the green system. 

![[application_layer_infographic.png]]

This data is processed through th OSI stack, each layer adding something to the data. This is called **Encapsulation** because the original data is encapsulated inside this extra information added by each layer.  By the time it reaches the physical layer, it is electrical signals on a wire and is sent to the green system. Then, the green system performs the opposite process, where additional information is stripped off from the oiriginal data. This process is called **De-encapsulation**, as the additional data is stripped off by the layers in the OSI stack.

Both encapsulation and de-encapsulation are examples of *adjacet-layer interaction*, which is interaction between the differetnt layers of the OSI model. However, the communication betweenm the two same layers of two different OSI stacks is called *Same-layer interaction*. This same layer interaction enables the application layers to perform its functions of identifying communication partners, synhcronising communications, etc.

### Presentation Layer (6)
* Data in the apllication layer is in *application format*
* It needs to be *translated* to a different format to be sent over the network
* The **Presentation** Layer's job is to translate between application and nework formats
* For example, encryption of data as it is sent, and decryption of data as it is received
* Also translates between different Application-Layer formats

### Session Layer (5)
* Controls dialogues (sessions) between communicating hosts
* Establishes, manages, and terminates connections between the local application (for e.g., your web browser) and the remote application (for e.g., YouTube)

After these 3 layers process the data, i.e., after the data is encapsulated in these 3 layers, the next layer, the *transport layer* adds a header to the data. 

![[L4header.png]]

### Transport Layer (4)
* Segments and reassembles data for communications between end hosts
* Breaks large pieces of data into smaller segments which can be more easily sent over the network and are less likely to cause transmission problems if errors occur
* For e.g., if a video is sent as one whole piece of data and an error prevents it from reaching the destination, the whole video would be gone. But, if it is segmented into small pieces, then if a piece is lost, the video might skip a little and then run smoothly again.
* Provide **host-to-host** communication.

To review until now, the data is prepared by the top 3 layers, a layer 4 header is added on. Note that at this point in the process, this unit of data plus the L4 header is called a **segment**. Remember, that if the data being sent is large enough, the data will be segmented into various smaller segments and each segment will have its own header. Next, that segment is sent to Layer 3 and another data header is added to it.

![[L3header.png]]

### Network Layer (3)
* Provides connectivity between end hosts on different networks (i.e. outside of LAN)
* Provides logical addressing (IP addresses)
* Provides path selection between source and destination
* Routers operate at Level 3

When the L3 header is added to the data segment, it is called a packet. Next, the data is further encapsulated at Layer 2, this time with both a layer 2 header and a layer 2 trailer.

![[L2_infographic.png]]

### Data Link Layer (2)
* Provides node-to-node connectivity and data transfer (for example, PC to switch, switch to router, router to router)
* Defines how data is formatted for transmissionover a physical medium (for example, copper UTP cables)
* Detects and (possibly) corrects Physical Layer errors
* Uses Layer 2 addressing, separate from Layer 3 addressing
* Switches operate at Layer 2

After a data packet gets encapsulated by Layer 2, it is called a **frame**. Now, the data is not further encapsulated at Layer 1. This frame is then sent over the connection, whether it is electrical signals over a cable, or wireless signales in the case of Wi-Fi to the neighbouring systems. Layer 1 is explained here:

### Physical Layer (1)
* Defines physcial caharacteristics of the medoum used to transfer data between devices
* For exmaple, voltage levels, maximum transmission distances, physical connectors, cable specifications, etc.
* Digital bits are converted into electrical (for wired connections) or radio (for wireless connections) signals

After the data frame reaches the other device, it is de-encapsulated to retreive the original data. This is done by sending the data frame through Layers 1 to 7 on the destination device.

![[data_transfer.gif]]

The data goes through a transformation from Layer 7 to Layer 1 while being encapsulated. The terms used for the data change over this encapsulation process. These terms are collectively called **Protocol Data Units** (PDUs). For example, a segment is a term for a Layer 4 PDU, packet is a term for a Layer 3 PDU, etc. At Layer 1, the name for the PDU is **Bit**.

![[PDUs.png]]

Here are a few acronyms to remember the data layers:

* **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing (Layer 7 to Layer 1)
* **P**lease **D**o **N**ot **T**each **P**eople **A**cronyms (Layer 1 to Layer 7)

* Conceptual model and set of communcations protocols used in the Internet and other networks
* Known as TCP/IP because those are two of the foundational protocols in the suite
* Developed by the United States Department of Defense through DARPA (Defense advanced Research Projects Agency)
* Similar structure to the OSI model, but with fewer layers
* This is the model actually in use in modern networks

## OSI vs TCP/IP

![[OSI_vs_TCPIP.png]]

Whenever people talk about the layers, they are usually talking about the layers in the OSI model. Even if we do use TCP/IP Suite in modern networks, we mostly refer to the layers in the OSI model when talking about networks.

The diagram below demonstrates the process of a host, Host A sendind data to Host B with two routers in between.

![[TCP_infographic.png]]



#day