# PHP and MYSQL infra 
AWS Infrastructure which includes Web app + RDS + all the bits and pieces that make it highly available, secure, resilient, automated.

## Diagram

![Diagram](https://github.com/carloshz4/aws-infra/blob/master/AWS-Infra.jpg)


## Cloudformation template

The following CF template builds the architecture represented in the diagram above:

```
![php-mysql-vpc.yml](https://github.com/carloshz4/aws-infra/blob/master/php-mysql-vpc.yml)
```


## Explanation

The CF template:

1. Creates a basic php web site hosted on AWS with a mysql DB backend (using RDS). It basically automates the manual creation followed in this page:
[Php-mysql](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Tutorials.WebServerDB.CreateWebServer.html)
2. The web servers and DB are provisioned on private networks considering high availability and fault tolerance.
3. The web servers launch as part of an autoscaling group and its setup and connection to the DB is done during bootstrapping.
4. An application load balancer is used to distribute the traffic.
5. In terms of networking the following elements are created to alocate the web servers and DBs: VPC, Subnets, IGW, NAT GW, RT.
6. In terms of security SG were created with restricted ports, servers cannot be access directly from internet but via a bastion host.
7. On the Outputs you can directly access the link to the SamplePage.php. Just give it some minutes, don't try to reach it right after the stack was created.


## Pre-requisites

1. Make sure you have a key pair created in the Region where you'll launch your CF Stack and provide it as a parameter input.
2. Create a user with enough privileges to launch the stack along with the different objects.
3. At the moment the template has the list of AMIs for each region. These AMI IDs may change in the future and will have to be listed again and included in the template. This could potentially be automated somehow. To get that list run the script **getaims.sh** included this repo (which is a modification of [this one](http://www.scalingbits.com/aws/cloudformation/amiids)). Note it uses AWS cli. You need to provide the AMI name, for instance:
```./getaims.sh amzn-ami-hvm-2018.03.0.20200318.1-x86_64-gp2```
Note it's important to use an Amazon Linux AMI (generation I), otherwise the bootstrap script won't work.
