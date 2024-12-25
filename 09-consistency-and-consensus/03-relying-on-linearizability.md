# Relying on Linearizability

## Locking and leader election

- A system that uses single leader replication need to ensure that indeed there is only one leader , not several (split brain).

- One way of electing a leader is to use a lock; every node that starts up tries
to acquire the lock and one that succeeds becomes the leader. 

- No matter how the lock is implemented it must be lineraizable, all nodes must agree which nodes owns the
lock

- Apache Zookeeper and etcd are often used to implement distributed locks and leader election.

- They use consensus algorithms to implement linearizable operations in fault tolerant way.

## Constraints and uniqueness guarantees

- To enforce unique constraint like database must have one username and one email etc , we need to have linearizability.

- If two clients perform a conflicting operation only one must go through and other should be failed 

- The situation is actually similar to lock , When a user registers they acquire a lock on the username.

- They will use the atomic compare and set operation to claim the username provided it is not already taken.

- Similar issues arise when bank bal doesn't want to go negative and dont want to sell items with more price in warehouse or booking flight seats concurrently the same seat. 

- These must be a single upto date value all nodes agree on

## Implementing Linearizable Systems

- Linearizability means behave as though there is single copy of data and all ops in it are atomic.

## Single Leader Repliaction(potentially linearizable)

- In system with single leader replication the leader has the primary copy of data that is used for writes.

- Followers maintain backup copies of the data on other nodes.

- If we make reads from the leaders or from synchornously updated followers they have the potential to be linearizalbe. However ntot every single leader replication database is linearizable either by design or due to concurrency bugs.

## Consensus algorithms (Linearizable)
- Consensus protocols contain measures to prevent split brain and stale replicas.

- They implement linearizable storage safely

## Multi-leader replication (not linearizable)

- They are not linearizable because they concurrently process writes on multiple nodes and asynchornously replicate to other nodes.

- For this reason they can produce conflicts writes that require resolution.

## Leaderless replication (probably not linearizable)

- For systems with leaderless replication we need to obtain strong consistency by requiring quorum reads and writes (w+r>n). Depending on the exact configuration of quorums and depending on how we define strong consistency.