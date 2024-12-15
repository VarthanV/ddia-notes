# Partition and Secondary Indexes

- A secondary index usually doesn't identify a record uniquelty but rather is a way of searching the occurences of particular value like actions by user123, car with color red etc.

- The problem with secondary indexes is that they don't map neatly to partitions. There are two main approaches to partitioning a database with secondary indexes
     - Document based partitioing
     - Term based partitioning

# Partitioning Secondary Indexes by document

- 