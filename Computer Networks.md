Notes for computer networks 

# Unit 1 

# Internetworking

TCP/IP is known as the internet model. Data link and physical layers are local layers

In order for data to reach from one device to another, data passes through links. A link is between a device to router or router to router (or switches). 

Data packets coming from source to routers have only the MAC addresses attached to them, they do not have any network information associated with them.  

## Responsibilities 

Network layer operates at the source, router and the destination and has different responsibilities
### at source 
1. takes data from the previous layers / other protocols, forms an IP packet with routing information
2. The header of the packet also contains logical addresses (an IP address is a type of logical address) of the source and destination
3. if the data is too large, it is broken down into fragments 

### at router / switch 
1. responsible for routing the packets it receives. 
2. looks at the routing table and figures out some changes in the header file 
3. after the changes to the routing information, the packet is passed to the data link layer again. 

### at the destination 
1. address verification - takes the packets received and checks if the destination address matches with it's own address. 
2. unpacks the packet and sends it to the other layers. 
3. if the data was fragmented, it will wait to receive other packets and then join them to pass the complete data to other layers. 

# Internet protocol version 4 (IPv4)

Fourth gen IP protocol that was widely used. 32-bit addresses. Ipv4 addresses are divided into private and public. The public ones are globally unique and are routable over the internet. The private ones cannot be reached and are only intended to be used within a local network.  

IPv4 is a unreliable, connectionless protocol. Works on the best-effort delivery model with no guarantee of data delivery, (no) error control or the order in which data in sent. 

These above issues are managed by another upper protocol (of the transport layer) called the TCP. 

## UDP vs TCP 

User datagram protocols operate on datagrams, they are connectionless and are self contained. Each datagram has all the information it needs to reach it's destination. The order of delivery, or the delivery itself, is not guaranteed in udp

TCP is the connection-oriented protocol where the delivery of data is guaranteed. Data is segmented into segments and each segment has TCP information attached to it. Segments lost during transmission can be requested again. 

TCP segments aren't self contained because they require a connection to be formed between devices (unlike datagrams which don't require connections)

## IPv4 datagram format

<<<<<<< HEAD
![](Pasted%20image%2020230809140629.png)

![](Pasted%20image%2020230809140639.png)

# Address resolution protocol (ARP)

Logical addresses are used to recognize hosts and routers at the network level. It's is unique universally, and is implemented in software. IP is the 32 bit logical address assigned by the TCP/IP protocol 

Physical addresses are implemented using hardware. it's unique locally, like the MAC address. You need both logical and physical addresses because a network can use two different networking protocols at the same time. IP address also acts like your neighborhood address (street name, city) and MAC address acts like your name.




