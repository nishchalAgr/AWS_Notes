# Security_Groups (ep22)

## Role of Security Groups
 - Security groups acts a firewall on EC2 instances
 - They regulate:
    - Port Access
    - IP Range
    - Control of inbound and outbound access

## Security Group Good-To-Know
 - If a security group blocks a request to connect, the EC2 instance will never see the request,
 basically the security group is outside of the instance
 - One can be attached to multiple instances, and one instance can have multiple security group
 - Good practice to maintain one seperate security group for SSH access, as it is the most complicated
 - Possible errors when an application is connecting to an instance:
    - if the connection times out, the issue is related to a security group
    - if the connection is refused, the issue is an application error
 - By default:
    - all inbound traffic is blocked
    - all outbound traffic is authorised

## Referencing Other Security Groups
- If security group A authorizes security group B and C, instance B and C can connect to instance A


## Public vs Private IP
- Public IP: 
    - Machine can be identified on the internet (WWW)
    - Must be unique across the whole web
    - Easy geo-location

- Private IP:
    - Machine can only be identified on _private network_
    - Must be unique across private network
    - Machines connect to WWW using NAT and gateway
    - Only specified range of IPs can be used as a private IP

- Elastic IP: 
    - When you stop and then start an EC2 instance, _it can change its public IP_ (not private)
    - Elastic IP provides a fixed public IP for an instance
    - You own an elastic IP as long as its not deleted
    - Can be attached to one instance at a time
    - If an instance fails, the elastic IP can be rapidly remapped to a working instance
    - 5 elastic IPs per account (to increase ask AWS)
    - not reccomended
        - Charges account when not associated with an instance
        - Elastic IPs point to a poor architecture
        - Better to use: 
            - a random public IP and register a DNS name
            - a load balancer
        