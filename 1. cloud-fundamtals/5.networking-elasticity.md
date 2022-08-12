-: Networking and Elasticity
This is abt letting internet user get access to ur site.
We'll also discuss tools required to configure and investigate 
network connectivity.

================================
-: Why do we need networking in the cloud?
Networks reliably carry loads of data around the globe allowing for 
the delivery of content and applications with high availability. 
*The network is the foundation of your infrastructure.*

Cloud networking includes:
network architecture
network connectivity
application delivery
global performance
delivery

Q: What is the address of a computer called?
IP(Internet Protocol)

DOMAIN NAME SYSTEM(DNS) asks a *domain authority* for d IP
address of the url, eg google.com, entered into browser.

Domain authority is the service with wc d domain name e.g
google.com was registered on.
================================
-: Route 53: routes end users to Internet applications
*Route 53 connects user requests to internet applications running 
on AWS or on-premises.*

Route 53 is a cloud DOMAIN NAME SYSTEM(DNS) service that has servers 
distributed around the globe used to translates human-readable names 
like www.google.com into the numeric IP addresses like 74.125.21.147.

Features
scales automatically to manage spikes in DNS queries
allows you to register a domain name (or manage an existing)
routes internet traffic to the resources for your domain
checks the health of your resources
It's nt used for website hosting

================================
-: Why do we need elasticity in the cloud?
With elasticity, your servers, databases, and application resources can 
automatically scale up (or vertically - by adding more RAM, CPU, or IO 
i.e resizing an instance to add more capacity) or scale down(or 
horizontally - by adding more servers) based on load.

================================
-: EC2 Auto Scaling
EC2 Auto Scaling is a service that monitors your EC2 instances and 
automatically adjusts by adding or removing EC2 instances based on 
conditions you define in order to maintain application availability 
and provide peak performance to your users.

Features
Automatically scale in and out based on needs.
Included automatically with Amazon EC2.
Automate how your Amazon EC2 instances are managed.

EC2 Auto Scaling adds instances only when needed, optimizing cost savings.

NB: AWS Autoscaling is diff from EC2 autoscaling bcos it involves
resources like autoscaling of DB, etc

Q: How could you know when EC2 Auto Scaling is launching or terminating 
an instance?
Via a messaging service like Simple Notification Service(SNS)

================================
-: EC2 - Create Auto Scaling group
EC2 Auto Scaling is a service that ensures you have the desired number 
of EC2 instances always up and running to handle the expected load for 
your application. To set-up an Auto Scaling group, you require the 
following basic details:

1. Count of instances - The desired count of the EC2 instances you want 
to have available. If any instance goes down/fails, a new instance 
automatically spins up.

2. Launch template - The auto scaling group contains a collection of 
EC2 instances that are treated as a logical group. All EC2 instances 
within a group share the same configuration. Therefore, You need to 
specify the configuration details, such as, the ID of the Amazon 
Machine Image (AMI), the instance type, a key pair, security groups, 
and the other parameters that you use to launch EC2 instances. You 
specify the configuration details in a Launch template.

3. Scaling policy - The auto scaling policy that defines how to 
scale your EC2 instances automatically, based on demand

A. Start the Auto Scaling Groups service
Search for Auto Scaling Group in AWS Console
Click Create Auto Scaling group btn

B. Create an Auto Scaling group
The Create Auto Scaling group is a seven-step process, as shown in the 
snapshot below. Provide a launch template or configuration in the first 
step. AWS prefers launch templates over launch configuration files. 
(Although, both convey similar information.) If you do not have a 
pre-created launch template, you can create a launch template from 
the current step.

C. Launch template
As mentioned above, a launch template specifies the configuration details, 
such as, the ID of the Amazon Machine Image (AMI), the instance type, a 
key pair, security groups, and the other parameters that you use to launch 
EC2 instances. 

================================
-: EC2 - Auto Scaling Group
Let's have a walkthrough of an Auto Scaling Group which has already 
been created.

