# CD for a Dockerized application using Github Actions, Amazon ECR and Amazon ECS

## Introduction
Containerized applications are becoming more popular due to the consistency they provide accross different machines and portability to different cloud providers. It is becoming increasingly valuable to build applications with dockerization in mind. With that comes the need to streamline deployment of these containerized applications.

## Pre-Requisites
- [Dockerizing an app](./Docker.md)
- [Github Actions](./Github_Actions.md)

## Step 1 (Setting up your application & AWS): 
- Essentially you want to follow the same steps as this tutorial [Deploy Node.js Docker AWS](./Deploy_Node.js_Docker_AWS.md), adjusting your dockerfile according to language and tools you are using for your application. The main goals are to
    - Containerize your application
    - Create an amazon ECR repository
    - Create an ECS cluster, service as well as task definition

**NOTE**: It's important that your ECR repository and ECS cluster are defined on the same AWS region otherwise you may have to sign into aws twice below


## Step 2 (Setting up the workflow -- triggers):
```
on:
  push:
    branches:
      - production
```
- With the above code we ensure that the workflow created in this guide is run only on pushes to the "production" branch
- Generally you only want to deploy your application on pushes to some branch designated as your production branch to avoid wasting github actions minutes and deploying when development is underway 

## Step 2 (Setting up the workflow triggers):
Create a new job
```
jobs:
  deploy:
    name: Deploy
    runs-on: ubuntu-latest
    environment: production

    steps:
```
- We'll be creating a new job called deploy that runs on an ubuntu instance
- All subsequent steps will fall under the "steps:" section in the code block above

## Step 3 (Checking out the repo)
```
- name: Checkout
        uses: actions/checkout@v4
```
- Create a new step for checking out the current repo. This ensures that in subsequent steps you have access to all code within your current repo

## Step 4 (Signing into AWS)
```
- name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@0e613a0980cbf65ed5b322eb7a1e075d28913a83
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: <YOUR_AWS_REGION>
- name: Login to Amazon ECR
        id: login-ecr
        uses: aws-actions/amazon-ecr-login@62f4f872db3836360b72999f4b87f1ff13310f3a
```
- For details on how to quickly set up your AWS credentials, view the following video: https://www.youtube.com/watch?v=gswVHTrRX8I
- From the above video, you should have recieved an access key as well as a secret access key which you should then set in your [Github Secrets](https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions)
- Setting secrets ensures that you have access to your credentials within your workflow without explicitly writing them out in the workflow file
- We are using an action defined by someone else to aid us in signing into aws for subsequent steps

## Step 5 (Building/tagging your image and pushing it to your ECR repo)
```
- name: Build, tag, and push image to Amazon ECR
        id: build-image
        run: |
          docker build -t <ECR_REGISTRY>/<ECR_REPOSITORY>:latest <DOCKERFILE_FOLDER_PATH>
          docker push <ECR_REGISTRY>/<ECR_REPOSITORY>:latest
```
- Just like how we build the docker image in order to run a container locally, we should build, tag and push our image to our ECR repository so that ECS can pull from it in a future step
- The `DOCKERFILE_FOLDER_PATH` is the path to the folder containing the dockerfile to build your application
- The `ECR_REGISTRY` and `ECR_REPOSITORY` can be retrieved from the repository URI
<img width="791" alt="Screenshot 2024-03-17 at 9 41 59 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/58835213/5dd3ce35-6094-48db-980e-a0456becc663">

## Step 6 (Deploying the application)
```
- name: Deploy Amazon ECS task definition
        uses: aws-actions/amazon-ecs-deploy-task-definition@df9643053eda01f169e64a0e60233aacca83799a
        with:
          task-definition: <PATH_TO_TASK_DEFINITION>
          service: <ECS_SERVICE>
          cluster: <ECS_CLUSTER>
          wait-for-service-stability: true
```
- Once again, using an existing action, we will deploy the app by specifying some additional information
- The task definition, ECS service and ECS cluster are defined as per [Deploy Node.js Docker AWS](./Deploy_Node.js_Docker_AWS.md)
- For `<PATH_TO_TASK_DEFINITION>` you should link to that path of your aws task definition JSON file in your repository. If you don't have one in your repository you can generate one by visiting the task definitions page in Amazon ECS <img width="1022" alt="Screenshot 2024-03-17 at 9 30 22 PM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/58835213/8144e7cf-21b7-4c8c-89ad-130e04b5f5a6">


- `wait-for-service-stability` keeps the workflow from passing until the ECS service has become stable given the most recent deployment

## Conclusion
Congrationations, you have reached the end of this tutorial! After a push to your production branch you should be able to sit back and watch your newest workflow deploy your app for you!

## Reference
This guide is inspired by this github actions guide [Deploying to amazon elastic container service](https://docs.github.com/en/actions/deployment/deploying-to-your-cloud-provider/deploying-to-amazon-elastic-container-service)
