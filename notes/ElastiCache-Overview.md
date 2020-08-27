# ElastiCache-Overview
 - managed Redis or Memcached
 - caches are in-memory DB with high performance, low latency, runs on RAM
 - helps reduce load off of DB for read intensive workloads
 - write scaling using sharding
 - read scaling using read replicas
 - multi AZ with failover capacity
 - Use Cases:
    - ElastiCache acts as a cache for an RDS
        - must have an invalidation strategy to make sure only the most current data is used in there
    - User session store
        - User logs into any application
        - App writes session data into ElastiCache
        - When user hits another instance of app, instance retrieves data and user is already logged in

## Redis vs Memcached
 - Redis
    - Multi-AZ with Auto-Failover
    - Read-Replicas to scale reads and have high availability
    - Data Durability using AOF persistance
    - Backup and restore features
 - Memcached
    - Multi-node for partitioning of data (sharding)
    - Non persistant
    - No backup and restore
    - Multi-threaded architecture