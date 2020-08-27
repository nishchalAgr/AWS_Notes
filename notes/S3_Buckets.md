# S3_Buckets
 - S3 allows you to store objects(files) in buckets(directories) 
 - Buckets must have a globally unique name
 - While S3 is global, buckets are defined at a regional level
 - Naming convention
    - No uppercase
    - No underscore
    - 3-63 chars long
    - not an IP
    - must start with lowercase letter or number
 
## S3 Objects
 - Objects have a Key
    - The Key is the full path to the object within the bucket
    - The Key is composed of prefix + key
 - No concept of "directories" within buckets, just key names
 - Object "values" are the content of the body:
    - Max size is 5TB
    - If uploading more than 5TB, must use multi-part upload
 - Can have:
    - metadata
    - tags
    - version ID

## Versioning
 - Enabled at bucket level
 - Same key overwrite will increment version rather than overwriting existing file
 - Best practice
    - Protect against unintended deletes (ability to restore a version)
    - Easy roll back to previous version
 - Suspending versioning does not delete previous versions
 - Files added to bucket before versioning was enabled will have a version ID of null
 - Deleting a versioned file without version showing will add a delete marker as the latest version of the file, but not actually delete any versions of the file 
    - To actually delete a version of a file, delete it with versions showing

## Replication
 - Must enable versioning on both source and destination
 - Cross Region Replication use cases
    - compliance
    - lower latency access
    - replication across accounts
 - Same Region Replication use cases
    - log aggregation
    - live replication between production and test accounts
 - Buckets can be in different accounts
 - Asynchronous (but very fast)
 - After activating, only new objects are replicated 
 - Delete markers or deleting source (w/ a version ID) are not replicated
 - No chaining of replication