# RDS-Security

## At Rest Encryption
 - Encrypt the master and read replicas with AWS KMS - AES-256
 - Encryption has to be defined at launch time
 - If the master is not encrypted, the read replicas cannot be encrypted
 - Transparent Data Encryption(TDE) available for Oracle and SQL server

## In-Flight Encryption
 - SSL certificates
 - Provide SSL options with trust certificates when connecting to DB
 - To enforce SSL:
    - PosgreSQL: rds.force_ssl = 1 in the AWS RDS console (parameter groups)
    - MySQL: Within the DB, GRANT USAGE ON \*.\* to 'mysqluser'@'%' REQUIRE SSL;

## Backups
 - Snapshots of un-encrypted RDS databases are un-encrypted
 - Snapshots of encrypted RDS databases are encrypted

## To encrypt an un-encrypted RDS DB
 - Create a snapshot 
 - Copy the snapshot and enable the encryption
 - Restore the DB from the encrypted snapshot
 - Migrate applications to the new DB, delete old DB
 
## Network and IAM
 - RDS DB are usually deployed in a private subnet
 - RDS security works by leveraging security groups, the same as EC2
 - IAM policies help control who can manage RDS
 - traditional username and password can be used to access the DB
 - IAM-based authentication can be used to login RDS MySQL and PostgreSQL
    - use an authentication token obtained through IAM and RDS API calls
    - auth token has 15min lifetime
        - Benefits of using the auth token:
            - Network in/out must be encrypted using SSL
            - IAM to centrally manage users instead of DB 

    