A Launch Template 

Instance refresh
An instance refresh allows you to trigger a rolling replacement of all 
previously launched instances in the Auto Scaling group with a new group 
of instances.

================================
-: Elastic Load Balancing
Elastic Load Balancing automatically distributes incoming application 
traffic across multiple servers.

Elastic Load Balancer is a service that:
Balances load between two or more servers
Stands in front of a web server
Provides redundancy (if a server is lost, load bal split requests
to other working servers) and performance(if a server is having issues, 
lb will add more servers to d pool of available servers)

Elastic Load Balancing works with EC2 Instances, containers, IP addresses, 
and Lambda functions.
You can configure Amazon EC2 instances to only accept traffic from a 
load balancer.

================================
-: EC2 - Elastic Load Balancing
A. Prerequisite
Go to the EC2 dashboard. In order to use elastic load balancing, you will 
need to make sure that you've launched the EC2 instances that you plan to 
register with your load balancer.

You must have more than one EC2 instance in the running state.

B. Start the Load Balancer service
On the EC2 dashboard, select the Load Balancers service from the navigation 
pane on left. Here, you can view the list and details of existing load 
balancers.

Launch the Create Load Balancer wizard. AWS offers three types of load 
balancers.

1. Application Load Balancer (ALB)
A simple use case: Assume you are running a microservices-architecture 
based application. An Application Load Balancer allows you to host the 
different API endpoints of your application on different servers. The 
load balancer then redirects the incoming HTTP/HTTP traffic to the 
suitable server based on the rules you specify in the configuration.

If you choose this option, you will be taken to a six-step process:
Configure Load Balancer
Configure Security Settings
Configure Security Groups
Configure Routing
Register Targets
Review

https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html

2. Network Load Balancer (NLB)
A Network Load Balancer helps to balance the load on each individual 
server. Having an NLB becomes essential when your application requires 
handling millions of requests per second securely while maintaining 
ultra-low latencies.

This option has a five-step process:
Configure Load Balancer
Configure Security Settings
Configure Routing
Register Targets
Review

https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html

3. Classic Load Balancer (CLB)
It is a previous generation option. You can choose a Classic Load 
Balancer when you have an existing application running in the 
EC2-Classic network. You will have to follow a seven-step process 
to create a CLB:

Define Load Balancer
Assign Security Groups
Configure Security Settings
Configure Health Check
Add EC2 Instances
Add Tags
Review

https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/introduction.html

================================
-: EC2 - Lab NLB
In this hands-on exercise, you will learn to create a network load 
balancer (NLB), and see the role of an NLB.

An NLB serves as the single point of contact for clients and automatically 
distributes the incoming traffic uniformly across multiple targets. The 
targets are the EC2 instances within the same or different AZs.

Prerequisites:
An AWS account
A default VPC. It is a VPC in a default region and has a public subnet 
in each Availability Zone.

Prerequisite 1: A default VPC
Prerequisite 2: Subnets in each AZ in the default VPC. Also, notice that 
a common route table is attached to all subnets.

Prerequisite 3: A route table with a rule for internet facing communication. 
See that it requires an internet gateway

Step 1. Create the first EC2 instance
Create the first EC2 instance in a public subnet in any one Availability Zone.

Under the Advanced Details → User data section, add the following configuration 
script to run automatically during launch.

#!/bin/bash
sudo yum update -y
sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2
sudo yum install -y httpd mariadb-server
sudo systemctl start httpd
sudo systemctl enable httpd
sudo chkconfig httpd on

# Set file permissions for the Apache web server
sudo groupadd www
sudo usermod -a -G www ec2-user
sudo chgrp -R www /var/www
sudo chmod 2775 /var/www
find /var/www -type d -exec sudo chmod 2775 {} +
find /var/www -type f -exec sudo chmod 0664 {} +

# Create a new PHP file at  /var/www/html/ path
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php

