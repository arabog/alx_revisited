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
**Description:** It presents a text description.  
**Parameters:** It contains the list of parameters that are being used in the current CloudFormation template. Parameters should be declared above your Resources. Any value that you consider to change in the future, put it as a parameter instead of hard-coding it into your script. Note that each parameter is further defined with the following properties (or fields):  
`Parameter Name` - You can provide the name of your choice  
`Description` - A textual value  
`Type` - Identifies the data type of the parameter, such as String or a Number  
`Default` (optional) - Presents the default value of the parameter  
`AllowedValues` (optional) - Presents the list of all possible values.  

You can also provide default values for parameters in case one was not passed in. e.g VpcCIDR has a default value of 10.0.0.0/16.  

The use of parameters in the template makes your CloudFormation templates more reusable, by allowing you to input custom values to your template each time you create or update a stack. These custom values can be defined in a separate JSON file. These parameters are referenced in the Resources and Outputs section using a !Ref intrinsic function.  
`Reference:` !Ref  

**Resources:** This (mandatory) section declares the AWS resources that you want to include in the stack, such as Servers, Gateways, VPN Connections, and more.  

Each resource is defined with the help of fields, such as Name, Resource type, and Resource properties.  
`Name` - It is a string value representing the resource name. You can use a name of your choice.  
`Resource type` - The resource type identifies the type of resource that you are declaring. For example, Type: AWS::EC2::VPC creates a VPC.  
`Resource properties` - The resource Properties field has further sub-fields that are specific to each type of resource.  

**Outputs:** This section declares output values for each resource that you can import into other stacks. For example, you can output the VPC ID for a stack to make it easier to find from another stack/template. You should not output any sensitive information, such as passwords or secrets. For each resource's output, you will have to provide the following:  
Description (optional) - A string  
Value (required) - The property returned by the aws cloudformation describe-stacks command.  
Export (optional) - The name of the resource output to be exported for a cross-stack reference.  

**Why do we need a separate parameter file (JSON)?**  
The separate parameter file (JSON) file helps us to avoid hard-coding the parameters in the template (YAML) file.  
Any named parameters in the Parameters section of our CloudFormation template will need to have a matching value in a separate, Parameter file, which is in JSON format.   
Having this additional file with actual parameter values allows you to change data used by your CloudFormation template without the risk of modifying the template directly and possibly introducing a typo or some logical error.  

**How to execute the Shell scripts?**  
You can run either of the shell scripts (create.sh or update.sh) as:
./<file_name> argument_1 argument_2 argument_3  
e.g: `./create.sh ourdemoinfra ourinfra.yml ourinfra.json`  

**Troubleshoot**
While running the AWS commands using either create.sh or update.sh file, if you face permission denied error, then you will have to grant the execute permission to the owner (yourself) explicitly as:  
`chmod +x update.sh`   
`chmod +x create.sh`   

### Connecting VPC's & Internet Gateways
Syntax of VPCGatewayAttachment resource: It's important to note when connecting an Internet Gateway to a VPC, we need to define an additional resource called InternetGatewayAttachment. This attachment references both the VPC and the InternetGateway.  

**InternetGatewayAttachment connect both VPC and Internet Gateway together! During the attachement, an IP address called Elastic IP is created wc is required by NAT Gateway to be able to communicate with internet on behalf of private subnets/infrastructural resources.**    


```
Type: AWS::EC2::VPCGatewayAttachment
Properties: 
    InternetGatewayId: String
    VpcId: String
    VpnGatewayId: String
```

Note that you must specify either InternetGatewayId or VpnGatewayId, but not both.  

## Subnets
![n3](n3.png?raw=true "n3")


```
 PrivateSubnet1: 
      Type: AWS::EC2::Subnet
      Properties:
          VpcId: !Ref VPC
          AvailabilityZone: !Select [ 0, !GetAZs '' ]
          CidrBlock: !Ref PrivateSubnet1CIDR
          MapPublicIpOnLaunch: false
          Tags: 
              - Key: Name 
                Value: !Sub ${EnvironmentName} Private Subnet (AZ1)

  PrivateSubnet2: 
      Type: AWS::EC2::Subnet
      Properties:
          VpcId: !Ref VPC
          AvailabilityZone: !Select [ 1, !GetAZs '' ]
          CidrBlock: !Ref PrivateSubnet2CIDR
          MapPublicIpOnLaunch: false
          Tags: 
              - Key: Name 
                Value: !Sub ${EnvironmentName} Private Subnet (AZ2)
```

Points to notice in the code above:  
!Ref VPC is referencing to the VPC created earlier.  

!Ref PrivateSubnet1CIDR is referencing to the PrivateSubnet1CIDR parameter. For this parameter, we have already defined the default value as 10.0.2.0/24. Similarly, the PrivateSubnet2CIDR parameter is being used in the above code.  

Notice that our private subnets are not sharing availability zones. We are keeping them separated as we displayed in our diagrams from the previous lesson. To do so, the !GetAZs‘’ function fetches the list of AZs in your region which are indexed 0, 1, etc. Then, the !select [0, !GetAZs‘’] returns only the first AZ.  
**Az is readily available when you create a VPC within a particular region**  

For PrivateSubnet1, the!Select [ 0, !GetAZs '' ] is returning the first AZ from the list of all AZs in your region. Similarly, for PrivateSubnet2, the !Select [ 1, !GetAZs '' ] will return the second AZ.  

