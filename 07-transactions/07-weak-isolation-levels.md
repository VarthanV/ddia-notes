#  Weak Isolation Levels

- Concurrency issues are hard to reproduce and solve , database has long tried to hide concurrency issues from application by providing **transaction isolation**.

- In theory isolation must make sure to pretend that no concurrency is happening ; serializable isolation means that the database guarantees that the transactions have same effect as if they ran serially.

- In practice isolation is not that simple , Serializable isolation has a performance cost and many dbs dont want to pay that price.

- It is common for systems to use weaker levels of isolation which protect against some concurrency issues. 

