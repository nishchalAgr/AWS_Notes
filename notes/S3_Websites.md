# S3_Websites
 - S3 can host static websites and have them accessible on the www
 - The website URL will be: 'bucket-name'.s3-website.'AWS-region'.amazonaws.com
 - To troubleshoot 403 error, make sure bucket policy allows public reads
 - General bucket policy: Allow s3.GetObject to everyone
    - It is reccommended that you never grant public access to a bucket unless its is for a website