Similar to the private subnets shown above, you will have to create two public subnets each in AZ0 and AZ1, except for the changed value in the field MapPublicIpOnLaunch: true. Marking this field as True will enable the Auto-assign public IP address field of the public subnet.  

## NAT Gateways
![n4](n4.png?raw=true "n4")

`Generally, we place a NAT gateway in a public subnet to enable the servers in a private subnet to connect to the Internet. And sometimes, we want to prevent the Internet from connecting to the servers in the private subnet`  

```
 NatGateway1EIP:
      Type: AWS::EC2::EIP
      DependsOn: InternetGatewayAttachment
      Properties: 
          Domain: vpc

  NatGateway2EIP:
      Type: AWS::EC2::EIP
      DependsOn: InternetGatewayAttachment
      Properties:
          Domain: vpc

  NatGateway1: 
      Type: AWS::EC2::NatGateway
      Properties: 
          AllocationId: !GetAtt NatGateway1EIP.AllocationId
          SubnetId: !Ref PublicSubnet1

  NatGateway2: 
      Type: AWS::EC2::NatGateway
      Properties:
          AllocationId: !GetAtt NatGateway2EIP.AllocationId
          SubnetId: !Ref PublicSubnet2
```

**You can use NAT Gateways in both your public and/or private subnets.?**  

### Elastic IP. 
![n5](n5.png?raw=true "n5")

This will give us a known/constant IP address to use instead of a disposable or ever-changing IP address. This is important when you have applications that depend on a particular IP address. NatGateway1EIP uses this type for that very reason.  

Use the DependsOn attribute to protect your dependencies from being created without the proper requirements. In the scenario above the **EIP allocation will only happen after the InternetGatewayAttachment has completed**.   

## Routing
![n6](n6.png?raw=true "n6")  

Before we proceed ahead, let's understand two terms:  
**Route table:** Routing is the action of applying rules to your network, VPC. A route table contains a set of rules. It blocks traffic from resources that do not follow the routing rule.   
**Rules:** Rules define the network protocol, allowed IP addresses, and ports to allow the inbound and outbound traffic separately. A single rule is called an **AWS::EC2::Route** resource.  

This section will create the following route tables (AWS::EC2::RouteTable) in our VPC and attach each of them to individual subnets, as mentioned below.  
PublicRouteTable - This route table will have a default rule (AWS::EC2::Route) to allow all outbound traffic routed to the internet gateway. Next, we will attach this route table (AWS::EC2::SubnetRouteTableAssociation) to both our public subnets.  

PrivateRouteTable1 - This route table will have a default rule (AWS::EC2::Route) to route all outbound traffic to the NAT gateway (NatGateway1). We will associate this route table to the PrivateSubnet1.  

PrivateRouteTable2 - This route table is similar in nature to PrivateRouteTable1, except that it is routing the traffic to the NatGateway2, and will be attached to the PrivateSubnet2.  

The flow of creating resources here will be: Create route tables → Add routes → Associate route table to subnets.  

Create route tables in your VPC, and then add routes (rules) to each route table. Later, associate the route table with individual subnets.  

The only required property for setting up a RouteTable is the VpcId.  
The default public route: the wildcard address 0.0.0.0/0, we are saying for any IP address in the world, send it to the referenced GatewayId.  

```
DefaultPublicRoute: 
      Type: AWS::EC2::Route
      DependsOn: InternetGatewayAttachment
      Properties: 
          RouteTableId: !Ref PublicRouteTable
          DestinationCidrBlock: 0.0.0.0/0
          GatewayId: !Ref InternetGateway
```
The default private route can be defined as:  
```
DefaultPrivateRoute1:
    Type: AWS::EC2::Route
    Properties:
        RouteTableId: !Ref PrivateRouteTable1
        DestinationCidrBlock: 0.0.0.0/0
        NatGatewayId: !Ref NatGateway1
```


### SubnetRouteTableAssociation
![n7](n7.png?raw=true "n7")  

In order to associate subnets with our route table, we will need to use a SubnetRouteTableAssociation resource.  

This only takes two properties, which are the id's used for our RouteTable and our Subnet.  
Important Note: Routes should be defined starting with the most specific rule and transitioning to the least specific rule.  


## Outputs
![n8](n8.png?raw=true "n8")  

Outputs are optional but are very useful if there are output values you need to:   
import into another stack  
return in a response  
view in AWS console  

To declare an Output use the following syntax:  
```
Outputs:
  Logical ID:
    Description: Information about the value
    Value: Value to return
    Export:
      Name: Value to export
```
The Value is required but the Name is optional. In the following example we are returning the id of our VPC as well as our Environment's Name:  
```
VPC: 
    Description: A reference to the created VPC
    Value: !Ref VPC
    Export:
        Name: !Sub ${EnvironmentName}-VPCID
```

### Join Function
You can use the join function to combine a group of values. The syntax requires you provide a delimiter and a list of values you want appended.  

In the following example we are using !Join to combine our subnets before returning their values:  
```
PublicSubnets:
    Description: A list of the public subnets
    Value: !Join [ ",", [ !Ref PublicSubnet1, !Ref PublicSubnet2 ]]
    Export:
        Name: !Sub ${EnvironmentName}-PUB-NETS
```