The script above will install, configure, and launch the Apache webserver 
on the EC2 instance. You can learn more about the individual steps at 
Create an EC2 instance and install a web server.
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Tutorials.WebServerDB.CreateWebServer.html#CHAP_Tutorials.WebServerDB.CreateWebServer.Apache


Keep the storage as default, and use a tag as Name: Server-A

At the Configure Security Group step, you can create a new one, and ensure 
to have a firewall rule to allow incoming HTTP traffic on port 80.

Type	Protocol	Port	Source
HTTP	TCP	        80	    0.0.0.0/0
It will allow all IPv4 addresses to access your instance.

SSH	    TCP	        22	    0.0.0.0/0

The step above is crucial for the current experiment.

Generate and download a new key pair, at the last stage of the Launch 
Instance wizard.

Important: This key-pair will allow you to log into your instance, using 
SSH, from your local machine. Save the key-pair carefully, because the 
same private key cannot be re-generated.

Step 2. Create the second EC2 instance, in a separate Availability Zone
Launch the second EC2 instance using the same steps above, except for the 
following changes at the Configure Instance Details step:

Select another public subnet in a different AZ, say us-east-2b
Replace the last line of the user data (shell script) with
echo "<? echo "<h1>Welcome to server 2</h1>" ?>" > /var/www/html/phpinfo.php
Additionally, change the tag to Name: Server-B.

Step 3. Verify the Apache webserver installation
Confirm that the newly created EC2 instances are in the running state.

Verify that the Apache server is running successfully on both the EC2 
instances. Simply copy, and paste the public IPv4 address of each instance 
in a new browser window. If the Apache is configured successfully, you will 
see the Apache welcome page.

Note: We have opened the HTTP traffic on the default port, therefore the 
public IPv4 address should be prepended with http://, instead of https://.

Configuring the secure HTTPS on EC2 will add overhead to the current 
experiment, and you may deviate from the intent of learning an NLB.

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/SSL-on-amazon-linux-2.html

http://18.217.72.14

View the content of the PHP page that you configured using the shell script 
such as, http://18.218.185.145/phpinfo.php and http://18.217.72.14/phpinfo.php

Step 4. Create an NLB
Select the Load Balancers service on the left-hand side menu of the EC2 
dashboard, and click on the Create Load Balancer button.

You will be prompt to choose the type of load balancer: Application, Network, 
or Classical load balancer. Choose to create a Network Balancer.
At the first step, Configure Load Balancer, use the following basic 
configuration details

Section	                Field	            Value
Basic Configuration	    Name	            udacity-nlb
                        Scheme	            internet-facing

Availability Zones	    VPC	                Choose default-vpc
                        Availability Zones	Check the two where  
                                            you've launched the EC2 instances,
                                            such as us-east-2a and us-east-2b

Skip the Configure Security Settings step, by clicking the Next button.
At the Configure Routing step, use the following configuration details 
in the Target group section:
Field	        Value
Target group	New target group
Name	        UdacityNLBTarget
Target type	    Instance
Protocol	    TCP
Port	        80

At the Register Targets step, add the two EC2 instances created previously 
to the target group.

Do not forget to click on the `Add to registered button` after selecting the 
instances from the list.

Leave the remaining things as default, and finish creating the NLB.

Step 5. Test the NLB
You will be taken back to the Load Balancers dashboard. Copy the DNS name of 
the newly created NLB, and append the /phpinfo.php at the end of it. A sample 
DNS name appended with the file name looks like this:
http://udacity-nlb-f00b2cb9e62f5c2a.elb.us-east-2.amazonaws.com/phpinfo.php

Paste the copied DNS name to a new browser window and refresh the browser a 
few times, each after a few seconds. You will notice that sometimes the 
request is redirected to Server-A and other times, it is routed to Server-B.

The NLB is getting the output from the two different webservers. Notice that 
the DNS name (URL) is the same in the above two cases


