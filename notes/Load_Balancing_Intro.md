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
 - Classic Load Balancer (v1 - old gen) - 2009
    - HTTP, HTTPS, TCP
 - Application Load Balancer (v2 - new gen) - 2016
    - HTTP, HTTPS, WebSocket
 - Network Load Balancer (v2 - new gen) - 2017
    - TCP, TLS, UDP
 - _v2 load balancers are usually reccommended_ as they have more features
 - internal (private) and external (public) options available

## Basic Security
 - Security group on load balancer to allow public access from different protocols
 - Security group on application level to only allow access to load balancer

