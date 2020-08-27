# S3_Security

## Encryption for Objects
 - 4 methods of encrypting objects in S3
    - SSE-S3: keys are handeled and managed by S3
    - SSE-KMS: keys are managed by AWS Key Management Service
    - SSE-C: you handle keys
    - Client Side Encryption
 - SSE-S3 and SSE-KMS can be set as default for all files

## SSE-S3
 - SSE: server side encryption
 - AES-256 encryption type
 - Must set header: "x-amz-server-side-encryption":"AES256"

## SSE-KMS
 - KMS advantages:
    - user control
    - audit trail
 - Must set header: "x-amz-server-side-encryption":"aws:kms"

## SSE-C
 - S3 does not store the key you provide 
 - HTTPS must be used
 - Key must be provided in HTTP headers for every HTTP request made
 - Flow: Key + Object -> HTTPS -> S3 -> Encrypt Object -> Bucket -> Key discarded
 - not available through AWS console

## Client Side Encryption
 - Multiple options, one is the client library: Amazon S3 Encryption Client
 - Clients must encrypt data themselves before sending to S3, and decrypt when retrieving from S3
 - Customer fully manages keys and encryption cycle
 - Flow: Encrypted Object -> HTTP/HTTPS -> S3 -> Bucket

## Encrpytion in Transit (SSL/TSL)
 - S3 exposes both HTTP and HTTPS endpoints, but HTTPS is reccommended
 - Used by most clients by default 
 - Mandatory for SSE-C

## S3 Security
 - User Based
    - IAM policies - which API calls should be allowed for a specific user from IAM console
 - Resource Based
    - Bucket policies - bucket wide rules from the S3 console - allows cross account
    - Object Access Control List (ACL) - finer grain
    - Bucket Access Control List (ACL) - less common
 - An IAM principal can access an S3 object if the user IAM permissions allow it or the resource policy allows it and there is no specific deny

## S3 Bucket Policies
 - JSON based policies
    - Resources: buckets and objects
    - Actions: Set of API to Allow or Deny
    - Effect: Allow/Deny
    - Principle: The account or user to apply the policy to
 - Use S3 bucket for policy to:
    - Grant public access to the bucket
    - Force objects to be encrypted at upload 
    - Grant access to another account

## Block Public Access
 - Block public access to buckets and objects granted through
    - any access control lists
    - new access control lists
    - new public bucket or access points policies
 - Block public and cross-account access to buckets and objects through any public bucket or access point policies
 - Created to prevent company data leaks 

## Other Security Concepts
 - Supports VPC endpoints 
 - S3 Access Logs can be stored in S3 buckets
 - API calls can be logged in AWS CloudTrail
 - MFA Delete: MFA can be required to delete objects in versioned buckets
 - Pre-Signed URLs: URLs that are valid only for a limited time

## MFA Delete
 - To use MFA Delete, enable Versioning on S3 bucket
 - After enabled, will need it to
    - permanently delete an object version
    - suspend versioning on the bucket
 - Only bucket owner (root account) can enable/disable MFA-delete
 - can only be enabled using CLI