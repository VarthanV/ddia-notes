# Handling node outages

- Any node in the system can go down, unexpectedly due to a fault but just as likely due to a planned maintenance.

- Being able to reboot individual nodes without downtime is a big advantage for operations and maintenance.

- The goal is to keep system as whole running despite individual node failures and to keep to impact of node outage small as possible

## Follower failure: Catchup recovery

- On its local disk ,follower keeps  a log of the data changes that is has received from the leader 

- When the follower node goes down or the network is cut between leader and follower node for some reason it can easily recover since it has the last transaction processed and requests changes from the leader.

- Once the follower has caught up, the leader can normally process data from leader.

## Leader Failure: Failover

- Handling a failure of leader is tricky one the follower needs to be promoted to new leader.

- Client needs to be configured to send the writes to the new leader. 

- Followers must tail changes from the new leader , This process is called **failover**

- Failovers can happen both manually and automatically.

## Automatic failover process

**Determining the leader has failed**: There can be many things that can go wrong for a leader to failure , Power outage , network issues , infinite deadlock and more. The simple way to detect is to pass back messages between leader and child if the leader doesn't response within threshold say 30 seconds the leader is determined as failed.

**Choosing a new leader**: This could be done through a leader election process or a controller node which elected the previous leader , Making the followers agree on new leader is a consensus problem , It is best to make the most upto-date replica the leader so that minimize data loss . In semi-synchornous replication the synchornous replica will be elected as the next leader since it has most / close to upto-date changes.

**Reconfiguring the system to use new leader**: If the new leader comes back it needs to realize that is been made to step down and join as one of the follower.

## Gotchas

- If async replication is used the new leader might not have received all writes from the old leader before it failed. If former self is back after new leader is chosen , what happens to those writes, the new leader might received conflicting writes mean time. The most common solution for the old leaders unreplicated writes to be discarded which may violate client's durability expectations.

- In some cases there is a chance that two leaders might act as leader , that phenomena is called **split brain**, In this case there might be conflicting writes going to both the nodes and there might be no strong mechanism to  resolve those , Clusters have mechanism to shutdown one leader if two leaders at detected.

- There are no easy solutions to this proble, some ops prefer to perform **failovers manually** even if the software supports automatic failover.

