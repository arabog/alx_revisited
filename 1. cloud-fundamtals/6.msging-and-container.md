-: Why do we need messaging in the cloud?
Messaging in the Cloud
There are often times that users of your applications need to be notified when certain events happen. Notifications, such as text messages or emails can be sent through services in the cloud. The use of the cloud offers benefits like lowered costs, increased storage, and flexibility.

-: Simple Notification Service (SNS)
Amazon Simple Notification Service (or SNS) is a cloud service that allows you to send notifications to the users of your applications. SNS allows you to decouple the notification logic from being embedded in your applications and allows notifications to be published to a large number of subscribers.
Features
SNS uses a publish/subscribe model.
SNS can publish messages to Amazon SQS queues, AWS Lambda functions, and HTTP/S webhooks.

-: Why do we need queuing technology?
Queues
A queue is a data structure that holds requests called messages. Messages in a queue are commonly processed in order, first in, first out (or FIFO). ds involves asynchronous processing.

Messaging queues improve:
performance
scalability
user experience

-: Simple Queue Service (SQS)
Amazon Simple Queue Service (SQS) is a fully managed message queuing service that allows you to integrate queuing functionality in your application. SQS offers two types of message queues: standard and FIFO.
FIFO queues guarantee the ordering of messages.
Standard queues offer best-effort ordering but no guarantees.
Features
send messages
store messages
receive messages


-: Why do we need containers?
A container is an isolated process that consists of the following items, all bundled into one package:
the application code,
the required dependencies (e.g. libraries, utilities, configuration files), and
the necessary runtime environment to run the application.

Each container is an independent component that can run on its own and be moved from environment to environment.

Benefit of Containers
Containers make it easier for developers to create, deploy, and run applications on different hardware and platforms, quickly and easily.
Containers share a single kernel and share application libraries.
Containers cause a lower system overhead as compared to Virtual Machines.
How to create containers?
Several platforms (called Container runtime/engines) allow us to create containers. A few such platforms are:
Docker
CRI-O
OpenVZ
Containerd

Docker Containers versus Virtual Machines
There are several benefits of using Containers over VMs:

Size: Containers are much smaller than Virtual Machines (VM) and run as isolated processes versus virtualized hardware. VMs can be in GBs while containers are in MBs.

Speed: Virtual Machines can be slow to boot and take minutes to launch. A container can spawn much more quickly typically in seconds.

Composability: Containers are designed to be programmatically built and are defined as source code. Virtual Machines are often replicas of a conventional computer system.

2. Docker
Docker is a (container runtime) tool that helps to build, test, and run containers. You can build containers locally using a command-line utility, Docker Desktop. If there are multiple containers running individual services of an application, you will need to use Docker Compose utility to specify dependent relationships between containers.

3. Docker Image
An image (or Docker image) is a portable auto-generated template that contains a set of instructions to create a container. An image can be instantiated multiple numbers of times to create multiple containers.

4. Dockerfile
A text file containing commands to create an image. In other words, Docker generates images by reading the commands from a Dockerfile.

https://www.docker.com/resources/what-container/

-: Elastic Container Service (ECS)
ECS is an orchestration service used for automating deployment, scaling, and managing of your containerized applications. ECS works well with Docker containers by:

launching and stopping Docker containers
scaling your applications
querying the state of your applications

Docker is the only container-runtime platform supported by Amazon ECS. Other container-runtime tools available in the insdustry are Rocket, LXD, OpenVZ, any a few more.

Before we move on to the demonstrate AWS ECS, make sure to have a glance at Docker basics for Amazon ECS
https://docs.aws.amazon.com/AmazonECS/latest/developerguide/create-container-image.html

*What is Amazon Elastic Container Service?*
Amazon Elastic Container Service (Amazon ECS) is a highly scalable and fast container management service. You can use it to run, stop, and manage containers on a cluster. With Amazon ECS, your containers are defined in a task definition that you use to run an individual task or task within a service. In this context, a service is a configuration that you can use to run and maintain a specified number of tasks simultaneously in a cluster. 

