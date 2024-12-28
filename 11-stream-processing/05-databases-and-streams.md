# Database and Streams

- An event is a record of something that happened some point in time.

- The thing happened may be user action , write to database , search qyery etc.

- The fact that something that is written to database is an event that can be captured, stored and processed.

- Replication log is a stream of database write events, produced by the leader as it processes the transaction. The events in replication log describe the data change that ocurred.

- Processing an event is assumed to be deterministic operation, its just another case of event streams.

## Keeping systems in Sync

- Related data that appear in different places need to be kept in sync with each other. 

- If an item is updated in the database , it also needs to update it in cache , search indexes and warehouse. 

- Without warehouse this is done using ETL processes, often taking a full copy of database transforming it and bulk loading into data warehous. 


- If periodic full db dump is slow , an alternative is to do **dual writes**, in which app writes to each of the systems when data change , for eg write first to db , then updating in search index, then invalidationg cache entries.


## ETL

ETL stands for **Extract, Transform, Load**, which is a common process in data engineering and data integration. Here's an overview of the ETL process:

---

### 1. **Extract**
This step involves gathering raw data from various source systems, such as:
- Databases (PostgreSQL, MySQL, MongoDB, etc.)
- APIs
- Flat files (CSV, JSON, Excel)
- Message queues
- Cloud storage or data lakes

### 2. **Transform**
The raw data is cleaned, enriched, or reshaped to fit the requirements of the target system. This step may include:
- Filtering irrelevant or erroneous data
- Joining or splitting datasets
- Normalization or denormalization
- Applying business rules or calculations
- Formatting and standardizing fields (e.g., date formats)

### 3. **Load**
The transformed data is then loaded into the target system, such as:
- Data warehouses (Snowflake, BigQuery, Redshift)
- Databases
- Analytics platforms
- Data lakes for further processing

---

### Tools and Technologies
#### ETL Tools
- **Traditional ETL Tools:** Informatica, Talend, SSIS (SQL Server Integration Services)
- **Modern Cloud Solutions:** Apache Airflow, AWS Glue, Google Dataflow, Azure Data Factory
- **Open Source:** Apache NiFi, Pentaho

#### Languages and Frameworks
- Python (Pandas, PySpark)
- Go (for lightweight ETL processes)
- SQL for data extraction and transformation

#### Databases
- Relational (PostgreSQL, MySQL)
- NoSQL (MongoDB, Cassandra)

#### Containerization and Orchestration
- Docker (for environment consistency)
- Kubernetes (for scaling ETL pipelines)

---

### Workflow in ETL
1. **Schedule**: Automate ETL jobs using a scheduler like Apache Airflow or cron jobs.
2. **Monitor**: Set up logging and monitoring for performance tracking.
3. **Optimize**: Use parallel processing or stream processing for real-time ETL.


- Dual writes have serious **race condition** problems. 

- Another problem with the dual writes it that one writes may fail while other succeeds. This is fault tolerance problem rather than a concurrency problem.

- It also has effect of two systems becoming inconsistent with each other , ensuring either both succeed or fail is case of atomic commit problem which is expensive to solve.

