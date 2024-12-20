# Detecting faults

- Systems need to automatically detect faulty nodes
    - A load balancer needs to stop sending requests to a node that is dead (take it out of rotation).

    - In distributed db with a single leader replication if the leader fails the follower needs to be promoted to be the new leader.

    
- If we can reach the machine on which the node should be running , but no process is listening on the destination port (because the process crashed). The operating system will helpfully close or refuse TCP connections by sending a **REST** or **FIN** packet in reply. However if node crashed while it was handling the request , we may have no way of knowing how much data was actually processed by remote node.

- If a node process crashed but the OS is still running a script can notify other nodes about the crash so that another node can take over quickly without having to wait for a timeout to expire (HBASE does this).

- If we have access for management interface to the network switches in datacenter we can query them to detect link failures in a hardware level (eg if remote machine is powered down). This option is ruled out if we are connecting via internet or if we are in shared datacenter with no access to switch themselves.

- If a router is sure that the IP address that we are trying to connect to is unreacheable ,it reply with an ICMP destination unreachable packet. 

- Eventhough if we get a TCP ACK there is no way to say that the application processed the request completely without crashing. 

- We cannot be sure about anything unless the network informs so.
