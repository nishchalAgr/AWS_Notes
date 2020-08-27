# RDS-Overview
 - Relational Database Service
 - a managed DB that uses SQL for query
 - allows for multiple types of cloud-based DBs managed by AWS
    - MySQL
    - Postgres
    - MariaDB
    - Oracle
    - Microsoft SQL Server
    - Aurora (AWS proprietary DB), not compatible with free tier

## RDS vs Deploying DB on EC2
 - RDS is managed:
    - Automated provisioning, OS patching
    - Continous backups and restore to specific timestamp
    - Monitoring dashboards
    - Read replicas for better read performance
    - Multi AZ setup for DR
    - Maintainance windows for upgrades
    - Horizontal and Vertical scaling capability
    - Storage backed by EBS
    - cannot SSH

## RDS Backups
 - Backups are automatically enabled in RDS
 - Automated backups:
    - Daily full backup of the database
    - Transaction logs are backed-up by RDS every 5 mins
        - ability to restore to any point in time
    - 7 days retention
 - DB Snapshots:
    - Manually triggered by user
    - Retention of backup for as long as you want

## Read Replicas
 - replicas of DB to increase scale reads
 - up to 5
 - within AZ, cross AZ, or cross region
 - replication is async, so reads are eventually consistent
 - replicas can be promoted to their own DB
 - Applications must update the connection string to leverage read replicas
 - Read replicas can only be used with SELECT statements    
 - In AWS, you are billed when data goes from on AZ to another
    - Having a read replica across AZ will incur alot of costs during replication

## RDS Multi-AZ for DR
 - SYNC replication
 - One DNS name
    - automatic failover to standby DB
    - failover in case of:
        - loss of AZ
        - loss of network
        - instance/storage failure
 - increase availablity
 - not used for scaling
    - standby DB cannot be used in away unless main DB fails
    - however, read replicas can be set up as Multi-AZ for DR
