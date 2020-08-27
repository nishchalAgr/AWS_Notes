# Route53-Overview
 - a managed DNS
 - DNS is a collection of rules and records which helps clients understand how to reach a server through its domain name
 - In AWS, the most common records are:
    - A: hostname to IPv4
    - AAAA: hostname to IPv6
    - CNAME: hostname to hostname
    - Alias: hostname to AWS resource
 - can use public domain names that you own or buy
 - can use private domain names that can only be resolved by instances in your VPC
 - features load balancing (through DNS - also called client load balancing)
 - features limited health checks
 - features multiple routing policy options:
    - simple
    - failover
    - geolocation
    - latency
    - weighted
    - multi-value
 - costs $0.50 per month per hosted zone

 ## DNS TTL
 - TTL: Time to live
 - When web browser sends a DNS request, it will get an IP and a TTL
 - The TTL tells the browser for how long it should keep the DNS response in cache
 - Increasing TTL lowers DNS traffic but increases the chance of the cache contained outdated records
 - In Route53, TTL is mandatory for each DNS record

 ## CNAME vs Alias
 - CNAME
    - Points hostname A to any other hostname B (ex. app.mydomain.com -> something.anything.com)
    - domain A must be non-root (ex. branch.root.com)
 - Alias
    - Points a hostname A to an AWS resource (ex. app.mydomain.com -> something.amazonaws.com)
    - domain A can be non-root or root
    - free of charge
    - native health check

 ## Simple Routing Policy
 - use when you need to redirect to a single resource
 - not compatible with health checks
 - if multiple values are given, user picks a random one

 ## Weighted Routing Policy
 - Controls the % of requests that go each specific endpoint
    - Route53 user assigns weight to each endpoint
 - compatible with health checks
 - use cases:
    - test 1% of traffic on a new app version
    - split traffic between two regions

 ## Latency Routing Policy
 - Redirects user to the server with the least latency 
 - latency is evaluated in terms of user to designated AWS region

 ## Failover Routing Policy
 - if health check fails, redirects to secondary instance

 ## Geo Location Routing Policy
 - routing purely on user location (continent or country)
 - default policy if there is a location match

 ## Multi Value Routing Policy
 - Use when routing to multiple resources
 - Want to associate a Route53 health check with records
 - Up to 8 healthy records are returned for each Multi Value query
 - not a substitued for an ELB
