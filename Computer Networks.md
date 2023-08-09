# Unit 1 

# Address resolution protocol 

logical address ----> physical address

Logical address - internetwork address, denotes the address of the network, and is implemented using software. Different protocols use different logical addresses. IP is the logical address implemented by the TCP/IP protocol. 

Physical address - local address, denotes the devices using their hardware. Implemented at the hardware level. Media access control (MAC) address is a physical address. 

## Mapping 

Mapping is done to have logical (IP) addresses associated with physical addresses (MAC). Two types 

Static mapping - IP addresses are mapped to physical addresses. No use of any address resolution protocol. needs to be updated periodically, bad for performance. 

dynamic mapping - each time a machine has logical address, it can find physical using a protocol. for example, the ARP protocol. 

## ARP packet format

![](Pasted%20image%2020230809185538.png)

This packet is encapsulated directly to the data link layer. The data link layer has a final destination IP address. the type of the data link layer frame is also set to ARP. The target IP address (for which a physical address is required) changes according to four cases. 

hardware type (16 bits) - denotes the type of the network. ethernet is given type 1 

protocol type (16 bits) - denotes the type of the higher order protocol. IP has the value (0800)16. 

hardware length (8bits) - denotes the length of physical address in bytes. 6 bytes for mac addresses

protocol length (8 bits) - denotes the length of the logical address in bytes. 4 bytes for ip addresses. 

operation (16 bits) - denotes if it's a arp request or a arp reply packet. 1 for request, 2 for reply 

sender hardware address (32bits)  - mac address of the sender 

sender protocol address (32 bits) - ip address of the sender 

target hardware address (32 bits) - mac address of target (filed with 0s for a request arp) 

target protocol address (32 bits) - ip address of the target 

# Cases

gives the target ip address used based on 4 cases 

1. you're a host and you want to send on the same network - target Ip address is the destination ip address in the IP datagram
2. you're a host and you want to send a packet on a different network - target ip address is that of a router (because you need the physical address of the router also) 
3. you're a router and you want to send a packet to a host on the same network - target ip address of the arp packet is the destination ip address in the ip datagram
4. you're a router and you want to send a packet to a host on a different network - target ip address is the ip address of a router

# Reverse address resolution protocol (rarp) 

physical address ----> logical address. 

to create an IP datagram, host needs to know it's own IP address. 

same packet as arp, only difference between for request the value is 3 and reply the value is 4. 

1. rarp request is broadcast on the local network
2. another device on the network with knowledge of all the IP addresses will response with a rarp reply. 
3. requesting machine must run rarp client, responding will run rarp server. 

rarp packet is also encapsulated to a data link layer frame. 

# Unicasting

One source and one destination. relationship between source and destination is one to one. Router forwards the datagram received by it through one of it's interfaces. 

# Multicasting 

One source and a group of destinations. relationship is one to many. source is a unicast address, destination is a group address. the router may forward the received datagram through several of it's interfaces. 

## Multicasting vs multiple unicasting 

![](Pasted%20image%2020230809214456.png)

Multicasting starts with one packet from the source that gets duplicated by the routers. Takes less bandwidth Only one single copy of the packet travels between any two routers. 

In multiple unicasting, several packets are sent from the source. takes more bandwidth. Multiple copies of packets may travel between any two routers. 

# Internet group management protocol (IGMP) 

it is not a routing protocol. it is responsible for correcting and interpreting information about groups in a network. 

Type of IGMP messages: 
1. membership query messages 
	1. general 
	2. group-specific 
	3. group and source specific 
2. membership report 

## membership query message format 

![](Pasted%20image%2020230809220212.png)

type of the message (8bits) - query or report

response code (8bits) - response time 

group address (32 bits) - x.y.z.t. all 0s for general query messages.

resv - reserved for future and is not used. 

s - suppress flag 

qrv - querier's robustness variable 

qqic - querier's query interval code 

number of sources (N) - all 0s for group query message, all 0s for general query message, N for group-source-specific messages. 

## membership report format 

![](Pasted%20image%2020230809220758.png)

Record type - there are 6 record types currently. they have types 1-6 

auxiliary data len - length of auxiliary data included in each report.  
