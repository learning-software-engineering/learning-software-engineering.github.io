# Learning Docker

## Table of Contents
### [Introduction](#introduction-1)
### [Installation](#installation-1)
### [Getting Started](#getting-started-1)
### [Next Steps](#next-steps-1)
### [Docker Terminology](#docker-terminology-1)

----

## Introduction

This article will help readers understand what Docker is, why it is used and how to start using it. Docker is used by developers for many reasons, however, the most common reasons are for building, deploying and sharing an application quickly. Docker packages your application into something that's called a [container](#docker-terminology-1). This [container](#docker-terminology-1) is OS-agnostic meaning that developers on Mac, Windows and Linux  can share their code without any worry of conflicts. Here's [Amazon's Intro to Docker](https://aws.amazon.com/docker/#:~:text=Docker%20is%20a%20software%20platform,tools%2C%20code%2C%20and%20runtime.) if you want to learn more.

----

## Installation

To start using Docker you will have to download Docker Engine. This is automatically downloaded alongside Docker Desktop (A Graphical User Interface for Docker). 
[Download Docker Desktop here](https://www.docker.com/get-started/)


For detailed installation instructions based on specific operating systems click here: [Mac](https://docs.docker.com/desktop/install/mac-install/), [Windows](https://docs.docker.com/desktop/install/windows-install/), [Linux](https://docs.docker.com/desktop/install/linux-install/) 

----

## Getting Started

Once you've installed Docker, to see it in action you can follow any one of these quick tutorials:

- [Dockerizing a React App](https://mherman.org/blog/dockerizing-a-react-app/) (Simple and quick tutorial for containerizing a React App, contains lots of explanations. I recommend this if you want to quickly get something running plus see what the next steps look like)
- [Dockerize a Flask App](https://www.freecodecamp.org/news/how-to-dockerize-a-flask-app/) (Super detailed step-by-step explanations tutorial for containerizing a flask app. I recommend this if you want to understand *everything* that goes on)
- [Docker's official tutorial for containerizing an application](https://docs.docker.com/get-started/02_our_app/) (Can't go wrong with the official tutorial.)

----

## Next Steps

Congratulations! you have successfully learnt how to Dockerize an app and use it. You have learnt what is a `Dockerfile`, how to create a `Dockerfile`, build a Docker Container Image and start a Docker Container. Now what's next?

Now you might want a React Container to communicate with a containerized Flask API. How do we do this? This is where [Docker Compose](https://docs.docker.com/compose/) comes in. It allows you to define, control multiple containers at once. Your next steps should be defining a `docker-compose.yml` for your project and see if you can get multiple services/containers to successfully communicate.

----

## Other Resources

Here's a [cheat sheet](https://docs.docker.com/get-started/docker_cheatsheet.pdf) of all useful Docker CLI commands and here's a [cheat sheet](https://devhints.io/docker-compose) for docker compose which should help you in your future endeavors All the best!

----

## Docker Terminology
- **Container**: A package of code bundled by Docker that runs as an isolated process from your machine. The package of code can be pretty much anything, a single python file, an API, a full stack web application etc. A container is also referred to as a **containerized application**.

- **Image**: template with a set of instructions for creating a container. *(most of the times these are pre-built so don't worry too much about making one)*

Explained in Docker's words [here](https://docs.docker.com/get-started/)