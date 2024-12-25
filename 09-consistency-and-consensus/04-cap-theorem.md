# The CAP theorem

- If application requires linearizability and some replicas are disconnected from other replicas due to a network problem then some replicas cannot process requests while they are disconnected, they must either wait until the network problem is fixed or return an error (either way they become unavailable).

- If application does not require lineraizability then it can be written in a way that each replica can process requests independently even if it is disconnected from other replicas (eg multi leader). in this case the application can be available in face of a network problem but behavior is not linearizable.

- Applications that don't require linearizability can more tolerant of network problems.

- In case of a network partition between the systems in the cluster , We can either choose between availability or consistency.

## Linearizability and Network delays

- Even RAM on a modern multi-core CPU is not linearizable , If a thread running one CPU core writes to memory address and thread on another CPU core reads the same address shortly afterward it is not guaranteed to read the value written by first thread(unless a  memory barrier or fence is used).

- The reason is that every CPU core has its own memory cache and store buffer. Memory access first goes to cache by default and any changes are directly written out to main memory.

- Accessing from a cache is faster , but it introduces duplicacy and loss of linerazibality.

- The reason for dropping linearizability i s performance.

- If we want linearizability the response time of read and write requests is propotional to the uncertainity of delays in network.

