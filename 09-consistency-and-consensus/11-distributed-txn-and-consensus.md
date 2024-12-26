# Distributed Transactions and Consensus

- There are number of situation in which it is important for nodes to agree

## Leader Election
 
- In database with single leader replication all nodes must agree on which node is the leader.

- The leadership position might become contested if some nodes can't communicate with other due to network fault.

- In this consensus is important to avoid a bad failover and split brain situation , where two nodes accept writes individually as if they are the leader and their data would diverge , leading to inconistency and data loss.

## Atomic Commit

- In a database the supports transactions spanning several nodes or partition we have the problem that a txn may fail on some nodes but succeed on other.

- If we want  to maintain transaction atomicity we have to get all nodes agree on the outcome of the txn , either they all abort/rollback if anything goes erong or they all commit. This is known as the ``atomic commit problem``.

