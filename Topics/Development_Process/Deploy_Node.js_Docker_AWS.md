# Node.js Deployment through Docker and AWS

## Overview
In the realm of modern software development, containerization has become a standard practice for deploying applications. Docker simplifies this process by packaging applications and their dependencies into containers, ensuring consistency across various environments. Node.js, a popular JavaScript runtime, is often used to build scalable and efficient server-side applications.

AWS (Amazon Web Services) provides a suite of cloud services that enable developers to deploy and manage applications easily. ECS (Elastic Container Service) and ECR (Elastic Container Registry) are two fundamental services offered by AWS to manage containers and container images, respectively.

## Tech Stack

Docker: Docker is a platform that allows you to package an application and its dependencies into a standardized unit called a container. It provides isolation, portability, and scalability for applications. It allows for easy deployment as it essentially creates a separate virtual machine to run the application on.

Node.js: Node.js is a JavaScript runtime environment which is built on Chrome's V8 JavaScript engine. It enables developers to run JavaScript code on the server-side, making it ideal for building scalable network applications.

Amazon ECS (Elastic Container Service): ECS is a fully-managed container orchestration service provided by AWS. It allows you to run, stop, and manage Docker containers on a cluster of EC2 instances easily.

Amazon ECR (Elastic Container Registry): ECR is a managed Docker container registry provided by AWS. It allows you to store, manage, and deploy Docker container images, making it easy to integrate with ECS for container deployments.

Amazon EC2 (Elastic Compute Cloud): EC2 is AWS's resizable cloud computing service offering virtual machines (instances) for running applications. It provides flexibility to configure and scale computing resources based on demand.

## Deployment Process
### Containerize your Node.js application:
Using Dockerfile allows one to create a container for the app.
Create a Dockerfile in the root directory of your Node.js application.
Write instructions to build your Node.js app within the Dockerfile.
Build the Docker image locally using docker build -t <image-name> .
Test the image locally to ensure it works as expected: docker run -p 8080:80 <image-name>
The first number 8080 is the host port and 80 is the container port. 

### Create an ECR repository:

Log in to the AWS Management Console.
Go to the Amazon ECR service.
Create a new repository to store your Docker image.
Push your Docker image to ECR:
Tag your Docker image with the ECR repository URL:
```bash
$ docker tag <image-name> <aws-account-id>.dkr.ecr.<region>.amazonaws.com/<repository-name>:<tag>
```
Log in to ECR using the AWS CLI:
```bash
$ aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <aws-account-id>.dkr.ecr.<region>.amazonaws.com
```
Push your Docker image to the ECR repository:
```bash
$ docker push <aws-account-id>.dkr.ecr.<region>.amazonaws.com/<repository-name>:<tag> 
```

Replace \<image-name> with the name you want to label your image with
Replace \<aws-account-id>, \<region>, \<repository-name>, \<tag> with your correct credentials and your ECR name URL.

Create an ECS Task Definition:

Go to the Amazon ECS service in the AWS Management Console.
Create a new task definition specifying your container image from ECR, CPU, memory requirements, etc.

Create an ECS Cluster:
Create an ECS cluster if you don't have one already.
Configure the ECS cluster settings and select launch type (Fargate or EC2).

Create an ECS Service:
Define a service within the ECS cluster.
Specify the task definition, desired number of tasks, network configuration, load balancer settings, etc.

Deploy your ECS Service:
Review and finalize the ECS service settings.
Deploy the service to the ECS cluster.

# Access your Node.js application
Once the ECS service is up and running, access your Node.js application using the provided service endpoint.
