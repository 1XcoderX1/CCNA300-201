## Application Layer (7)
* This layer is closest to the end user
* Interacts with spftware applications, for e.g., your web browser (Brave, Firefox, Chrome, etc)
* HTTP and HTTPS are Layer 7 protocols
* Keep in mind that layer 7 does not include the browser itself, but just the protocols they use.

### Functions of Layer 7 include:
* Identifying communication partners
* Synchronizing communication

In the infographic below, there are 2 OSI model stacks  represening 2 computers which will communicate with each other. The browser on the application laeyer on blue side wants to send some data to the aplication layer on the green system. 

![[application_layer_infographic.png]]

This data is processed through th OSI stack, each layer adding something to the data. This is called **Encapsulation** because the original data is encapsulated inside this extra information added by each layer.  By the time it reaches the physical layer, it is electrical signals on a wire and is sent to the green system. Then, the green system performs the opposite process, where additional information is stripped off from the oiriginal data. This process is called **De-encapsulation**, as the additional data is stripped off by the layers in the OSI stack.

Both encapsulation and de-encapsulation are examples of *adjacet-layer interaction*, which is interaction between the differetnt layers of the OSI model. However, the communication betweenm the two same layers of two different OSI stacks is called *Same-layer interaction*. This same layer interaction enables the application layers to perform its functions of identifying communication partners, synhcronising communications, etc.

## Presentation Layer (6)
* Data in the apllication layer is in *application format*
* It needs to be *translated* to a different format to be sent over the network
* The **Presentation** Layer's job is to translate between application and nework formats
* For example, encryption of data as it is sent, and decryption of data as it is received
* Also translates between different Application-Layer formats

## Session Layer (5)
* Controls dialogues (sessions) between communicating hosts
* Establishes, manages, and terminates connections between the local application (for e.g., your web browser) and the remote application (for e.g., YouTube)

## Transport Layer (4)
* Segments and reassembles data for communications between end hosts
* Breaks large pieces of data into smaller segments which can be more easily sent over the network and are less likely to cause transmission problems if errors occur
* For e.g., if a video is sent as one whole piece of data and an error prevents it from reaching the destination, the whole video would be gone. But, if it is segmented into small pieces, then if a piece is lost, the video might skip a little and then run smoothly again.
* Provide **host-to-host** communication.

## Network Layer (3)
* Provides connectivity between end hosts on different networks (i.e. outside of LAN)
* Provides logical addressing (IP addresses)
* Provides path selection between source and destination
* Routers operate at Level 3

## Data Link Layer (2)
* Provides node-to-node connectivity and data transfer (for example, PC to switch, switch to router, router to router)
* Defines how data is formatted for transmissionover a physical medium (for example, copper UTP cables)
* Detects and (possibly) corrects Physical Layer errors
* Uses Layer 2 addressing, separate from Layer 3 addressing
* Switches operate at Layer 2

## Physical Layer (1)
* Defines physcial caharacteristics of the medoum used to transfer data between devices
* For exmaple, voltage levels, maximum transmission distances, physical connectors, cable specifications, etc.
* Digital bits are converted into electrical (for wired connections) or radio (for wireless connections) signals