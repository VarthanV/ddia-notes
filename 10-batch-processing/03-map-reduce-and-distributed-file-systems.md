# MapReduce and Distributed FileSystems

- MapReduce is like unix tool but distributed across thousands of machines.

- A single MapReduce job is comparable to a single unix process, it takes one or more inputs and produces and one or more outputs.

- Running a mapreduce job doesn't modify the input since the input to the job is immutable and it doesn't have any side effect rather than writing to the output. Files are written once in sequential fashion.

- MapReduce jobs read and write files on a distributed file system. 

- In Hadoop's implementation of Map-Reduce the filesystem is called **HDFS**. 


## HDFS

- HDFS is based on shared-nothing principle.

- Shared Disk Storage is implemented by a centralized storage appliance . 

- Shared nothing requires no special hardware just conventional computers connected over network.

- HDFS consists of daemon process running on each machine , exposing a networ service that allows other nodes to access the files stored on that machine.

- A central server called **NameNode** keeps track of which files blocks are stored on which machine.

- HDFS conceptually creates one big filesystem that can use the space on the disks of all machines running the daemons.

- In order to tolerate machine and disk failures file blocks are replicated on multiple machines.


