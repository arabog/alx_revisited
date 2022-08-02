Elastic Block Store (EBS): you can think of EBS as an external hard drive that we attach to the server for additional storage. It helps with data persistence even when a server is terminated mking d data ready available for the next server.

Elastic IP addresses- An Elastic IP address can mask the failure of an instance by remapping the current IP address to another instance in your account.

Load Balancer - A load balancer distributes the incoming traffic across multiple targets, such as EC2 instances in one or more Availability Zones.

EC2 Auto Scaling- It is a service that automatically launches/terminates EC2 instances based on user-defined scaling policies, scheduled actions, and health checks.

=========================================
Virtual Private Cloud (VPC) allows you to create your own private network in the cloud. You can launch services, like EC2, inside of that private network. A VPC spans all the Availability Zones in the region.

VPC allows you to control your virtual networking environment, which includes:
IP address ranges
subnets
route tables
network gateways

You can store data in Amazon S3 and restrict access so that it’s only accessible from 
instances in your VPC.

Q: What can a VPC protect?
Data stored on AWS S3
AWS EC2 instances

Subnets - It represents a subset of your VPC, i.e., a range of IP addresses from the CIDR (classless inter-domain routing) block allocated to your VPC. Subnets of a VPC can be present in different AZs.

Route tables - These are the set of RULES, called routes, that determine to which IP address the network traffic should be directed.

Internet gateways - If any of your resources within your VPC wants to communicate to the internet, then you must attach an internet gateway to your VPC. The internet gateway enables the communication between resources in your VPC and the internet.

The IP address in the VPC follows a classless inter-domain routing (CIDR) block of IP addresses. You will have to specify the IPv4/IPv6 CIDR block to be allocated to the VPC. In the snapshot above, it uses an IPv4 10.0.0.0/16 block, which allocates 2^(32-16) = 65,536 IP addresses. A few IP addresses are reserved, so you get 65531 IP addresses for further allocation.

You will have to specify the range of IP address from the allocated CIDR block for each subnet. In the example above, the public subnet has been allotted the 10.0.0.0/24 range, which comprises 2^(32-24) = 256 IP addresses. But, again a few IP addresses are reserved, so you get 251 available for resources in that subnet.

According to AWS, for  IPv4 CIDR block, the block sizes must be between a /16 netmask and /28 netmask. AWS provides a fixed size (/56) IPv6 CIDR block. AWS doesn't allow choosing the range of IPv6 addresses for the CIDR block.

Similarly, for the private subnet in the snapshot above, you will get 251 (/24) IP addresses.

Flow logs tab- The flow logs allow you to capture details about the IP traffic going to/from the network interfaces in your VPC.

Network ACL- A network access control list (ACL) defines the set of firewall rules for controlling traffic coming in and out of subnets in your VPC.

Inbound/Outbound rules are numbered and ordered. The lowest numbered rule is evaluated first. In other words, the incoming/outgoing traffic to/from a given subnet follows the rules mentioned in the associated network ACL.

Network ACLs are stateless in nature. Assume an inbound request arrived in your subnet. A "response" to the inbound request can only be sent out of the subnet if the outbound rules allow the outgoing traffic to the desired destination. A vice-versa scenario is also possible.

Rule with 0.0.0.0/0 source will allow all IP
addresses to access your instance.

EC2: Elastic Compute Cloud - is a service that provides servers for rent in the cloud.
dy r phy server in AWS AZs

Pricing Options
There are several pricing options for EC2.
On Demand - Pay as you go, no contract.

Dedicated Hosts - You have your own dedicated hardware and 
don't share it with others.

Spot - You place a bid on an instance price. If there is 
extra capacity that falls below your bid, an EC2 instance 
is provisioned. If the price goes above your bid while the 
instance is running, the instance is terminated.

Reserved Instances - You earn huge discounts if you pay up front 
and sign a 1-year or 3-year contract.

=======================================
-: Lambda
AWS Lambda provides you with computing power in the cloud by allowing you 
to execute code without standing up or managing servers.

The code you run on AWS Lambda is called a “Lambda function.”
Lambda  is a serverless computing technology

AWS Lambda
Run code without thinking about servers or clusters

AWS Lambda is a serverless, event-driven compute service that lets you run code for 
virtually any type of application or backend service without provisioning or managing 
servers. You can trigger Lambda from over 200 AWS services and software as a service 
(SaaS) applications, and only pay for what you use.

-: Elastic Beanstalk - is an orchestration service that allows you to deploy a web application 
at the touch of a button by spinning up (or provisioning) all of the services that you 
need to run your application.

While launching the environment and deploying EC2 instances to run your application, the following resources get created automatically:

Amazon S3 storage bucket
A target group in the default VPC
Multiple security groups
An autoscaling launch configuration and an autoscaling group
Multiple EC2 instances
Multiple CloudWatch alarms
EC2 load balancer You can even see the logs of each event (success and failure) after the creation of the environment. 



