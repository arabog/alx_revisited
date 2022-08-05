-: Why do we need security for applications?
Security In The Cloud
As adoption of cloud services has increased, so has the need for increased security in the cloud. The great thing about cloud security is that it not only protects data, it also protects applications that access the data. Cloud security even protects the infrastructure (like servers) that applications run on.

The way security is delivered depends on the cloud provider you're using and the cloud security options they offer.

=============================
-: AWS Web Application Firewall
A firewall is a network security mechanism dt monitors and
ctrls incoming and outgoing network traffic based on preset 
security rules.

WAF can protect websites not hosted in AWS through Cloud Front.

AWS WAF: It allows you to protect your web applications from common web exploits by monitoring and controlling the web requests coming to an Amazon API Gateway, an Amazon CloudFront distribution, or an Application Load Balancer.

AWS Shield: It provides continuous DDoS attack detection and automatic mitigations. AWS Shield offers two tiers of protection - Standard and Advanced.

AWS Firewall Manager: It allows you to configure and manage firewall rules across accounts and applications centrally.

Within AWS WAF service, you can create Web access control lists (web ACLs) to monitor HTTP(S) requests for AWS resources. You can protect the following types of resources:

CloudFront distributions
Regional resources (Application Load Balancer, API Gateway, AWS AppSync)
While creating a web ACL, you add rules, such as conditions like originating IP addresses, that determines whether to allow/block each request.

=============================
-: AWS Shield
AWS Shield is a managed DDoS (or Distributed Denial of Service) protection service that safeguards web applications running on AWS. AWS Shield offers two tiers of protection - Standard and Advanced.

Standard tier: Standard AWS Shield is a service that you get "out of the box", it is always running (automatically) and is a part of the free standard tier.
Advanced tier: If you want to use some of the more advanced features, you'll have to utilize the paid tier.

DDoS: overwhelm a website with requests to make it crash.

=============================
-: Identity and Access Management (IAM)





=============================



=============================
