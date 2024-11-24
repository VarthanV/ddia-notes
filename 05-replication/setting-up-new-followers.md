# Setting up new followers

## Algorithm 

- Take a consisent snapshot of the leader's database some point in time , if possible without taking lock on entire DB.

- Copy the snapshot to the new follower node

-  The follower connects to the leader and requests all the data changes that have happened since the snapshot was taken. This requires snapshot is associated with exact position in the leaders replication log. The position has various names for example PGSQL calls it as **log sequence number**

- When the follower has processed the backlog of data changes since the snapshot it has now caught up. it can now normally process data from leader as they happen

- In some systems this process is fully automated where as in others i can be a multi-step workflow that needs to manually performed by admin

