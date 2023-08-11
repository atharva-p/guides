# Unit 1 
## questions 

12M 

IOT architecture and it's layer.
IOT Reference model
Main design principle

4m

Protocol of IOT (physical, data link, network, transport, application)
Difference LAN, WAN
Basic and advance devices
Devices and gateway difference
# IOT architecture and it's layers 

![](Pasted%20image%2020230810195755.png)

Use **BADSCRA** to remember the layers. 

asset layer - manages assets in the iot system. includes devices like actuators, gateways, sensors and devices and other objects within the iot system. 

resource layer - the resource layer provides the sensing capabilities for the different sensors, actuators and devices within the system. This is also where gateways are placed. identification of devices can be done using RFID (radio frequency distribution)

communication layer - responsible for seamless data transfer between different devices within an IOT system. 

service support layer - provides services to perform common and routine tasks. usually offloaded to data centers or in a cloud environment. 

data and information layer - processes data to get meaningful insights from the data collected, like data analytics. 

application layer - this is where the actual user facing applications are deployed. interface between IOT system and the users. 

business layer - makes sure that IOT supports the core business or operations. 

security - makes sure the data from the IOT system is secure and prevents outside threats. 

management - manages various parts of the IOT system. 

IOT data and services - processing, managing interactions within the system and providing services. 

# IOT reference model

![](Pasted%20image%2020230810202428.png)

# Main design principles 

![](Pasted%20image%2020230811062113.png)

1. overall design objective is to get horizontal system of real world services that are open source oriented. 
2. design for reuse of IOT resources 
3. design for a set of support services that can be used for application development and execution 
4. design for abstraction 
5. design to ensure trust, security and privacy 
6. design to ensure scalability, performance and evolvability, simplicity and diversity
7. design for simplicity of management 

# Protocol of IOT 

application layer - responsible for providing user interfaces and functionalities to the users. hypertext transfer protocol (HTTP) is used in this layer 

data link layer - concerned with the local delivery of data between nodes on the same network. Ethernet, IEEE 802.11 wifi protocols are examples 

physical layer - responsible for collecting data from the physical world and transmitting it to other layers of the architecture. it can include 

1. sensors - they collect data from the real world 
2. gateways - these devices connect sensors and actuators to the network. they convert data collected into transmittable format
3. actuators - take action based on the input from the sensors
4. power sources - batteries, power lines or solar 
5. network - physical transmission of data, like using wired ethernet, wifi or bluetooth 

# difference between LAN and WAN 

![](WhatsApp%20Image%202023-08-11%20at%2006.40.47.jpg)

# basic vs advanced IOT devices 

![](WhatsApp%20Image%202023-08-11%20at%2006.40.47%201.jpg)

# devices vs gateways 

![](WhatsApp%20Image%202023-08-11%20at%2006.40.48.jpg)
