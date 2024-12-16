# Durability

- The purpose of a database system is to provide a safe place where data can be stored without fear of losing it.

- Durability is the promise that once a txn has commited succesfully any data it has written will not be forgotten, even there is a hardware fault or database crashes.

- In a single node database durability typically means the data has been written to nonvolatile storage such as hard drive or SSD. It usually involes a write ahead log or similar which allows recovery in datastructures on disk are corrupted.

- In replicated database durability means the data has been successfully copied to some number of nodes.in order to provide a durability guarantee a db . We must wait until these writes or replications are complete before reporting a txn as success.

