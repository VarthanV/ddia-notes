# Handling node outages

- Any node in the system can go down, unexpectedly due to a fault but just as likely due to a planned maintenance.

- Being able to reboot individual nodes without downtime is a big advantage for operations and maintenance.

- The goal is to keep system as whole running despite individual node failures and to keep to impact of node outage small as possible

## Follower failure: Catchup recovery

- On its local disk ,follower keeps  a log of the data changes that is has received from the leader 

- When the follower node goes down or the network is cut between leader and follower node for some reason it can easily recover since it has the last transaction processed and requests changes from the leader.

- Once the follower has caught up, the leader can normally process data from leader.

## Leader Failure: Failover

- 