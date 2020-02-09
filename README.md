# aws-infra
AWS Infrastructure which includes Web app + RDS + all the bits and pieces that make it highly available, secured, resilient, automated.

## Requirements

1. Create a WordPress Web Site on hosted in AWS with a backend mysql/postgresql DB.
2. Make sure the Web/application and DB tiers are highly redundant/available and fault tolerant.
3. The DB servers should be to access the internet but incoming internet traffic to them should be blocked.
4. Provide the Web and DB instances logging and alarming via Cloudwatch (elaborate a bit more on this).
5. Generate email notifications once any of the hosts exceeds 90% CPU usage, it is termated or becomes unavailable.
6. Networking:
	- Use a VPC class B
	- Use multiple subnets class C
	- Use load Balancing
	- Restrict unnecesary ports and source IPs/networks. Only set up the minimun necesary
	- Consider GeoRedundancy
	- Restrict direct internet access to the hosts. 
7. Security:
	- Make sure only admin users can create, modify or delete infra.
	- Give infra read access mode to relavant services and infra.
	- Use roles when necessary.
	- If possible protect from DDOS and flooding attacks.
	- Monitor who makes changes to the infraestructure.


## Proposed architecture

