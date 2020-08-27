# 3-tier_solution
 - User communicates with Route 53 and retrieves URL
 - User connects to ELB in public subnet
 - ELB connects to user to an EC2 instance
    - EC2 instance is in an Auto-Scaling group in a private subnet
    - Each AZ has EC2 instances
 - EC2 read/writes data to data subnet
    - data subnet is a private subnet which contains an RDS and (usually) an Elasticache

## LAMP Stack on EC2
 - Linux: EC2 OS
 - Apache: Web Server run on Linux (running on EC2)
 - MySQL: database on RDS
 - PHP: Application logic (running on EC2)
 - Optional: 
    - Memcached or Redis for caching
    - EBS drive (root) to store local app data and software
