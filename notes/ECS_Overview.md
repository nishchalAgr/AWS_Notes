# ECS_Overview

## Docker
- platform to deploy apps
- packaged in containers that can be run on any OS
- apps run the same regardless of where they are run
- Docker images are stored in repositories:
    - Public: Docker Hub
        - Find base images for many technologies or OS
    - Private: Amazon ECR (Elastic Container Registry)

## ECS Clusters
 - Logical grouping of EC2 instances
 - EC2 instances run on the ECS agent (Docker container)
 - The ECS agents register the instance to the ECS cluster
 - The EC2 instances run a special AMI made specifically for ECS
 - Comes with an ASG containing the EC2 instances

## ECS Task Definitions 
 - JSON metadata that tells ECS how to run docker
 - Information contained:
    - Image name
    - Port binding for Container and Host
    - Memory and CPU required 
    - Environment vars
    - Networking info

## ECS Service with Load Balancer
 - If we want to increase number of tasks, each container port will have be mapped to a different and random port. To allow us to still connect to these containers, we can use a load balancer with dynamic port forwarding (which is not included in CLB)

## ECR 
 - Private docker repo with your AWS account
 - Access is controlled by IAM policies
 - CLI v1 login: $(aws ecr get-login --no-include-email --region)
    - run output of above command
 - CLI v2 login: aws ecr get-login-password --region | docker login --username AWS --password-stdin 1234567890.dkr.ecr.region.amazonaws.com
    - pipes password into second part of the command to login
 - Docker CLI:
    - docker push 1234567890.dkr.ecr.region.amazonaws.com/demo:latest
    - docker pull 1234567890.dkr.ecr.region.amazonaws.com/demo:latest

## IAM 
 - EC2 Instance Profile
    - Used by ECS agent
    - Makes API calls to ECS service
    - Send container logs to CloudWatch Logs
    - Pull Docker image from ECR
 - ECS Task Role
    - Allow each task to have a specific role with minimum permissions
    - Use different roles for different AWS services you run
    - Defined in Task Definition

## Task Placement
 - When a new task is launched, ECS must determine where to place with the constraints of memory, CPU, and available port
 - When a service scales in, ECS needs to determine which task to terminate
 - Task placement strategies and constraints are used to assist with this
    - Not available with Fargate
 - ECS uses the following process to select container instances to place tasks:
    1. Satisfy CPU, memory, and port availability
    2. Satisfy task placement constaints
    3. Satisfy task placement strategies
 - Task Placement Strategies
    - Binpack
        - Place tasks on the minimum amount of CPU or memory
        - saves cost by minimizing number of EC2 instances in use by maximizing tasks per instance
    - Random
        - Places tasks randomly
    - Spread
        - Place tasks evenly based on the specified value
            - ex: instanceId, attribute:ecs.availability-zone
            - ex: first task on AZ1, second task on AZ2, third task on AZ3, and so on
    - Can be mixed together
        - ex: spread on AZ, binpack on memory 
 - Task Placement Constraints:
    - distinctInstance: place each task on a different container instance
    - memberOf: places task on instances that satisfy an expression
        - Uses Cluster Query Language
        - ex: attribute:ecs.instance-type =~ t2.*

## Auto Scaling
 - For service auto scaling, same options as ASG
 - Fargate Auto Scaling is easier to set up     