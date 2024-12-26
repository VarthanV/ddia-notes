# Distributed Atomic Commit

-  When a client asks the database to commit the txn on a single node setup , the writes are made durable

-  Each write is written to the write ahead log (WAL) before modifying the original pages for durability

- And lastly the COMMIT record is appended .

- If the database recovers from a crash we check in the WAL if the commit record was successfully written to the disk before crash , if not txn is rollbacked.

- If we have multi object transaction in a partitioned database or a term partitioned secondary index, it is simply not sufficient to simply send a commit request to all of nodes and independtly commit the txn to each one. In doing so it could easily happen that the commit succeeds on some nodes and fails on onther nodes which violates atomicity guarantee.

     - Some nodes may detect a constraint violation or conflict, making an abort necessary while other nodes are succesfully able to commit.

     - Some of the commit requests might be lost in the network , eventually aborting due to a timeout while other commit requests get through.

     - Some nodes may crash before the commit record is fully written and rollback on recovery while others commit.

