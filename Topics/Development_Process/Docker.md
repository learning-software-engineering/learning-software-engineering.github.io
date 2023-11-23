# Learning Docker

## Table of Contents
### [Introduction](#introduction-1)
### [Installation](#installation-1)
### [Getting Started](#getting-started-1)
### [Next Steps](#next-steps-1)
### [Docker Terminology](#docker-terminology-1)

----

## Introduction

This article will help readers understand what Docker is, why it is used and provide resources on how to start using it. Docker is used by developers for many reasons, however, the most common reasons are for building, deploying and sharing an application quickly. Docker packages your application into something that's called a [container](#docker-terminology-1). This [container](#docker-terminology-1) is OS-agnostic meaning that developers on Mac, Windows and Linux can share their code without any worry of conflicts. Here's [Amazon's Intro to Docker](https://aws.amazon.com/docker/#:~:text=Docker%20is%20a%20software%20platform,tools%2C%20code%2C%20and%20runtime.) if you want to learn more.

## Installation

To start using Docker you will have to download Docker Engine. This is automatically downloaded alongside Docker Desktop (A Graphical User Interface for Docker) which I **strongly** recommend for Windows and macOS users.
[Download Docker here](https://www.docker.com/get-started/)

For detailed installation instructions based on specific operating systems click here: [Mac](https://docs.docker.com/desktop/install/mac-install/), [Windows](https://docs.docker.com/desktop/install/windows-install/), [Linux](https://docs.docker.com/desktop/install/linux-install/) 

## Creating Dockerfiles

Once you've installed Docker, to see it in action you can follow any one of these quick tutorials on creating a Dockerfile that builds a Docker image:

- [Dockerizing a React App](https://mherman.org/blog/dockerizing-a-react-app/) (This simple and quick tutorial for containerizing a React App, contains explanations when needed. I recommend this if you want to quickly get something running plus see what the next steps look like)
- [Dockerize a Flask App](https://www.freecodecamp.org/news/how-to-dockerize-a-flask-app/) (Super detailed step-by-step explanations tutorial for containerizing a flask app. I recommend this if you want to understand the process in detail)
- [Docker's official tutorial for containerizing an application](https://docs.docker.com/get-started/02_our_app/) (Can't go wrong with the official tutorial.)

### Automatic Dockerfile Generation

Since Docker is widely used, there is a lot of Dockerfile-related knowledge in ChatGPT's training data, and the AI is capable of generating Dockerfiles for most software architectures. If you want to easily containerize your app, you can use OpenAI's ChatGPT 3.5-turbo to generate the Dockerfile for you. To do this, you first need to gather a tree of your project directory for ChatGPT to better understand your project architecture (On Linux/macOS, run `tree -I node_modules` in your project directory). Then, you can ask ChatGPT using something similar to the following prompt:

```
Please write a Dockerfile for my project. I use the command `python3 -m projectname` to start my app. My project file structure is specified by the tree below. Please make sure that the Dockerfile is optimized with best practices from the industry and that the image size is as small as possible.

.
├── README.md
├── backend
│   ├── __init__.py
│   ├── database
│   │   ├── __init__.py
│   ├── flow.py
│   ├── rapidpro.py
│   └── user.py
├── poetry.lock
├── pyproject.toml
└── tests
    ├── RapidProAPI_test.py
    ├── __init__.py
    └── flow_test.py

I have the following runtime dependencies that might require APT packages: psycopg2
```

This method will generate something that's much more optimized than any beginner can write. For example, it will clear the APT cache for dependency installation, and use separate builder and runtime images to reduce image size, which involves understanding the intricate Docker image layering mechanism. You can learn a lot from reading and understanding the generated Dockerfile.

## Next Steps

Congratulations! You have successfully learned how to Dockerize an app. In the process, you have learnt what is a `Dockerfile`, how to create a `Dockerfile`, how to build a Docker Container Image and how to start a Docker Container. Now what's next?

Now you might want a React Container to communicate with a containerized Flask API. How do we do this? This is where [Docker Compose](https://docs.docker.com/compose/) comes in. It allows you to define, and control multiple containers at once. Your next goal should be defining a `docker-compose.yml` for your project and see if you can get multiple services/containers to successfully communicate.

## Free Automatic Builds

You can use various CI (Continuous Integration) tools to automatically build, push, and deploy your Docker Images. While the official [Docker Hub](https://hub.docker.com/) is a great place to store your images for free, the automated builds are only available for paid accounts. Here, we will guide you on how to use [GitHub Actions](https://github.com/features/actions) to automatically build and push your Docker Images to Docker Hub.

### Prerequisites

- A [Docker Hub](https://hub.docker.com/) account
- A [GitHub](https://github.com) account and a repository
- A Dockerfile

### Steps

#### Creating Access Token

1. First, you need to create a Docker Hub token to allow GitHub Actions to push to your Docker Hub repository. To do this, go to your [Docker Hub Account Settings](https://hub.docker.com/settings/security) and click on "New Access Token". Give it a name and click on "Create". (Don't close this page yet, you will need it later)
2. Open your GitHub repository and go to the "Settings" tab. Click on "Secrets" and then "New repository secret". Give it a name (e.g. `DOCKERHUB_TOKEN`) and paste the token you just created in the previous step. Click on "Add secret".
3. Do the same for `DOCKERHUB_USERNAME`

#### Creating Workflow

1. In your GitHub repository, create a new folder called `.github/workflows`
2. Paste the following file under `.github/workflows/docker.yml` (Make sure to replace `YOUR_IMAGE_NAME_HERE` with your image name)
3. Commit and push your changes
4. Profit!

```yml
name: Build and Push Docker Image

on:
  push:
    branches:
      - main  # Change this to your default branch

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
    - uses: docker/setup-buildx-action@v3

    - name: Login to DockerHub
      uses: docker/login-action@v3
      with:
        username: ${{ secrets.DOCKERHUB_USERNAME }}
        password: ${{ secrets.DOCKERHUB_TOKEN }}

    - name: Build and push Docker image
      uses: docker/build-push-action@v5
      with:
        push: true
        tags: ${{ secrets.DOCKERHUB_USERNAME }}/YOUR_IMAGE_NAME_HERE:latest
```

Note: This workflow will automatically build and push after each commit to the `main` branch. This is ideal for development, assuming that your main branch is the staging branch. However, you might want to change it or create a separate workflow with a separate image name to only build on tags (releases) for production so that the deployment is more controlled.

## Deploying and Automatic Updates

Now that you have a Docker Image on Docker Hub, you can deploy it to a server. There are many ways and platforms that allow you to do this. You can rent a minimal Linux VPS server or a Docker server for $4-6 per month on various platforms. One platform I recommend is DigitalOcean, as they have a very intuitive web interface and very good [documentation](https://www.digitalocean.com/docs/) for beginners. you can click the referral link (icon) below to get a free $200 credit for 60 days, what a deal!

[![DigitalOcean Referral Badge](https://web-platforms.sfo2.cdn.digitaloceanspaces.com/WWW/Badge%201.svg)](https://www.digitalocean.com/?refcode=86dbfd5d0266&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge)

<!-- You can also use Linode, they are more advanced and provide a wider range of services. They also have a referral program, but it's not as good as DigitalOcean's. You can click the referral link below to get a $100 credit for 60 days. -->

Once you have a Linux server, the easiest way to deploy a docker image is to use [Docker Compose](https://docs.docker.com/compose/). You can define your services in a `docker-compose.yml` file and then run `docker-compose up -d` to start the containers in the background.

### Deploying with Docker Compose on DigitalOcean

1. Install Docker Core on your server [(official guide for Ubuntu)](https://docs.docker.com/engine/install/ubuntu)
2. Install docker-compose plugin [(official guide)](https://docs.docker.com/compose/install/linux/#install-using-the-repository).
3. Create a `docker-compose.yml` file on your server and paste the following (Make sure to replace `YOUR_IMAGE_NAME_HERE` with your image name)
4. Run `docker-compose up -d` to start the containers in the background

```yml
version: "3.9"

services:
  app:
    image: YOUR_IMAGE_NAME_HERE:latest
    restart: always
    ports:
      - 80:80  # Expose any ports you need
```

If you need a database, you can add it to the composition as well! For example, if you want to use PostgreSQL, you can add the following to your `docker-compose.yml` file:

```yml
version: "3.9"

services:
  app:
    image: YOUR_IMAGE_NAME_HERE:latest
    restart: always
    ports:
      - 80:80  # Expose any ports you need
    depends_on:
      - db
    environment:  # In your program, use these environment variables to connect to the database
      DB_HOST: db
      DB_PORT: 5432
      DB_USER: postgres
      DB_PASSWORD: postgres
      DB_NAME: postgres

  db:
    image: postgres:13
    restart: always
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: postgres
```

Since the database is contained within the docker-compose network, it is perfectly secure to use the default `postgres` user and password, since it cannot be accessed through the wider internet. However, if you want to expose your database (which is not recommended), you can add the port `5432:5432` to the `db` service and use a stronger password.

If you are using any other database, you can find the docker image on [Docker Hub](https://hub.docker.com/search?q=&type=image&category=Database) and follow the instructions there. Please be sure to read the docker container's documentation carefully! Most questions regarding database images can be answered by reading the documentation.

### Automatic Updates

To automatically update your deployment when you push a new image to Docker Hub, you can use [Watchtower](https://github.com/containrrr/watchtower). It is a simple container that monitors your other containers and updates them when a new image is available. You can add it to your `docker-compose.yml` file like this:

```yml
services:
  # ...

  watchtower:
    image: containrrr/watchtower
    restart: always
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    command: --interval 30
```

This will check for updates every 30 seconds. You can change this to whatever you want. You can also add a `--cleanup` flag to remove old images after updating.

### Advanced Deployment

If you have multiple services and want to deploy them on the same server with different domain names or set up SSL to make your services secure from MITM (man-in-the-middle) attacks, you can use [Traefik](https://doc.traefik.io/) or [Nginx](https://www.nginx.com/) as a reverse proxy. This is a more advanced topic and is out of the scope of this article. However, you can find many tutorials online on how to do this, such as this DigitalOcean article: [How To Use Traefik v2 as a Reverse Proxy for Docker Containers on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-use-traefik-v2-as-a-reverse-proxy-for-docker-containers-on-ubuntu-20-04)

## Other Resources

Here's a [cheat sheet](https://docs.docker.com/get-started/docker_cheatsheet.pdf) of all useful Docker CLI commands and here's a [cheat sheet](https://devhints.io/docker-compose) for docker-compose which should help you in your future endeavours. All the best!

## Docker Terminology
- **Container**: A package of code bundled by Docker that runs as an isolated process from your machine. The package of code can be pretty much anything, a single Python file, an API, a full-stack web application etc. A container is also referred to as a **containerized application**.

- **Image**: template with a set of instructions for creating a container. *(most of the times these are pre-built so don't worry too much about making one)*

Explained in Docker's own words [here](https://docs.docker.com/get-started/)
