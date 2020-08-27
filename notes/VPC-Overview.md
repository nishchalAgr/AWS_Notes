# VPC-Overview
 - Virtual Private Cloud
 - private network to deploy resources (regional)
 - Subnets allow you to partition your network within your VPC (AZ)
    - A public subnet is accessible from the internet
    - A private subnet is not accessible from the internet
 - route tables define access to the internet and between subnets

## Gateways
 - Internet gateways helps VPC instances connect with the internet
 - public subnets have a direct route to an internet gateway
 - NAT gateways (AWS-managed) and NAT instances (self-managed) allow your instances in your private subnets to access the internet while remaining private
    - NAT is placed in public subnet, and private subnet has route to NAT, which has a route to the internet through the public subnet

## NACL
 - Network ACL
 - A firewall attached at the subnet level, controls traffic to and from the subnet
 - Can have ALLOW and DENY rules, only with IP adresses
 - Default NACL in a VPC allows everything in and out

## Security groups
 - A firewall that controls traffic to and from an ENI / an EC2 instance
 - can only have ALLOW rules, but can include both IP and other security groups

- Flow: Internet -> Public Subnet -> NACL -> Security group -> EC2 instance

## VPC Flow Logs
 - Capture info about IP traffic going into your interfaces:
    - VPC 
    - Subnet
    - ENI
 - Helps to monitor and troubleshoot connectivity issues
 - Also captures network info from AWS managed interfaces
 - Log data can be sent to S3/Cloudwatch Logs

## VPC Peering
 - Connect two VPC, privately using AWS' network
 - Make them behave as if they were in the same network
 - Must not have overlapping CIDR
 - Not transitive 
    - ex. if A is connected to B, and A is connected to C, B and C are not necessarily connected
 
## VPC Endpoints
 - Endpoints allow you to connect to AWS services using a private network instead of a public www network
 - Gives enhanced security and lower latency to access AWS services
 - S3 and DynamoDB utilize VPC endpoint gateways, the rest use VPC endpoint interfaces (ENI)
 - Gateways are outside the private subnet, ENIs are inside the private subnet

## Site to Site VPN
 - Connect an on-premises VPN to AWS
 - The connection is automatically encrypted 
 - Goes over the public internet

## Direct Connect (DX)
 - Establish a physical connection between on-premises and AWS
 - Private, secure, and fast
 - Goes over private network
 - Takes at least a month to establish

- Site-to-site VPN and DX cannot access VPC endpoints