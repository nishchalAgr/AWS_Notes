# EBS_Volumes
 - When an EC2 machine is terminated, it loses its data 
    - Unexpected terminations can happen, so you may want to store instance data elsewhere
 - An EBS Volume is a network drive that can be attached to instances 
    - Allows for instances to persist data
 - By default, it is locked to an AZ
    - Snapshots are needed to move EBS volumes across AZs
 - Has a specified provisioned capacity
    - You get billed for all the provisioned, not used, data
    - Capacity can be increased over time
 - 4 types of EBS volumes
    - GP2 (SSD): General purpose SSD, balances price and performance
    - IO1 (SSD): Highest Performance SSD, for low-latency and high throughput workloads
    - ST1 (HDD): Low cost HDD, for frequently accessed, high throughput workloads
    - SC1 (HDD): Lowest cost HDD, for infrequently accessed workloads 
 - EBS volumes are characterized by size, throughput, and IOPS (I/O Ops per second)
 - Only GP2 and IO1 can be used as boot volumes

## GP2
 - Rec. for most workloads
 - Useful for:
    - System boot 
    - Virtual desktops
    - Low-latency interactive apps
    - Development and test environments
 - 1GB-16TB
 - Small gp2 volumes can burst IOPS to 3000
 - Max IOPS is 16000 (at 3 IOPS/GB)

## IO1 
 - For critical business apps that require sustained IOPS performance or higher than GP2 limit
 - 4GB-16TB
 - IOPS is provisioned (PIOPS) - MIN 100 - MAX 64000(nitro) or MAX 32000(not nitro)
 - Max IOPS:GB ratio is 50:1

## ST1
 - Streaming workloads requiring affordable, consistent, and fast throughput
    - Apache Kafka
 - 500GB-16TB
 - Max IOPS is 500
 - Max throughput of 500 MB/s, can burst

## SC1
 - Throughput-oriented storage for large, infrequently accessed, volumes of data
 - Most affordable
 - 500GB-16TB
 - Max IOPS is 250

## EBS vs Instance Store
 - Some instances come with instance store rather than just root EBS volumes
 - Instance store is physically attached to the machine while EBS is a network drive
 - Pros:
    - Better I/O performance (very high IOPS)
    - Good for temporary data (ex. cache)
    - Data survives reboots
 - Cons:
    - On stop or termination, data is lost
    - Cannot be resized
    - Backups are more complicated and must be done manually