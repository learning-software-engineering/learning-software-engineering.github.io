# Introduction to Kubernetes

## What is Kubernetes?

Kubernetes, also known as K8s, is an open-source platform that automates the management process for application containers. It was developed by Google and is now maintained by the Cloud Native Computing Foundation.

## Key Features

- **Auto Scailing:** Kubernetes automatically scales its resources dyamically to meet application's demand.
- **Container Orchestration:** Kubernetes efficiently manages containers across multiple hosts.
- **Self-healing:** It automatically restarts containers that fail, replaces them, and kills containers that don't respond to user-defined health checks.
- **Load Balancing:** Kubernetes can distribute network traffic to ensure stability.
- **Automated Rollouts and Rollbacks:** Allows changes to the application or its configuration while monitoring application health.

## Components

1. **Pods:** The smallest deployable units that can be created, scheduled, and managed.
2. **Services:** An abstraction to expose an application running on a set of Pods.
3. **Volumes:** Provides a way to store data and stateful applications.
4. **Namespaces:** Enable multiple virtual clusters on the same physical cluster.

## Set-up (For macOs)
1. **Install Homebrew** (if not already installed):
  [Homebrew](https://brew.sh/)

2. **Install Minikube via Homebrew**:
   - In Terminal, run `brew install minikube`.

3. **Start Minikube**:
   - Run `minikube start` in Terminal. This command starts a local Kubernetes cluster.

4. **Check the Minikube Status**:
   - Run `minikube status` to ensure everything is up and running.

5. **Install `kubectl`**:
   - If you don't have `kubectl` installed, run `brew install kubectl`.

6. **Run a Kubernetes Pod**:
   - Use `kubectl` to run a pod, for example, `kubectl run my-pod --image=nginx`. Replace `my-pod` with your desired pod name and `nginx` with the Docker image you want to use.

7. **Check the Pod Status**:
   - Run `kubectl get pods` to see if your pod is running. 

That's it! 

## Conclusion

Kubernetes is a powerful tool for managing containerized applications, providing efficiency and flexibility in application deployment and management.

---

For more detailed information, visit the official Kubernetes website: [kubernetes.io](https://kubernetes.io).
