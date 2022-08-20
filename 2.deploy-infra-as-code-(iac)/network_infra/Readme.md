# Network Infrastructure
## Workflow and Helpers
Examples r create.sh, update.sh files.  

![n1](n1.png?raw=true "n1")

The unidirectional directional arrows in the diagram above show the inbound requests and help you track the sequence of resource creation. The actual traffic flow would be bidirectional, with the following considerations:  

The NAT gateway serves as an intermediary to take a private resource's outbound request, connect to the Internet gateway, and then relay the response back to the private resource without exposing that private resource's IP address to the public.    

We will deploy the (publicly visible) load balancer in the same VPC having both public and private subnets. Note that *all resources within a VPC can connect to each other directly using the private IP address*. Therefore, the elastic load balancer can directly distribute the ingress requests across multiple targets VMs within the same VPC, even if the VMs are in a private subnet.  

Let's create the networking infrastructure first, such as, VPC, subnets, Internet gateway, NAT gateway, and route tables.  

![n2](n2.png?raw=true "n2")

### Learning about the YAML file
Format version: The AWSTemplateFormatVersion section is optional. The current valid value is 2010-09-09. You can add it to your file as:  
`AWSTemplateFormatVersion: 2010-09-09`  

Description: TheDescription field is also optional. Here we start by adding a short description of the project we are working on.  
`AWSTemplateFormatVersion: 2010-09-09`  
`Description: Carlos Rivas / Udacity - This template deploys a VPC`  

Resouces: Although a description is optional, the Resources section is required. Remember to include at least one resource (e.g., a VPC, an EC2 instance, a database) in the CloudFormation template, otherwise, it will give an error when you try to run the script.  

```
AWSTemplateFormatVersion: 2010-09-09
Description: Carlos Rivas / Udacity - This template deploys a VPC
Resources:
    UdacityVPC:
        Type: 'AWS::EC2::VPC'
        Properties:
            CidrBlock: 10.0.0.0/16
            EnableDnsHostnames: 'true'
```
### AWS command in a Shell script
As demonstrated in the video above, you can save your aws cloudformation command in a shell (.sh) script, so that you can run it multiple times easily. e.g create.sh  

### Practice Fixing Errors
Practice fixing errors, as this will help you prepare for real scenarios on the job.  

## VPC and Internet Gateway  
**Parameters** in a cloudformation template/script is used to pass value from json file into the cloudformation script. This helps to avoid hard coding values dt can chnge into d script.  

### Purpose of the network.yml and network-parameters.json files
We have already created a CloudFormation template (network.yml) and a properties file (network-parameters.json) that contains the code related to provisioning the networking infrastructure.  

The network.yml file contains four sections:  
**Description ** It presents a text description.  
Parameters - It contains the list of parameters that are being used in the current CloudFormation template. Parameters should be declared above your Resources. Any value that you consider to change in the future, put it as a parameter instead of hard-coding it into your script. Note that each parameter is further defined with the following properties (or fields):  
Parameter Name - You can provide the name of your choice  
Description - A textual value  
Type - Identifies the data type of the parameter, such as String or a Number  
Default (optional) - Presents the default value of the parameter  
AllowedValues (optional) - Presents the list of all possible values.  

You can also provide default values for parameters in case one was not passed in. e.g VpcCIDR has a default value of 10.0.0.0/16.  

The use of parameters in the template makes your CloudFormation templates more reusable, by allowing you to input custom values to your template each time you create or update a stack. These custom values can be defined in a separate JSON file. These parameters are referenced in the Resources and Outputs section using a !Ref intrinsic function.  















<a href="https://www.lucidchart.com/" target="_blank">Lucid</a>