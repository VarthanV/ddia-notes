# Actual Serial Execution

-  The simplest way to avoid concurrency problems is to remove the concurrency entirely and to execute only one transaction at a time in serial order on a single thread.

-  By doing so we completely avoid the problem of detecting and preventing conflicts between txn , the resulting isolation is by defenition serializable.

- A system designed for single threaded execution can perform better than a system that supports concurrency because it can avoid the coordination overhead of locking. 

- However throughput is limited that to a of single CPU core.

- In order to make use of the Single thread txn needs to be structured differently from their traditional form.


## Encapsulating Transactions in Stored Procedures

- Systems with single threaded serial txn processing don't allow interactive multi statement txns. Instead the application must submit the entire txn code to the database ahead of time as a **stored procedure**. 

- Provided all data for txn is in the memory the stored procedure can execute very fast without waiting for any network or disk I/O.

## Pros and cons of stored procedures

- Each database vendor has its own language for stored procedures. 

- Code running in a database is difficult to manage compared to an application server, hard to debug , trickier to test and difficult to collect metrics.

- A database is more performance sensitive than an application server. Because a single database instance ins often shared by many application servers. A badly written stored procedure (using lot of time memory or CPU time) can ensure more trouble than bad written code in server.

## Summary

- Every txn must be small and fast because it takes only one slow txn to stall all the txn processing

- It is limited to usecases where active dataset can fit in memory. Rarely accessed data could potentially be moved to disk , but if needed to be accessed in a single-threaded txn the system could get very slow.

- Write throughput must be low enough to be handled on a single CPU core or else txn be  to be partitioned without requiring corss partition coordination.


