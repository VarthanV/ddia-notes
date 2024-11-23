# Replication

- Replication means keeping a copy of same data on multiple machines that are connected via network.

# Reasons

- To keep data geographically closer to users (reduced latency)

- To make sure the application works even though some parts fail thus incerasing high availability.

- To scale out number of machines that can serve read queries (thus increase read throughput).

- The most popular algorithms for replicating changes between nodes
    - Single-Leader
    - Multi-Leader
    - Leaderless

