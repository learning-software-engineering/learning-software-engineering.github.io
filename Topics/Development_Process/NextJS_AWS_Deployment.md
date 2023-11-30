# Next.js app deployment using AWS EC2

## Table of Contents
### [Introduction](#introduction-1)
### [Getting started with Next](#getting-started-with-next-1)
### [Creating an EC2 Instance](#creating-an-ec2-instance-1)
### [Deploying your app](#deploying-app-1)

## Introduction
As a computer science student, mastering deployment processes is crucial for translating your coding skills into real-world applications. This guide will help 
a CSC301 student understand the deployment process of a Next.js app, a framework deeply rooted in React, on Amazon EC2, a cloud computing platform that is likely to come up in future professional scenarios. Whether you're aiming to enhance your software deployment expertise or just beginning to navigate this aspect of development, this tutorial is designed to equip CSC301 students with hands-on experience and insights into deploying web applications efficiently.

In a brief rundown, the process of deploying a Next.js app on AWS with EC2 consists of creating an EC2 instance (a virtual machine on the cloud), cloning the project's repo into that virtual machine, creating a build file of the app, then finally running the Next.js app as a background process. 

## Getting started with Next
Since this is primarily a guide in the deployment process, it is assumed that the reader has their Next.js app already created and ready to go. IF that's not the case, no problem!

Next.js is a react framework for the web, which enables you to create **full-stack** Web applications, all by extending React features. In addition to countless online rescources and excellent docs the Next.js team provides, getting started is even simpler with Next.js's command line interface tool, [`create-next-app`](https://nextjs.org/docs/app/api-reference/create-next-app). This helpful tool can really kickstart your development, and get your project off to a clean start.

## Creating an EC2 Instance
Now that you've hopefully got your hands a little dirty with Next.js develepment, its time to get your app off localhost and into the cloud! This process begins by creating an EC2 Instance.

1) Log in to AWS, or create a free account.(Note you will need to provide credit card information, but as long as you only use free services, you won't get billed).
2) Navigate to the **EC2 Dashboard**. ![image](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/62919149/935781b1-e426-453c-84d6-4dec25e53901)
3) Create a new instance by clicking **Launch Instance**.
4) Name your instance (name doesn't really matter), select the Ubuntu server for you Amazon Machine Image, select your desired instance type (micro for free tier), create a new RSA key pair(make sure you keep track of its location). That's it for config; select the **Launch Instance** button at the bottom of the screen.
5) Locate your instance by navigating to **All Instances**, then select your newly created instance. Open the **Security** tab, and click the security groups tab.![image](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/62919149/bc74382e-12b9-4041-9dc3-db1dcc61a8be)
6) Head to **Edit Inbound Rules**, and create a new rule with Type = Custom, Port range = the port your app runs on(by default, it will be 3000), Source=IPv4.

Now its time to connect to your EC2 instance from your machine.
1) Open a terminal in the same directory as the .pem key file that your downloaded earlier when creating your key pair.
2) Click the **Connect** tab while your EC2 instance is selected ![image](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/62919149/709744fd-9472-4ea1-a6c9-58468fb9b80e)
3) Copy and paste bullet point #3 and the example into your terminal and run both commands. Enter `yes` when asked if you wish to continue connecting. You should now be connected to your EC2 through shell!
4) Next, run `sudo apt update`
`curl -sL https://deb.nodesource.com/setup_lts.x | sudo -E bash -`
`sudo apt-get install -y nodejs` to install sudo and NPM.
5) Now, its time to clone your git repo into the EC2 instance. [This](https://stackoverflow.com/questions/19596974/ec2-how-to-clone-git-repository) stack overflow thread is an excellent step by step of creating a github deploy key. Only thing to note, all the commands ran should be done **inside** your local SSH terminal.
6) Once you've cloned your repo into the EC2 instance, all that's left to do is deploy!
## Deploying your app
1) In order to make your app feel at home, run `npm i` to install all your node modules into this local repository.
2) Next, build your project, by running `npm run build'. Your output should look something like this.![image](https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/62919149/a5ca3219-0488-491e-bdbf-b3513f730811)
3) Finally, to deploy your app as a background process on your cloud server, run `npm start &`.
4) Using the public IPv4 link, with `:YOUR_PORT_NUMBER`, you should see your deployed Next.js app up and running!



