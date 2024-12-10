# What is Conflict? 

- Some kinds of conflict are obvious, Two writes concurrently modified the same
field and same record , setting it to two different values.There is little doubt
than this is a conflict.


# Multi-Leader Replication Topologies

- A **replication topology** describes the communication paths along which writes are propogated from one node to another.

- If there are two leaders L1, L2 , there is only one way to propogate writes, 
Leader L1 must send all writes to L2 and viceversa. With more than two leaders various topologies are possible

- Circular Topology
- Star topology
- All to all topology


- The most general topology is **all-to-all** in which every leader sends it writes to every otuer leader.

- However more restricted topologies are used for MYSQL by default support only a circular topology 