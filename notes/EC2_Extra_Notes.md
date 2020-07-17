# EC2_Extra_Notes

## EC2_Pricing
 - EC2 instances prices (per hour) varies on following parameters:
  - region
  - instance type
  - OS of the instance
 - Billed per second, min of 60 seconds
 - You do not pay for stopped instances

## Custom AMIs
 - Advantages of a custom AMI:
  - Pre-installed packages
  - Faster boot time (no need for EC2 user data)
  - More control over security 
  - More control over maintainance of the AMI
  - Out of the box Active Directory Integration
  - Installing apps ahead of time
  - Using someone else's custom AMI that fits your needs