# Kubernetes

## Table of Contents
1. [Introduction](#Introduction)
    - [What is Kubernetes(k8s)?](#What-is-Kubernetes(k8s)?)
    - [Kubernetes vs Docker](#k8s-vs-docker)
    - [Why k8s?](#why-k8s)
2. [CI/CD](#CI/CD)
3. [Examples](#Examples)

## Introduction
### What is Kubernetes(k8s)?

Kubernetes known as k8s is a cluster manage tool and distrubuted supporting platform to use automate, deploying, and scaling container.

### k8s vs Docker? 
Docker provides consistent environments for developing and running applications across different systems, isolating applications within containers, enabling deployment anywhere, optimizing resource utilization, implementing version control for images, and facilitating DevOps practices. This allows multiple processes to run on the same machine without interfering with each other during execution.

In contrast, Docker and Kubernetes (often abbreviated as k8s) are complementary technologies in containerization. Docker focuses on container creation and runtime, while Kubernetes addresses challenges in deploying and managing containers in production environments. Together, they form a powerful combination for modern application development and deployment workflows.

An illustrative analogy is imagining your program running within a box; the box represents Docker, while Kubernetes acts as the delivery person ensuring your box reaches the correct destination with the appropriate wrapping.

### why k8s? 
k8s played a significant role in cloud-native computing due to its ability to streamline the deployment and management of containerized applications at scale. K8s help improve resolve complex microservices architectures across distributed environments. It offers automated scaling, self-healing capabilities, and declarative configuration, empowering developers to focus on building robust and scalable applications without being bogged down by the complexities of infrastructure management. 


### CI/CD
k8s with CI/CD practices revolutionizes the software development lifecycle, offering agility and efficiency.  By integrating K8s with CI/CD pipelines, user can achieve faster release cycles, improved quality assurance, and greater overall productivity. CI/CD pipelines trigger automated tests and builds whenever new code is committed, with K8s enabling the seamless deployment of these changes into production environments. This integration ensures consistency between development, testing, and production environments, reducing the risk of errors and ensuring a smoother deployment process. With K8s and CI/CD, organizations can embrace a DevOps culture, delivering value to customers more quickly and efficiently while maintaining a high standard of readbilty and scalability in their applications.

### Examples

k8s are usually config in yaml format

 Deployment: manage and scale applications. It defines the desired state for a set of pods (replica set) and ensures that the specified number of replicas are running at `all times`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: example-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: example-app
  template:
    metadata:
      labels:
        app: example-app
    spec:
      containers:
      - name: example-container
        image: nginx:latest
        ports:
        - containerPort: 80
        env:
        - name: USERNAME
          valueFrom:
            secretKeyRef:
              name: example-secret
              key: username
        - name: PASSWORD
          valueFrom:
            secretKeyRef:
              name: example-secret
              key: password
        volumeMounts:
        - name: config-volume
          mountPath: /etc/config
      volumes:
      - name: config-volume
        configMap:
          name: example-configmap

```
Certainly! Here's the reworded version:

k8s allows for dynamic patching of environment variables into containers using `Secrets` and `ConfigMaps`. `Secrets `typically safeguard vital credentials from unauthorized access, while `ConfigMaps` serve as repositories for local configurations that dictate application behavior. `Secrets` encode sensitive data like passwords and API tokens in a base64 format to maintain confidentiality, while `ConfigMaps` store non-sensitive settings such as environment variables and application configurations.  
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: example-secret
type: Opaque
data:
  username: <base64-encoded-username>
  password: <base64-encoded-password>
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: example-configmap
data:
  app-config.yaml: |
    key1: value1
    key2: value2
---

```

CronJob: schedule and run tasks at specific times or intervals, similar to the cron utility in Unix-like operating systems. It allows users to define a job template and specify a schedule using the cron format.
```yaml
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: example-cronjob
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: example-container
            image: busybox
            command: ["echo", "Hello from the cron job"]
          restartPolicy: OnFailure
```
`schedule` takes an input unix-like, a really useful website would be `https://crontab.guru/`

Here is few examples:
- `*/1 * * * *` : “At every minute.”
- `0 * * * *` : "At the beginning of every hour."
- `0 0 * * *`: "At midnight every day."
- `0 9 * * MON-FRI`: "At 9:00 AM every weekday."

