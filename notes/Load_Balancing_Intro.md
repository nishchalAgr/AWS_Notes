# Load_Balancing_Intro
 - servers that _foward internet traffic_ to multiple downstream servers (EC2 instances)
 - allows only _one point point of access_ (DNS) to be exposed for the application
 - handles failures of downstream instances
 - preforms regular _"health checks"_ on instances
 - provides SSL termination (HTTPS) for websites
 - enforce stickiness with cookies
 - _high availability_ across zones
 - seperate public from private traffic

## ELB 
 - a _managed_ load balancer for EC2 instances
 - AWS guarantees it will be working
 - AWS takes care of upgrades, maintainance, high availability
 - AWS only provides only a few configuration knobs

## Health Checks
 - enable a load balancer to know if instances it forwards traffic to are _available to reply_ to requests
 - check is done on a port and route (usually /health)
 - instance is healthy if _200 response_ is returned

## Types of Load Balancers (AWS)
### Classic Load Balancer (v1 - old gen) - 2009
 - HTTP, HTTPS, TCP
 - Health checks are TCP or HTTP based
 - Fixed hostname XXX.region.elb.amazonaws.com
### Application Load Balancer (v2 - new gen) - 2016
 - HTTP, HTTPS, WebSocket
 - LB to multiple HTTP applications _across machines_
 - LB to multiple applications on the _same machine_ (ex. containers)
 - Routing tables to _different target groups_
    - Routing based on path in URL
    - Routing based on hostname in URL
    - Routing based on Query String, Headers
 - ALB are great for _micro-services_ and _container-based_ applications (ex. Docker and ECS)
    - Has port mapping feature to redirect to dynamic port in ECS
 - In comparison, multiple CLBs would be needed per application
 - Fixed hostname
### Network Load Balancer (v2 - new gen) - 2017
 - TCP, TLS, UDP
 - _v2 load balancers are usually reccommended_ as they have more features
 - internal (private) and external (public) options available
 - Can handle millions of requests per second
 - Lower latency ~ 100ms (vs 400 ms for ALB)
 - One static IP per AZ, supports elastic IPs
 - Good for extreme performance, but not included in free tier

## Basic Security
 - Security group on load balancer to allow public access from different protocols
 - Security group on application level to only allow access to load balancer

## Good-To-Know
 - Load Balancers can scale but not instantaneously
 - Troubleshooting
    - 4xx are client induced errors
    - 5xx are application induced errors
    - LB Error 503 means LB is at capacity or has no registered target
    - if LB can't connect to application, check security groups
 - Monitoring
    - ELB will log all access requests into access logs
    - CloudWatch Metrics provide aggregate stats
 
## Load Balancer Stickiness (ALB / CLB)
 - same client is always reconnected to the same instance behind a load balancer
    - prevents user from losing session data
 - cookie comes with a customized expiration date
 - stickiness can cause load imbalance

## Cross-Zone Load Balancing
 - each LB distributes evenly across all registered instances in all AZ
 - otherwise, each LB would only distribute traffic among instances in its own AZ