Step 6. Delete the resources
Delete the NLB by going to the Load Balancer dashboard.
Stop and terminate the EC2 instances by going to the Instances dashboard.

================================
-: Lab - EC2 Auto Scaling
In this hands-on exercise, you will use Auto Scaling to automatically launch 
Amazon EC2 instances in response to the conditions you specify. You will also 
see auto-scaling in action as it automatically provisions replacement 
instance(s).

Definition: An Autoscaling group contains a collection of EC2 instances 
that share similar characteristics and are treated as a logical group.

All EC2 instances that are provisioned as a part of auto-scaling have the 
same configuration because they are instantiated from a Launch template. 

Preparatory Steps
Sign in to the AWS Management Console.
Navigate to the EC2 dashboard. In this exercise, we will use the following 
two services available in the EC2 dashboard:
Instances → Launch templates
Auto Scaling → Auto Scaling Groups

Stage 1. Create a Launch template
Definition: A Launch template specifies instance configuration information, 
such as, AMI ID, the instance type, a key pair, security groups, and the 
other parameters that you use to launch EC2 instances.

Go to the Launch templates service, and create a new template by specifying 
the following parameters:
Template name, and description of your choice.

Template contents:
AMI ID:             Amazon Linux 2 AMI (HVM), SSD volume type
Instance type:      t2.micro
Key-pair for logging in to the EC2 instances:       Your choice of key-pair
Network settings: Choose a Virtual Private Cloud (VPC), and a subnet in which 
the network interface is located. Choose a security group accordingly, because 
this step will ensure that a public IP address is assigned automatically to 
every instance.
Storage (volumes), tags, and network interfaces:    Default


Stage 2. Create an Autoscaling group
Go to the Auto Scaling Groups service, and create a new Autoscaling group. 
Creating an Autoscaling group is a multi-step process, in which you specify 
the configuration settings, group size, scaling policies (step/simple/target 
scaling policy), notifications, and tags. For this exercise, you have to 
specify the following minimal set of configurations:
Choose a Launch template that you have created in the previous step.
Provide the VPC, and subnets in which you want to create your EC2 instances.
Specify the Group size with the desired, minimum, and maximum capacity, i.e., 
count of EC2 instances at any given moment. You can choose the default value, 
1, for each capacity.
Use the default values in the remaining steps of this process


Stage 3. Verify your Autoscaling group
On the Auto Scaling Group dashboard, select the Autoscaling group that 
you have created in the step above.

Verify the details that were provided while creating the Autoscaling group.

Verify that the Autoscaling group has launched the desired number of EC2 
instance(s). The status of your instance(s) should be Successful, which 
means the instances are launched.

Verify that the instances have the desired lifecycle and health. Also, 
note the Instance ID for the next step.

Stage 4. Test Autoscaling group
In this step, you will terminate only those instance(s) that were launched 
as a part of the Autoscaling group. And, then we will verify if the 
Autoscaling group automatically launches new instances to maintain the 
desired number of running instances.

Note - In addition to the instances that are launched as a part of the 
Autoscaling group, it is possible that you have additional instances 
already created in your EC2 dashboard.

Go to the EC2 Instances dashboard, and select the instance(s) that you 
want to terminate.

Terminate the selected instance(s).
Go back to the Auto Scaling Group service and select the Autoscaling group 
that you have created in the step above.
While viewing the details of the Autoscaling group, review the history for 
the EC2 instance(s). You will see that the previous EC2 instance has been 
terminated, and a new one(s) are being instantiated.

Stage 5. Delete Autoscaling group resources
In order to avoid being billed unnecessarily, it is important to delete 
the resources provisioned during this exercise.

Come back on the Auto Scaling Group dashboard, and select the checkbox 
against the auto-scaling group you want to delete.
At the top of the screen, click the Delete option.

Tutorial:
https://aws.amazon.com/getting-started/hands-on/ec2-auto-scaling-spot-instances/?trk=gs_card#