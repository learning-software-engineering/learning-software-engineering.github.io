# CI/CD with CircleCI

## Table of Contents
1. [CircleCI Overview & Motivation](#overview--motivation)
    - [What is CircleCI?](#what-is-circleci)
    - [Why should you use it?](#why-should-you-use-it)
2. [Guide Overview and Prerequisites](#guide-overview-and-prerequisites)
3. [Preconfiguration](#preconfiguration)
    - [Account Creation](#account-creation)
4. [The config.yml file](#when-does-rest-make-sense-to-use)
5. [When does GraphQL make sense to use?](#when-does-graphql-make-sense-to-use)
6. [Quick Reference](#quick-reference-for-common-uses)
7. [Summary](#summary)
8. [Additional Readings](#additional-reading)

## Overview & Motivation
### What is CircleCI? 
CircleCI is a continuous integration and continuous delivery (CI/CD) platform that automates the software development process just like Github Actions, Jenkins, or Gitlab. It is designed to help software teams rapidly release code with confidence by automating the build, test, and deployment processes.


### Why should you use it?
- Separating platform for code and CI/CD.
    - Unlike Github Actions, which is a platform integrated into Github. CircleCI is a platform separate from where you store your code. For teams that want to have this clear separation, CircleCI is a suitable choice.
- Performance
    - CircleCI supports parellelization for faster builds and is faster than Github Actions in terms of build time.
- CLI
    - CircleCI provides a local command line interface which allows you to test configurations and run jobs locally through docker so that you don't have to push to github to check if your config.yml is properly configured.


## Guide Overview and Prerequisites
This guide will walk through automatically testing and deploying a github repository using CircleCI. Specifically, the guide will be testing and deploying a node application to NPM. For your use case, you may choose to deploy an application of your choice to a package repository of your choice. For the purposes of this guide we will assume that you have the following:
- Basic knowledge of node.js and the node package manager.
    - This guide will be primarily focused on the elements of CircleCI rather than the node project itself.
- A github repository containing your project.

## Preconfiguration
### Account Creation
First, go to the [CircleCI website](https://circleci.com/signup/) and create an account. You will have to specify some details such as whether the account is for business or personal, if your project contains AI elements, and the your title.

### Connecting to a Project
After you have filled out the details, you will be prompted to a page where you'll be able to connect to an existing Github, Gitlab or Bitbucket project. For this guide, we will be connecting to our existing github repository. You will be prompted to login on Github, and where you would like to install CircleCI. It will show the list of organizations that you belong to within Github. For this guide, we will assume that the repository is yours. Select your github username to install CircleCI as a third party app onto your repos. Specify the scope of the installation, whether it be for a specific repository or all of them. Here, find your repository and give CircleCI access to it.
 
You will be prompted to a page where you will have to generate an ssh key pair. Add the public key as a deploy key on your github repository, and the private key into the prompt.

You will have the option to choose between a "faster" or "fast" way to initialize your project. The faster method has CircleCI make a new branch and automatically make a circleci config yml for you. For this guide, we will use this method. However, if you would like to make your own branch and add a config.yml that way, that is also okay. 

Once you have created your project, you will be prompted to make the commit that contains your config yaml. Here, you will have a variety of configuration templates that you can choose to initialize with. For the purposes of this guide, use the "Hello World" option. Now commit and run.


## The config.yml File
When CircleCI reads a github repository, it first looks for the .circleci directory in the root directory. This directory contains configuration files that CircleCI uses to determine how to build, test, and deploy your application.
The most important file in this directory is the config.yml file. This is file that contains all the confiugration information for your jobs and workflows.

If you selected the "faster" initialzation option in the previous step, you should see a pull request in your project to a branch titled 'circleci-project-setup' that initializes these files. If you selected the 'fast' option, you will have to create this file manually.

The initialized .circleci/config.yml should look like this:
```yaml
version: 2.1
jobs:
  say-hello:
    docker:
      - image: cimg/base:stable
    steps:
      - checkout
      - run:
          name: "Say hello"
          command: "echo Hello, World!"
workflows:
  say-hello-workflow:
    jobs:
      - say-hello
```

## Jobs
Like other CI/CD platforms such as Github Actions, CircleCI uses jobs to define a collection of steps which can be executed by a virtual machine or a fresh docker container.

```yaml
jobs:
  say-hello:
    docker:
      - image: cimg/base:stable
    steps:
      - checkout
      - run:
          name: "Say hello"
          command: "echo Hello, World!"
```
We can see in our config.yml file that the 'say-hello' job is defined. `docker` is calling a pre-built CircleCI Docker image, cimg/base, an Ubuntu Docker image. The image in this example contains the minimum tools required to operate a build on CircleCI, as well as Docker. For more information on available CircleCI pre-built images, see the [CircleCI images documentation]('https://circleci.com/developer/images').

In the steps of the job, we first checkout (meaning we retrieve the source code and set up the workspace), then we run the command "Say Hello", which echo Hello World! to the terminal. 

For our node project we will define the job: `publish`, which will look something like this:
```yaml
  publish:
    docker:
      - image: cimg/node:16.10
    steps:
      - checkout
      - run:
          name: Publish to NPM
          command: |
            npm set //registry.npmjs.org/:_authToken=${NPM_KEY}
            npm publish
```
This job uses the prebuilt node image from CircleCI running node version 16.10.

It will run checkout, and then run the commands required to publish our node package to NPM.

As you can see, we are using the environment variable `NPM_KEY`, since we don't want to include private data in our public config file. This is not yet defined in our CircleCI project. We will get to this in the [Environment Variables](#environment-variables) section.

## Environment Variables

## Workflows



## Summary
## Additional Reading