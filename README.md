# aws-infra
AWS Infrastructure which includes Web app + RDS + all the bits and pieces that make it highly available, secured, resilient, automated.

## Diagram

![Diagram](https://github.com/carloshz4/aws-infra/blob/master/AWS-Infra.jpg)


## Cloudformation template

The following CF template builds the architecture represented in the diagram above:

''
php-mysql-vpc.yml
''


## Explanation

The CF template:

1. Creates a basic php Web Site hosted on AWS with a backend mysql DB (using RDS). It basically automates the manual creating followed in this page:
![Php-mysql](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Tutorials.WebServerDB.CreateWebServer.html)
2. The web servers and DB are located on private networks and highly available.
3. The web servers launch as part of an autoscaling group and its setup and connection to the DB is done when booting up.
4. An application load balancer is used to distribute the traffic.
5. In terms of networking these elements are created to alocate the resources: VPC, Subnets, IGW, NAT GW, RT.
6. In terms of security SG were created with restricted ports, servers cannot be access directly from internet but via a bastion host.


## Pre-requisites

1. Make sure you have a key pair created in the Region where you'll launch your CF Stack.
2. Create a user with enough privileges to launch the stack along with the different objects.
3. At the moment the template has the list of AMIs for each region. This ids may change in the future and will have to be listed again and included in the template. This could potentially be automated somehow. To get that list run the script **getaims.sh** in this repo. Note it used AWS cli. You need to provide the AMI name for instance:
''./getaims.sh amzn-ami-hvm-2018.03.0.20200318.1-x86_64-gp2''

Note it's important to use an Amazon Linux AMI (generation I), otherwise the bootstrap script won't work.
