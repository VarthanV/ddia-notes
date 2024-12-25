# Lamport Timestamps

- Each node has a unique identifier and each node keeps a counter of number of operations that is has processed.

- The Lamport timestamp is a simply  a pair of (counter,node id). 

- Two nodes may have same counter value but by including the node id in the timestamp each timestamp is made unique.

- Lamport timestamp bears no relationship to a physical time of day clock , but it provides total ordering , if we have two timestamps the one with a greater counter value is the greater 

- If the counter values are the same , the one with the grearter node ID is the greater timestamp.

- Every node and every client keeps track of the maximum counter value it has seen so far and includes the maximum on every request.

- When a node receives a request or res with maximum counter value greater than its own counter value, it increases is own counter to that maximum.

- Version vectors can tell if two operations are concurrent but lamport timestamp cannot tell where two opeartions are concurrent or whether they are casually dependent. Lamport is more compact than version vectors.

