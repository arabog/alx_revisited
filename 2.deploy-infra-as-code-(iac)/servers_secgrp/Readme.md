# Lesson Objectives
In particular, we will create the following resources using the CloudFormation template:  
**Security groups** - Security group specify firewall rules. We will create two of them, one for a load-balancer and another for a web server.  
**AutoScaling group** - An autoscaling group ensures that a desired number of servers (EC2 instances) are always up and running. If an instance goes down due to any reason, such as bad health, a substitute instance with a similar configuration will spin up automatically.  
**Launch configuration** - The configuration of the EC2 instance that spins up automatically, if required, as a part of autoscaling group resides in a launch configuration.  
**Load balancer** - A load balancer distributes the incoming traffic uniformly across multiple servers (target group) within the same or different AZs. We will also create a listener and target group for the load balancer.  

