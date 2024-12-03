# Problems with replication log

- Being able to tolearte node failures is the one of the reason for wanting replication.

- Leader-based replication needs the writes to go through a single node , but reads can go to any replica. 

- For **read-heavy** workload it is a common pattern to create multiple followers and divert this read across these nodes to reduce the load on the leader.

- In read-scaling arch we can handle load by increasing the follower nodes, This approach realistically works only with **asynchornous-replication**. In synchornous replication it will be likelier for all nodes will be unavailable for writing.

- Unfortunately if an application reads from any **asynchornous follower** , it may see outdated information if the follower has fallen begin . 

- This leads to inconsistencies in the database , if we query both on leader and follower we will get different results because all writes have not been reflected in the follower.

- The inconsistency is just a temporary state if the leader stops transferring data to the follower it might catch up with the leader. This is known as **eventual consistency**.

- The term eventually is deliberately vague , there is no limit to how far a replica can fall behind. 

- In normal op , the delay betwen write happening on a leader and reflecting in  a follower (replication lag) is just fraction of second.

- If system is operating in capacity or the network lag is higher it may extend to several seconds.

- When the lag is high the inconsistencies it introduces are major. 

## Reading your Own writes

