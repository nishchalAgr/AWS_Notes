# Auto_Scaling_Groups
 - in real life, the load on a website or application can change very quickly
 - ASGs address this issue by:
    - Scaling out (adding EC2 instances) to match an increased load
    - Scaling in (removing EC2 instances) to match a decreased load
    - Ensuring a max/min number of instances are always running
    - Automatically register new instances to a LB

## Important Attributes for an AWS ASG
 - A launch configuration
    - AMI + Instance type
    - EC2 user data
    - EBS volume 
    - Security Groups
    - SSH Key Pair
 - Min Size / Max size / Initial Capacity
 - Network + Subnet info
 - LB info
 - Scaling policies 

## ASG Alarms
 - A CloudWatch alarm monitors a metric (ex. Average CPU usage)
 - Metrics are computed for the overall ASG instances
 - Based on alarms, scale out/in policies cna be created

## New ASG Rules
 - New and better rules that are directly managed by EC2
    - Target Avg CPU usage
    - Number of requests on the ELB per instance
    - Avg network in/out
 - Easier to set up and make more sense

## ASG Custom Metrics
 - We can auto scale based on a custom metric also (ex. number of connected users)
    1. send custom metric from app in EC2 to CloudWatch (PutMetric API)
    2. create CloudWatch alarm to react to low/high values 
    3. use CloudWatch alarm as the scaling policy for ASG

## Other
 - ASGs can also operate on a schedule
 - To update and ASG, and new launch config/template must be provided
 - IAM roles attached to an ASG will apply to all underlying instances
 - ASGs are free
 - If an underlying instance gets terminated for whatever reason, the ASG will automatically create new ones as a replacement
    - An ASG can terminate and replace a instance that is pinged as unhealthy by an LB

# ASG Scaling Groups
 - Target Tracking Scaling
    - Easiest to set up
    - ex. I want the average ASG CPU usage to stay around 40%
 - Simple / Step Scaling
    - Uses CloudWatch alarms to give more control over when to scale in/out
 - Scheduled Actions
    - Scale in/out on a schedule
    - Useful when usage patterns are known

## Scaling Cooldowns
 - helps to ensure that ASG doesn't launch or terminate additional instances before the previous scaling takes effect
 - scaling-specific cooldowns override the default (300 sec)
     - scaling cooldowns can be shortened when paired with a scale-in policy

