# Multi Leader Replication

- Leader based replication has one major flaw, All writes go through a single leader, if the leader node goes down writes are blocked.

- Extension of this model is to allow more than one leader to accept writes.

- Replication still happens the same way each node that processes a write must forward the data change to all other nodes. 

- This is known as **multi-leader,master/master or active/active** replication

- Each leader simultaneoulsy acts as follower to other leaders.


![Multi Leader Replication](../assets/multi-leader-replication.png)

## Single-leader and Multi-leader configurations in a multi-data-center deployment

## Performance

- In a single-leader configuration every write must go over the internet to data center with leader, This can add significant latency to writes
and might contravene the purpose of having multiple datacenters.

- In a multi-leader configuration every write can be processed in the local datacenter and replicated asynchornously to
other data centers.

- Thus inter datacenter network delay is hidden from the user thus increasing overall latency.


## Tolerance of datacenter outages

- In single leader configuration if the datacenter with leader , failover can promote another follower in a datacenter
to be leader.

- In multi leader configuration each data center can operate independently of others and replication catches up
when failed datacenter comes back online.

## Tolerance of network problems

- Traffic between datacenters goes over public internet which may be less reliable than local network 
within a datacenter.

- A single leader configuration is very sensitive to problems within inter-datacenter link because writes are made
synchornously over this link. A multi leader configuration with usually network problems can tolerate better.

## Disadvantages of multi leader replication

- Same data might be concurrently modified in two datacenters and those write conflicts must be resolved
(conflict resolution)

- Auto-incrementing keys, triggers and integrity constraints

## Clients with offline operation

- Another situation where multi-leader replication is appropriate is if we have an application that needs to
continue work while it is disconnected from the internet.

- Consider apps like Calendar in phone , we are able to create events when it is offline,  the data syncs
with the remote when the connections is back

- Every device has a local database that acts as a leader (accepts write requests)  and there is asynchornous multi-leader
replication process , between the replicas of the calendar and other devices.

- The replication lag depends on internet availablity


- It is essentially same as multi-leader replication between data centers. each device is a **datacenter** and network
connection between them is extremely unreliable. 

- **CouchDB** is designed for mult leader replication purpose.


## Colloborative Editing

- 
