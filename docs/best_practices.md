# Best Practices for Deploying and Managing SnappyData
The following topics are covered in this section:

* [Using Index](best_practises/using_index.md)

* [Using Collocated joins](best_practises/collocated_joins.md)

* [Physical Designing with SnappyData](best_practises/physical_design.md)

* [Using Row vs Column Table](best_practises/use_row_column_table.md)

* [Right Affinity Mode to Use](best_practises/affinity_mode_to_use.md)

* [Capacity Planning](best_practises/capacity_planning.md)

* [Preventing Disk Full Errors](best_practises/prevent_disk_full_errors.md)

* [Design Database and Schema](best_practises/design_schema.md)

Loading data from external repositories like S3, CSV, HDFS, RDBMS and NoSQL
 (Should be a separate section if we have enough content ... )
  - how to load from S3, CSV, HDFS using SQL external tables
     -- How to deal with missing data or ignoring errors (CSV)
  - How to manage parallelism for loading
  - how to transform datatypes before loading (using SQL Cast, expressions)
  - How to transform and enrich while loading (Using spark program)
  - How to load an entire RDB (from a schema)? Example that reads all table names from catalog and then execute select from external JDBC source table on each table?
  - How to load data from NoSQL stores like cassandra (give Cassandra example using Spark-cassandra package)
  
  Snapshotting state from SnappyData to external repositories like S3,CSV/parquet, RDBMS and NoSQL
   - We recommend backing up state from SnappyData into a repository like HDFS or S3 in Parquet format. 
   - Repeat the How-tos from the above section
   
 Optimizing Query performance
   - Explaining 'Explain plan' 
   - 'Where is the time spent' using SnappyData Pulse
   - Tuning data shuffling costs and configuring /tmp for optimal performance
   - Tuning memory and eviction settings
   - Tuning JVM heap settings and GC settings
   - Tuning Offheap settings
   - Tuning broadcast , hash join thresholds
   - Tips for optimizing query performance when using the Smart connector
     -- e.g. when to use JDBC connection to route entire query vs only applying filters and projections    
   
 How to plan for large data volumes (maybe the same as capacity planning)
   - Sumedh, Hemant, etc are working on this
   - Computing heap requirements for different table types
   - a step-by-step guide to configuring heap and GC settings
   - Why we recommend SSD for disk or at least for /tmp
      -- crucial to speed up recovery when the cluster goes down , for instance. 
   - Figuring out GC problems and tuning pre-production
   - When to use additional compute nodes when resources are scarse or to manage concurrency
     -- i.e. suggest Apps use the smart connector and run very expensive batch jobs in a compute cluster
  
 When should I use Smart connector? (same as 'Right affinity mode' above)
 
 Managing the cluster
   - Starting, stopping the cluster .. configuring ssh and local disks?
   - backup, recovery of SnappyData disk stores, Snapshots to external repos.
   - Expanding the snappyData cluster at runtime -- rebalancing, etc
   - Linux level configuration: ulimit settings, etc. 

MISC
- Backups and Recovery
- online/offline backup and recovery -- needs testing
- redundancy and ensuring data availability for failures
- recovering from failures, revoking safely ensuring no loss of data
- last ditch recovery using data extractor; data redundancy implications
Troubleshooting and analysis
getting thread dumps from GUI or detailed stacks using SIGURG
observing logs for warning/severe/errors and decoding log messages
collating logs and stats using collect-debug-artifacts.sh
using VSD (can we make use of GemFire VSD docs?)
enabling/disabling logging levels/traces on-the-fly
 