# Using Python Ray Tasks to distribute your functions on multiple machines


## Table of Contents
- [Prerequisites](#prerequisites)
- [Introduction](#introduction)
- [Introduction to Ray](#introduction-to-ray)
- [Installation](#installation)
- [Creating a Ray Cluster](#creating-a-ray-cluster)
- [Running a Task on the Cluster](#running-a-task-on-the-cluster)
- [Stop Ray on the Cluster](#stop-ray-on-the-cluster)
- [Additional Resources](#additional-resources)


## Prerequisites
- Two Machines
- You are interest in building and scaling distributed applications

## Introduction
Ray is a heavyweight framework and it's expensive to learn all the functionalities. This tutorial will only introduce Ray Tasks as the tip of the iceberg for building and scaling distributed applications. I will give you a small tour of using Ray Tasks to distribute your functions to two different machines.

### Introduction to Ray
Ray is a unified framework for scaling AI and Python applications. Ray consists of a core distributed runtime and a set of AI Libraries for accelerating ML workloads.

Today's ML workloads are increasingly compute-intensive. As convenient as they are, single-node development environments such as your laptop cannot scale to meet these demands.

Ray is a unified way to scale Python and AI applications from a laptop to a cluster.

With Ray, you can seamlessly scale the same code from a laptop to a cluster. Ray is designed to be general-purpose, meaning that it can performantly run any kind of workload. If your application is written in Python, you can scale it with Ray, no other infrastructure required.

### Introduction to Ray Tasks
Ray Core provides a small number of core primitives (i.e., tasks, actors, objects) for building and scaling distributed applications. You can turn your functions and classes easily into remote tasks in the cluster.

## Installation
Install Ray in python:
```
pip install ray
```

If you are looking for installation on different platform or for different languages, please visit [here](https://docs.ray.io/en/latest/ray-overview/installation.html).


## Creating a Ray cluster
Creating a Ray cluster that spans across two machines involves setting up one machine as the head node and the other as a worker node. Here's how you can do it:

### Step 1: Install Ray on Both Machines
First, ensure Ray is installed on both machines. You can install it using pip:
```
pip install ray
```

### Step 2: Set Up the Head Node
On the machine you choose to be the head node, start Ray with the following command:
```
ray start --head --port=6379
```

This command will output several addresses, but the most important one is the ray://<head-node-ip-address>:10001. You'll need this to connect the worker node to the head node.

### Step 3: Set Up the Worker Node
On the other machine (the worker node), you will connect to the head node using the address provided above. Replace <head-node-ip-address> with the actual IP address of the head node:
```
ray start --address='<head-node-ip-address>:6379'
```

### Step 4: Check the status of your Ray cluster
To check the status of your Ray cluster, you need to run `ray status`` on the head node of your cluster.

If ray status shows all expected nodes with their resources, it indicates that the cluster nodes are connected and communicating properly.


## Running a Task on the Cluster
Now, you can run a Python script on the head node that utilizes the cluster. Here’s a simple example:

Initialize Ray: In your Python script on the head node, initialize Ray and connect it to the cluster:
```
import ray
ray.init(address='auto')  # Connect to the existing cluster
```

Define a Task: Create a task as a remote function:
```
# Define the square task.
@ray.remote(num_cpus=1)  # Assuming each node has the same number of CPUs
def square(x):
    return x * x
```

Run the Task: Execute the task. It can now run on any node in the cluster:
```
# Launch four parallel square tasks.
futures = [square.remote(i) for i in range(4)]
```

Retrieve the Result: Get the result of the task:
```
# Retrieve results.
print(ray.get(futures))
# -> [0, 1, 4, 9]
```

Shutdown: When done, you can disconnect from the cluster:
```
ray.shutdown()
```

In this example, each task is configured to use a single CPU. Ray will schedule these tasks across the available nodes, aiming to utilize the CPUs as evenly as possible.


## Stop Ray on the Cluster
When you're finished, you can stop Ray on both machines:

On the head node:
```
ray stop
```

On the worker node:
```
ray stop
```

## Additional Resources
(Ray)[https://www.ray.io/]

(Introduction to Ray Core)[https://docs.ray.io/en/latest/ray-core/walkthrough.html#running-a-task]

