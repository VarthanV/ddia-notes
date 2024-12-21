# Timeouts and Unbounded Delays

- A long timeout means a long wait until a node is declared dead (during this time users may have to wait or see error messages)

- A shorter timeout detects fault faster but carries a higher risk of incorrectly dectecting a node dead
when it has suffered only temporary slowdown.

- Prematurely declaring a node dead is problematic , because if it is in the middle of processing a action
(eg sending an email) and another node takes over, then we end up performing the action twice.

- When a node is declared dead its responsibilities need to be transferred to another node which places
additional load on other nodes and network .

- If the node is already struggling with high load , declaring nodes dead prematurely can make the problem 
worse. 

- In particular it could happen that the node was not completely dead but due to slow to respond due
to overload. transferring load to other nodes can cause cascading failure.

--- 

# Network congestion and queuing

- The variability of packet delays on a computer networks is more often due to **queuing**

- If several different nodes simultaneously try to send packets to the same destination , the network switch must
queue them up and feed them into destination one by one. 

- On a busy network link a packet have to wait until it can get a slot.  This is called **network congestion**.

- If the switch is full the packet is dropped so it needs to be resent eventhough the network is functioning fine.

-  When packet is reached the destination and all the CPU cores are busy processing , the incoming
request from network is queued by operating system , until the application is ready to handle. Depending 
on the load in the machine this may take arbitary length of time.

- In virtualized environments a running OS is often paused for tens of milliseconds while another virutal machine
uses a CPU core. During this time tthe VM cannot consume any data from the network so the incoming data is
queued (buffered by the virutal machine monitor) further increasing the variability of network delays.

- TCP performs flow control in which node limits rate of sending in order to avoid overloading a network link.

