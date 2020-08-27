# Aurora-Overview
 - proprietary to AWS
 - supports Postgres and MySQL
 - Aurora is "cloud optimized"
    - 5x performance improvement over MySQL on RDS
    - 3x performance improvement over Postgres on RDS
 - Aurora automatically grows in increments of 10GB, up to 64GB
 - up to 15 read replicas (vs 5 on MySQL) along with faster replication process
 - instantaneous failover
 - 20% higher cost than RDS

## High Availability
 - 6 copies of data across three AZ
    - 4/6 copies needed for writes
    - 3/6 copies needed for reads
    - self-healing with peer-to-peer replication
 - One Aurora instance takes writes (master)
 - Automated failover for master in less than 30 seconds
 - Support for cross-region replication
 - Support for auto-scaling on number of read replicas
 - Aurora provides a writer endpoint such that the writer has a DNS that always points to the master
 - Reader endpoint automatically connects to all read replicas, provides load balancing at a connection level
 - Features Backtrack: restore data at any point in time without using backups

## Security
 - Encryption at rest using KMS
 - Automated backups, snapshots, and replicas also encrypted
 - Encryption in flight using SSL (same process as MySQL or Postgres)
 - Allows authentication using IAM token (same method as RDS)
 - Protected with security groups
 - Cannot SSH into Aurora instance

## Serverless Aurora
 - Automated database instantiation and auto-scaling based on actual usage
 - Good for infrequent, intermittent, or unpredictable workloads
 - Pay per second 

## Gloval Aurora
 - Aurora Cross Region Read Replicas:
    - Useful for DR
    - Simple to put in place
 - Aurora Global Database (recommended):
    - 1 Primary Region (read/write)
    - Up to 5 secondary (read-only) regions, replication lag is less than 1 second
    - Up to 16 read replicas per secondary region
    - Helps for decreasing latency 
    - Promoting another region has an RTO of < 1 minute

