# Scalability_Concepts_Notes

## Scalability
 - Scalability refers to the ability of a system to handle greater loads by adapting
 - Two kinds:
    - Vertical
        - _increase the size_ of the instance
            - ex. upgrade t2.micro to t2.large
        - usually, databases scale vertically
        - vertical scaling has a hardware limit
    - Horizontal (elasticity)
        - _increase number_ of instances
        - implies _distributed system_
        - cloud offerings like EC2 make modern horizontal scaling easy

## High Availability
 - System runs in _at least two data centers_ (ex. AZs)
 - Goal is to survive a data center loss
 - Can be passive (ex. RDS Multi AZ)
