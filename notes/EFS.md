# EFS
 - Managed NFS (network file system) that can be mounted on many EC2
 - EFS works with EC2 instances in multi-AZ
 - Highly available, scalable, expensive (3x gp2), pay per use
 - Uses security groups to control access
 - Compatible only with Linux-based AMIs
 - Encryption at rest using KMS
 - POSIX file system that has a standard file API
 - Scales automatically

## Scale and Performance
 - 1000s of concurrent NFS clients, 10GB+/s throughput
 - automatically grow to petabyte-scale
 - Performance modes
    - General purpose (default): latency sensitive (ex. web server)
    - Max I/O: higher latency, throughput, highly parallel (ex. big data)
 - Storage Tiers 
    - Standard: for frequently accessed files
    - Infrequent Access (EFS-IA): cost to retrieve files, lower price to store
      - controlled by a lifecycle policy 