# Summary

## Partitioning

- In MapReduce, mappers are partitioned according to input file blocks. The output of mappers is repartitioned sorted and merged into a configurable number of reducer partitions.

- The purpose of this process is to bring all the related data (eg all records with the same key together in same ) place.

- Post MapReduce dataflow engines try to avoid sortng unless it is required but they take a approach similar to partitioning.


### Role of Partitioning in MapReduce

Partitioning plays a critical role in the **Shuffle and Sort phase** of a MapReduce job, determining how the intermediate data from the mappers is distributed among the reducers.

---

### How Partitioning Works:

1. **Mapper Output:**
   - Each mapper produces key-value pairs as output.
   
2. **Partitioning Function:**
   - The partitioning function takes a key as input and determines which reducer should process it, often using a formula like:  
     ```
     partition = hash(key) % numReducers
     ```

3. **Data Transfer:**
   - The partitioned data is shuffled and sent to the appropriate reducers.

---

### Example:

**Use Case: Word Count**  
- Input: `["apple", "banana", "apple", "cherry"]`
- Mappers emit:
  ```
  Mapper 1 -> (apple, 1), (banana, 1)  
  Mapper 2 -> (apple, 1), (cherry, 1)
  ```

- Partitioning: Based on hash values of the keys:
  ```
  apple -> Reducer 1  
  banana -> Reducer 2  
  cherry -> Reducer 3
  ```

- Reducers then aggregate the values:
  ```
  Reducer 1 -> (apple, 2)  
  Reducer 2 -> (banana, 1)  
  Reducer 3 -> (cherry, 1)
  ```

  ## Fault Tolerance

  - MapReduce frequently writes to disk which makes it easy to recover from a individual failed taks without restarting the entire job but slows down execution in the failure free case.


  ## Sort Merge join

  - Each of inputs being joined goes through a mapper that extracts the join key , by partitioning sorting and merging all the records with same key end up going to same call of the reducer. The fn can output then joined records.


  ## Broadcast hash joins

  - One of two joins input it small so it is not partitioned and can entirely loaded into hash table. Thus 
  can start a mapper for each partition of the large join input , load the hash table for small input into each mapper and then scan over the large input one record at a time, querying the hash table for each record.

  - The distinguished feature of batch processing job is that it reads some input and produces some output data without modifiying the input. 

  - The input is bounded and has fixed size


  In batch processing systems like Hadoop MapReduce, fault tolerance is handled automatically, and duplication is avoided by the system's design. Here's why fault tolerance does not typically result in duplicate entries:

---

### 1. **Write-Once Data Model**  
- HDFS (Hadoop Distributed File System), commonly used for batch processing, follows a **write-once, read-many** model.
- Once data is written to the output directory by a MapReduce job, it cannot be overwritten unless explicitly removed.

---

### 2. **Checkpointing and Re-execution**  
- If a task (mapper or reducer) fails, the system re-executes only the failed task from the last checkpoint, ensuring that its partial or uncompleted work is not included in the final output.
- Tasks are idempotent, meaning that running them multiple times on the same data produces the same result without duplication.

---

### 3. **Intermediate Data Handling**  
- Intermediate outputs from mappers (stored on local disks) are not directly written to the final output directory. 
- If a mapper fails, its intermediate data is discarded and recomputed.

---

### 4. **Atomic Writes to Output**  
- Reducers write their final outputs to HDFS in an **atomic operation**. This ensures that either:
  - The entire output is successfully written.
  - Or nothing is written at all in the case of a failure.
- This prevents partial or duplicate outputs in the final data.

---

### 5. **Task Deduplication**  
- The system tracks the status of tasks using a **JobTracker** (in older versions of Hadoop) or **ResourceManager** (in YARN).
- If a task is restarted due to failure, its previous attempts are discarded, and only the last successful attempt is considered valid.

---

### Example Scenario: Word Count  
- Input: `["apple", "banana", "apple", "cherry"]`
- If a mapper processing the chunk with "banana" fails, the system re-executes only that mapper.
- Reducers write final output like:
  ```
  apple -> 2  
  banana -> 1  
  cherry -> 1
  ```

There are no duplicates because:
1. The failed task's output is discarded.
2. Reducers write data atomically.

---

### 6. **Manual Duplication Avoidance**  
- If multiple runs of the same batch job write to the same output directory without cleaning it, duplicates may occur. This is why it's recommended to clean or use a new output directory for each job run.
---
Fault tolerance in batch processing systems like Hadoop MapReduce is achieved through checkpointing, re-execution of failed tasks, and atomic writes. These mechanisms ensure there are no duplicate entries in the final output, allowing developers to focus on logic rather than fault tolerance.