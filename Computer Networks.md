# Unit 1 

# Address resolution protocol 

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