Containers r inside cluster. A cluster is a set of container instances running d 
container agents/applications(eg web app)


Launch types
There are two models that you can use to run your containers:
Fargate launch type - This is a serverless pay-as-you-go option. You can run containers without needing to manage your infrastructure.

EC2 launch type - Configure and deploy EC2 instances in your cluster to run your containers.

The Fargate launch type is suitable for the following workloads:
Large workloads that need to be optimized for low overhead
Small workloads that have occasional burst
Tiny workloads
Batch workloads

The EC2 launch type is suitable for the following workloads:
Workloads that require consistently high CPU core and memory usage
Large workloads that need to be optimized for price
Your applications need to access persistent storage
You must directly manage your infrastructure

Access Amazon ECS
You can create, access, and manage your Amazon ECS resources using any of the following interfaces:

AWS Management Console — Provides a web interface that you can use to access your Amazon ECS resources.

AWS Command Line Interface (AWS CLI) — Provides commands for a broad set of AWS services, including Amazon ECS. 


AWS Copilot — Provides an open-source tool for developers to build, release, and operate production ready containerized applications on Amazon ECS. 

Amazon ECS CLI — Provides a command line interface for you to run your applications on Amazon ECS and AWS Fargate using the Docker Compose file format. You can quickly provision resources, push and pull images using Amazon Elastic Container Registry, and monitor running applications on Amazon ECS or Fargate. You can also test containers that are running locally along with containers in the Cloud within the CLI. 

*Creating a container image for use on Amazon ECS*
Amazon ECS uses Docker images in task definitions to launch containers. Docker is a technology that provides the tools for you to build, run, test, and deploy distributed applications in containers. Docker provides a walkthrough on deploying containers on Amazon ECS


*Use containers to Build, Share and Run your applications*
https://www.docker.com/resources/what-container/
Package Software into Standardized Units for Development, Shipment and Deployment

A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. 
A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

Container images become containers at runtime and in the case of Docker containers – images become containers when they run on Docker Engine. 

Containers isolate software from its environment and ensure that it works uniformly despite differences for instance between development and staging.

Docker containers that run on Docker Engine r:
Standard: Docker created the industry standard for containers, so they could be portable anywhere

Lightweight: Containers share the machine’s OS system kernel and therefore do not require an OS per application, driving higher server efficiencies and reducing server and licensing costs

Secure: Applications are safer in containers and Docker provides the strongest default isolation capabilities in the industry

CONTAINERS
Containers are an abstraction at the app layer that packages code and dependencies together. Multiple containers can run on the same machine and share the OS kernel with other containers, each running as isolated processes in user space. Containers take up less space than Virtual Machines VMs (container images are typically tens of MBs in size), can handle more applications and require fewer VMs and Operating systems.

Environment: production and deployment environments

*Demo - Elastic Container Service*
How does Amazon ECS helps?
Assume you have a multi-container application that you want to run on the cloud. You may also require to scale the containers automatically based on the incoming traffic in such a case.

Amazon ECS deploys, manages, and scales containers based on your resource needs and supports other AWS services like Elastic Load Balancing, EC2 security groups, EBS volumes, and IAM roles.

Key terms related to Amazon ECS
1. Task definition
A task definition describes the application requirements concerning containers, such as the max amount of total CPU and memory used for the task (not for the individual container) and container definitions.

ECS offers to create a task definition using either the AWS Fargate or AWS EC2. AWS Fargate is priced based on the task size, whereas the EC2 service is priced based on computing resource usage.

2. ECS cluster
A cluster is a set of containers running task requests within an AWS region. A default cluster gets created when you create and run your first task definition.
3. Container agent
It is a utility that connects container instances to one of your clusters. Each container instance runs a container agent.
4. Container instance
A container instance is an EC2 instance that is registered into any of your ECS clusters.













