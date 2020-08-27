# S3_Performance

 - S3 automatically scales to high request rates, latency 100-200ms
 - can acheive at least 3,500 PUT/COPY/POST/DELETE and 5,500 GET/HEAD requests per second per prefix in a bucket
 - no limits to number of prefixes in a bucket 
    - prefix: anything between bucket and file name in object path
 - performance can be impacted by KMS limits (if SSE-KMS is enabled)
    - when an object is enabled, the GenerateDataKey KMS API is called
    - when an object is downloading, the Decrypt KMS API is called