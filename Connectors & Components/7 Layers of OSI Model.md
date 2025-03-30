# OSI Model :

The OSI `(Open Systems Interconnection)` Model is a set of rules that explains how different computer systems communicate over a network. The OSI Model consists of 7 layers and each layer has specific functions and responsibilities.

![image](https://github.com/user-attachments/assets/5b0ea920-a663-441d-b269-a64e74b37d49)

## Layer 1 – Physical Layer

The lowest layer of the OSI reference model is the Physical Layer. It is responsible for the actual physical connection between the devices. 
- The physical layer contains information in the form of `bits`.
- Common physical layer devices are `Hub, Repeater, Modem, and Cables`.

![image](https://github.com/user-attachments/assets/a229005a-56ff-4b08-9c69-3d452a537fc4)

## Layer 2 – Data Link Layer (DLL)

The data link layer is responsible for the node-to-node delivery of the message. The main function of this layer is to make sure data transfer is error-free from one node to another, over the physical layer. When a packet arrives in a network, it is the responsibility of the DLL to transmit it to the Host using its MAC address. `Packet` in the Data Link layer is referred to as `Frame`. `Switches` and `Bridges` are common Data Link Layer devices.

The Data Link Layer is divided into two sublayers:

- Logical Link Control (LLC)
- Media Access Control (MAC)

The packet received from the Network layer is further divided into frames depending on the frame size of the NIC (Network Interface Card). DLL also encapsulates Sender and Receiver’s MAC address in the header.

The Receiver’s MAC address is obtained by placing an ARP (Address Resolution Protocol) request onto the wire asking, “Who has that IP address?” and the destination host will reply with its MAC address.

![image](https://github.com/user-attachments/assets/c752a80d-6bf8-45cb-9476-cf9abab49040)

## Layer 3 – Network Layer

The network layer works for the transmission of data from one host to the other located in different networks. It also takes care of packet routing i.e. selection of the shortest path to transmit the packet, from the number of routes available. The sender and receiver’s IP address are placed in the header by the network layer. Segment in the Network layer is referred to as Packet. Network layer is implemented by networking devices such as `routers` and `switches`.

![image](https://github.com/user-attachments/assets/e057b255-dc96-469c-9b47-094051de469f)

## Layer 4 – Transport Layer

The transport layer provides services to the application layer and takes services from the network layer. The data in the transport layer is referred to as `Segments`. It is responsible for the end-to-end delivery of the complete message. The transport layer also provides the acknowledgment of the successful data transmission and re-transmits the data if an error is found. Protocols used in Transport Layer are `TCP, UDP NetBIOS, PPTP`.

![image](https://github.com/user-attachments/assets/4f7a3fd1-d815-4ff1-a83b-4564fb2da8e2)

## Layer 5 – Session Layer

Session Layer in the OSI Model is responsible for the establishment of connections, management of connections, terminations of sessions between two devices. It also provides authentication and security. Protocols used in the Session Layer are `NetBIOS, PPTP`.

![image](https://github.com/user-attachments/assets/94efb8ae-03b6-4ded-af71-50ae2cdea250)

## Layer 6 – Presentation Layer

The presentation layer is also called the Translation layer. The data from the application layer is extracted here and manipulated as per the required format to transmit over the network. Protocols used in the Presentation Layer are `JPEG, MPEG, GIF, TLS/SSL` etc.

![image](https://github.com/user-attachments/assets/f44c82f1-ab1f-45d9-8195-6073e26a3a75)

## Layer 7 – Application Layer

Applications produce the data to be transferred over the network. This layer also serves as a window for the application services to access the network and for displaying the received information to the user. Protocols used in the Application layer are `SMTP, FTP, DNS` etc.

![image](https://github.com/user-attachments/assets/7779d7b1-f870-4bec-91e1-a779f7f0e699)

![image](https://github.com/user-attachments/assets/fd85e2ec-48bc-4086-b9c8-9c1b8318a0ee)

![image](https://github.com/user-attachments/assets/def22527-1235-4e7c-890e-55d85db9e2ed)

# OSI vs TCP/IP

![image](https://github.com/user-attachments/assets/3827b33a-2872-4fff-9630-0cb7ca1c0774)
