# OSI Model

* `Open Systems Interconnection` model
* A conceptual model that categorizes and standardizes the different functions in a network
* Created by the `International Organization for Standardization` (ISO)
* Functions are divided into 7 `Layers`
* These layers work together to make the network work

![[OSI_model.png]]

## Upper Layers (Host Layers) 
It is important to know the function of the three layers mentioned below. But, network engineers don't really work with the top 3 layers. 
* Application developers work with the top layers of the OSI model to connect their applications over networks

### [[OSI Model Layers#Application Layer]]
### [[OSI Model Layers#Presentation Layer]]
### [[OSI Model Layers#Session Layer]]

After these 3 layers process the data, i.e., after the data is encapsulated in these 3 layers, the next layer, the *transport layer* adds a header to the data. 

![[L4header.png]]

The transport layer is explained in detail here:


### [[OSI Model Layers#Transport Layer]]

To review until now, the data is prepared by the top 3 layers, a layer 4 header is added on. Note that at this point in the process, this unit of data plus the L4 header is called a **segment**. Remember, that if the data being sent is large enough, the data will be segmented into various smaller segments and each segment will have its own header. Next, that segment is sent to Layer 3 and another data header is added to it.

![[L3header.png]]

### [[OSI Model Layers#Network Layer]]

When the L3 header is added to the data segment, it is called a packet. Next, the data is firther encapsulated at Layer 2, this time with both a layer 2 header and a layer 2 trailer.

![[L2_infographic.png]]

### [[OSI Model Layers#Data Link Layer]]

After a data packet gets encapsulated by Layer 2, it is called a **frame**. Now, the data is not further encapsulated at Layer 1. This frame is then sent over the connection, whether it is electrical signals over a cable, or wireless signales in the case of Wi-Fi to the neighbouring systems. Layer 1 is explained here:

### [[OSI Model Layers#Physical Layer]]

After the data frame reaches the other device, it is de-encapsulated to retreive the origianl data. This is done by sending the data frame through Layers 1 to 7 on the destination device.

![[data_transfer.gif]]

The data goes through a transformation from Layer 7 to Layer 1 while being encapsulated. The terms used for the data change over this encapsulation process. These terms are collectively called **Protocol Data Units** (PDUs). For example, a segment is a term for a Layer 4 PDU, packet is a term for a Layer 3 PDU, etc. At Layer 1, the name for the PDU is **Bit**.

![[PDUs.png]]

Here are a few acronyms to remeber the data layers:

* **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing (Layer 7 to Layer 1)
* **P**lease **D**o **N**ot **T**each **P**eople **A**cronyms (Layer 1 to Layer 7)

Here is a link to the next section:
[[TCP IP Suite]]
