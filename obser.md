EC2: Elastic Compute Cloud
VPC: Virtual Private Cloud

Elastic Block Store (EBS): you can think of EBS as an external hard drive that we attach to the server for additional storage. It helps with data 
persistence even when a server is terminated mking d data ready available
for the next server.

Elastic IP addresses- An Elastic IP address can mask the failure of an instance by remapping the current IP address to another instance in your account.

Load Balancer - A load balancer distributes the incoming traffic across multiple targets, such as EC2 instances in one or more Availability Zones.

EC2 Auto Scaling- It is a service that automatically launches/terminates EC2 instances based on user-defined scaling policies, scheduled actions, and health checks.

=========================================
Virtual Private Cloud (VPC)
Virtual Private Cloud or VPC allows you to create your own private network in the cloud. You can launch services, like EC2, inside of that private network. A VPC spans all the Availability Zones in the region.

VPC allows you to control your virtual networking environment, which includes:

IP address ranges
subnets
route tables
network gateways

You can store data in Amazon S3 and restrict access so that it’s only accessible from 
instances in your VPC.


