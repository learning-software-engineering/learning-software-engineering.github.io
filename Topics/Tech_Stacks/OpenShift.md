
## Table of Contents

- [Introduction](#introduction-to-openshift)
- [Key Features](#key-features)
- [Architecture](#architecture)
- [Deploying an Application](#deploying-a-simple-application)
  - [Prerequisites](#prerequisites)
  - [Accessing your Cluster](#accessing-your-cluster)
  - [Creating an Application](#creating-an-application)
  - [Deploying an application](#deploying-an-application)
  - [Accessing application](#accessing-application)z
- [Additional Resources](#additional-resources)

## Introduction to OpenShift

Red Hat OpenShift is an open source container application platform that runs on Red Hat Enterprise Linux CoreOS (RHCOS). It is built on existing Kubernetes features with additional features specific to OpenShift. It takes care of scaling, monitoring, logging, and metering functions like Kubernetes but also provides an in cluster docker registry, developer friendly environment amongst other features. 

## Key Features:

-	**Security**: It provides features such as role-based access control (RBAC), image scanning to ensure images have less vulnerabilities and applications can run in a secure environment with restricted access.

-	**Container Registry**: It includes an integrated container registry, that allows storage and management of container images in the cluster.

-	**Container Orchestration**: It uses Kubernetes to automate the deployment, scaling, and management of containers. These features allow developers to focus on application code rather than infrastructure.

-	**Developer**:  It provides several features that enhances development process by provided a user-friendly UI that allows developers to manage application, resources, and pod health. Additionally, it includes Source-to-Image (S2I) a tool which simplifies building and deploying container images from source code. 

-	**Operator**: This is a key feature that distinguishes OpenShift from Kubernetes. Operators are a method for packaging and running Kubernetes applications. It greatly simplifies installation, updates, and management. In essence, it automates the entire lifecycle management process.


## Architecture

In order to understand OpenShift, it is crucial to know the architecture. It has several layers with dedicated responsibilities.

### Infrastructure Layer

This layer allows the cluster to be deployed on the cloud either private or public or on physical or virtual servers.

### Service Layer

This layer is an abstraction provided by Kubernetes primarily used to expose and access applications within the cluster. It facilitates communication between different components. It primarily consists of 2 types of nodes: master and worker node. Each node has a host and IP address that can be accessed within the cluster. Only the master node has a public IP address that can be accessed from outside the cluster.

#### Master node
-	**API and authentication**: To ensure the security of the cluster, any administration/ access request goes through the API.
-	**Data Store**: Stores the state and information related to the environment and application.
-	**Scheduler**: Determines where pods and jobs  will run  while considering current memory, CPU, and other environment factors.
**Health/scaling**:  Monitors the well-being of pods and adjusts their scale according to CPU utilization. In the event of pod failure, the primary node initiates an automatic restart. In case of frequent failures, the pod is flagged as bas and is temporarily withheld from further restart attempts.


#### Worker node
 The worker node is made of pods, pods are the smallest unit that can be deployed, and it can contain one or more containers. Containers typically include requirements and dependencies your applications need to run. It is important to note that containers are ephemeral, and containers restart often which can lead to loss of data. To prevent that, persistent storage is used to save data. It also consists of registry to store images.


### Routing Layer

It provides routes that allow for external access to applications.

## Deploying a Simple Application

### Prerequisites
- RedHat OpenShift Cluster
  - You can create a minimal preconfigured cluster using the Developer Sandbox package [here](https://www.redhat.com/en/technologies/cloud-computing/openshift/try-it).
- Python
- OpenShift CLI - Instructions can be found [here](https://docs.openshift.com/container-platform/4.11/cli_reference/openshift_cli/getting-started-cli.html)
- Docker

### Accessing your Cluster
- To log in to your cluster use `oc login <cluster-name> -u kubeadmin -p <password>` in your terminal. The password can be found on the Openshift console web page. On the upper right corner of the toolbar, there you will find your username `kubeadmin`, click on it to get your password.
- Alternatively, you can ssh into your cluster with the public IP address of the master node and kubeadmin password.

### Creating an Application
- Create a simple python file app.py as follows
```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8080)
```

- Create a requirements file called requirements.txt:
```
Flask==2.1.0
```

- Create a docker file named Dockerfile as follows:
```
FROM python:3.9-slim

WORKDIR /app
COPY . .

RUN pip install --no-cache-dir -r requirements.txt

CMD ["python", "app.py"]
```

### Deploying an application

Now, we will create an image and push the image to our registry. In order to do so, we need to find our registry name, username and password
- `oc get route -n openshift-image-registry` will provide you with the name of your image registry in your Openshift Cluster.
- `oc whoami -t` will output the password for the registry

Once you have your registry's URL, username and password, you can login with the following command:
```
docker login -u <username> -p $(oc whoami -t) <registry-url>
```

Then, we can build our image and push it to the registry with the following commands:
```
docker build -t <registry-url>/hello-world-app
docker push <registry-url>/hello-world-app
```

Now, lets deploy an application using this image.

```
oc new-app <registry-url>/hello-world-app
```

### Accessing application

In order to the application and make it accessible, we will have to "expose" the service. This can be done with the following command:
```
oc expose svc/hello-world-app
```

With the following command,  you can find the URL where the app has been deployed, i.e. there will be a "Hello World!"
```
oc get route | grep hello-word-app
```



## Additional Resources
You can find additional information and details here:

- [Openshift 101:  Introduction, architecture, and operators](https://developer.ibm.com/blogs/openshift-101-architecture)
- [OpenShift 101: Web console and CLI](https://developer.ibm.com/blogs/openshift-101-web-console-and-cli)



