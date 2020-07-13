# EC2_Instance_Launch_Types
 - On demand instance: short workload
 - Reserved (MIN 1 year):
    - Reserved Instance: long workloads
    - Convertible Reserved Instances: long workloads with flexible instances
    - Scheduled Reserved Instances: ex. every Friday between 3 and 5pm
 - Spot Instances: short workload, cheap but can lose instances
 - Dedicated Instances: no other customers will share hardware
 - Dedicate Hosts: book entire physical server, control instance placement

 ## On Demand
 - Pay for what you use
 - _Highest cost_ but no upfront payment
 - No long term commitment
 - reccomended for _short-term, uninterrupted, unpredictable_ workload

 ## Reserved Instances
 - Up to _75% discount_ compared to On Demand pricing
 - Upfront cost with long term commitment (1 or 3 years)
 - Recommended for _steady state usage_ applications (ex. database)
 - Convertible Reserved Instance
    - can change the EC2 instance type
    - Up to _54% discount_ compared to On Demand
 - Scheduled Reserved Instance 
    - launch within time window you reserve

 ## EC2 Spot Instances
 - Up to _90% discount_ compared to On Demand pricing
 - Instances can be lost at any time if your max price is less than current spot price
 - Most _cost efficient_ of all instances
 - Useful for _low-priority_ and _resilient-to-failure_ workloads (ex. batch jobs, data analysis, img processing)
 - Popular combo: reserved instances for baseline, On-Demand + Spot for peak

 ## EC2 Dedicated Host
 - _Physical dedicated_ EC2 server for your use
 - _Full control_ of EC2 instance placement
 - Visibility into the underlying sockets/physical cores of the hardware
 - _3 year_ reservation 
 - More expensive
 - Useful for software with _complicated licensing models_ (BYOL) and for companies with _strong regulatory/compliance needs_

 ## EC2 Dedicated Instances
 - Instaces running on _hardware that is dedicated to you_
 - _No control_ over instance placement