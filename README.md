# aws-infra
AWS Infrastructure which includes Web app + RDS + all the bits and pieces that make it highly available, secured, resilient, automated.

## Requirements

1. Create a WordPress Web Site on hosted in AWS with a backend mysql (or postgresql) DB.
2. Make sure the Web/application and DB tiers are highly redundant/available and fault tolerant.
3. The DB servers should be to access the internet but incoming internet traffic to them should be blocked.
4. Provide the Web and DB instances logging and alarming via Cloudwatch (elaborate a bit more on this).
5. Generate email notifications once any of the hosts exceeds 90% CPU usage, it is termated or becomes unavailable.
6. Networking:
	- Use a VPC class B
	- Use multiple subnets class C
	- Use load Balancing
	- Restrict unnecesary ports and source IPs/networks. Only set up the minimun necesary
	- Consider Location Redundancy
	- Restrict direct internet access to the hosts. 
7. Security:
	- Make sure only admin users can create, modify or delete infra.
	- Give infra read access mode to relavant services and infra.
	- Use roles when necessary.
	- If possible protect from DDOS and flooding attacks.
	- Monitor who makes changes to the infraestructure.


## Proposed architecture

![Diagram](https://github.com/carloshz4/aws-infra/blob/master/AWS-Infra.jpg)



## Solution

Besides what is clear in the diagram, the proposed solution will consider:

**Networking and Security**:
- Routes and Routing tables.
- Restrict unnecessary incoming traffic via Security Groups and Network Access Control Lists.
- Provide egress (only) internet access to the ec2 and RDS instances via NAT GW.
- Provide ssh access to the EC2 instances only via Bastion host.
- Protection from DDOS and flooding attacks via AWS Shield and WAF.
- Enable Cloudtrail to monitor the activity of the IAM users.

**General functionalities**:
- Web instances part of the Auto Scaling Group will have a minimum of one instance per Availability Zone.
- A first image of the Web instance may be required to define the launch template of the autoscaling group.

**Automation**:
Most of the creation of the whole infra will be automated via Cloudformation. Some manual steps may be required as prerequisites to later create the Cloudformation stack. More details as the project progresses.
