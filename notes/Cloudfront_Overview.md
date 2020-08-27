# Cloudfront_Overview
 - Content Delivery Network (CDN)
 - Improves read performance, content is cached at the edge
 - 216 Point of Presence globally currently (edge locations)
 - DDoS protection, integration with Sheild, AWS Web Application Firewall
 - Can expose external HTTPS and can talk to internal HTTPS backends

## Origins
 - S3 Bucket
    - Distribute files and cache them at edge
    - Enhanced security with CloudFront Origin Access Identity (OAI)
    - CloudFront can be used as an ingress (to upload files to S3)

 - Custom Origin (HTTP)
    - Application Load Balancer 
    - EC2 instance 
        - ALB or EC2 would need to be public and allow public IP of Edge Locations
        - For EC2 to be private, use an ALB in public
    - S3 website 
    - Any HTTP backend

## Geo Restriction
 - Whitelist/backlist to allow/prevent users from certain countries
 - "Country" is determined using a 3rd party Geo-IP database

## CloudFront vs S3 CRR
 - CloudFront:
    - Global Edge network
    - Files are cached for a TTL (ex. a day)
    - Great for static content that must be globally available

 - S3 CRR:
    - Must be setup for each you want replication to happen
    - Near real-time file updates
    - Read-only
    - Great for dynamic content that needs to be availble at low-latency in a few regions

## Caching 
 - Cache based on 
    - Headers
    - Session Cookies
    - Query String Parameters
 - Cache lives at each CloudFront Edge Location
 - Goal is to maximize cache hit rate to minimize requests on origin
    - Control the TTL (0 sec - 1 yr) through Cache-Control header or Expires header
    - Can invalidate part of cache using CreateInvalidation API
    - Seperate cache for dynamic and static requests

## HTTPS
 - Viewer Protocol Policy:
    - Redirect HTTP to HTTPS
    - Or use HTTPS only 
 - Origin Protocol Policy:
    - HTTPS only 
    - Or Match Viewer
    - Note: S3 "Websites" do not support HTTPS

## Signed URLs / Signed Cookies
 - ex. you want to distribute paid shared content to users around the world
 - Attach a policy with:
    - URL expiration
    - IP ranges to access data from
    - Trusted signers (which AWS accounts can create signed URLs)
 - URL can have TTL of minutes to years
 - Signed URL allows access to individual files, while signed cookies allow for access to multiple files
 - Flow: User connects to our authenticator application, which uses the AWS SDK to generate a 
 CloudFront signed URL, which is then returned to the user and can be use to access the S3 bucket through an edge location, which is connected to the bucket through OAI

## CloudFront Signed URL vs S3 Signed URL
 - CloudFront Signed URL:
    - Allow access to a path regardless of origin 
    - Account wide key-pair, only the root can manage it 
    - Can filter by IP, path, expiration
    - Can leverage caching
 - S3 Signed URL:
    - Issue a request as the person who pre-signed the URL
    - Uses the IAM key of the signing IAM principle 
    - Limited lifetime
