# Django Project Deployment: AWS, Vercel, and Railway

## Table of Contents:
### [Introduction](#introduction-1)
### [A Guide to Choosing the Right Hosting Service](#a-guide-to-choosing-the-right-hosting-service-1)
#### [Where to Start](#where-to-start-1)
#### [Advantages and Disadvantages (AWS, Vercel, Railway)](#advantages-and-disadvantages-aws-vercel-railway-1)
#### [How to Decide on the “Right” Hosting Service](#how-to-decide-on-the-right-hosting-service-1)
### [Deploying a Django Project on AWS](#deploying-a-django-project-on-aws-1)
#### [EC2 vs. Elastic Beanstalk (EB)](#ec2-vs-elastic-beanstalk-eb-1)
#### [Deploying on AWS: The Hard (but Better) Way (EC2)](#deploying-on-aws-the-hard-but-better-way-ec2-1)
#### [Deploying on AWS: The Easy Way (EB)](#deploying-on-aws-the-easy-way-eb-1)
### [Deploying A Django Project on Railway](#deploying-a-django-project-on-railway-1)
### [Deploying A Django Project on Vercel](#deploying-a-django-project-on-vercel-1)

## Introduction

This article will specifically focus on the deployment of a new Django project. Primarily, this will serve as an initial introduction to some current popular hosting services (AWS, Vercel, and Railway), serving as more of a guide to understanding which platform is right for you and your team before. Once you feel confident on the platform that you wish to deploy on, we will then go into detail on how to successfully deploy your new Django project. After reading this article, you should hopefully have enough knowledge and resources to know which hosting service is best for you (and your team) and start deploying your Django project. 

Note: For the sake of consistency, no prior knowledge of DevOps or deployment will be assumed. 

## A Guide to Choosing the Right Hosting Service

### Where to Start

Deployment and DevOps can be a dreadful and daunting task for many. While starting from the beginning it is important to remember, that like any other skill, this will probably take many iterations of past failures before success. Given the vast array of popular hosting services, it is easy to get lost before you can even choose a hosting service. To ease this process, this article collates 3 free-to-use, prominent, and reliable hosting services based on functionality, ease-of-learning, and desirability to learn DevOps: Amazon Web Services (AWS), Vercel, and Railway.

### Advantages and Disadvantages (AWS, Vercel, Railway)

Each of the 3 hosting services focused on in this article have their own distinct advantages and disadvantages. To compare across these platforms, we will do so in a table format. Note that for the majority of these hosting platforms, you will need a GitHub Account, and a GitHub Repository with your Django Project on it.

It is highly suggested you read through the following table carefully to learn which service you and your team may prefer before continuing:


| Criteria | AWS (EC2/EB) | Vercel | Railway   |
| ---------| ------------ | ------ | --------- |
| Complexity (Deployment Difficulty) | <ul><li>The most difficult to deploy on</li></ul> | <ul><li>Relatively easy to deploy</li></ul> | <ul><li>The easiest platform to deploy on</li></ul> |
| Price of Hosting (Price Charged for Hosting Time) | <ul><li>Completely free-to-use and host on (for 1 project of your choice)</li></ul> | <ul><li>Completely free-to-use and host on (for 1 project of your choice)</li></ul> | <ul><li>Free-to-use for only ~3 weeks per month</li></ul> |
| Price of Storage (Price Charged for Hosting Storage) | <ul><li>Completely free</li></ul> | <ul><li>Only enough to store code behind Django</li><li>No storage for SQLite Database and media files</li></ul> | Free until 100GB of total storage |
| Security | <ul><li>Minimal security</li><li>SSL certificate to communicate over HTTPS requires a paid for domain</li><li>Process to obtain SSL certificate with domain can be daunting</li></ul> | <ul><li>As Vercel own their own domain, all hosted services communicate over HTTPS for free</li></ul> | <ul><li>As Vercel own their own domain, all hosted services communicate over HTTPS for free</li></ul> |
| Longevity | <ul><li>Most stable in the long-term (storage and reliability wise)</li></ul> | <ul><li>Least stable in the long term for larger backend servers</li><li>Consider whether usage is purely API based, or also includes storage</li></ul> | <ul><li>Relatively reliable for long term projects</li><li>Consider growth of backend (and potential SQLite Database)</li></ul> |
| Best Features | <ul><li>Customizability (multiple ways to deploy)</li><li>Most valued among employees to learn</li><li>Essentially unlimited storage and hosting for free (for 1 hosted service)</li></ul> | <ul><li>Automated deployment is made very easy (add GitHub Action to your Forked Repo)</li><li>Little to no set-up required</li><li>Easy and free communication over HTTPS</li></ul> | <ul><li>Automated deployment is made very easy (add GitHub Action to your Forked Repo)</li><li>Very little set-up required</li><li>Easy and free communication over HTTPS</li></ul> |
| Pain Points | <ul><li>Set-up can be long and complex</li><li>May require learning other tech stacks (e.g. NGINX, Docker)</li><li>Processes to setup automated deployment and acquiring an SSL certificate (for HTTPS communication) are long and complex</li></ul> | <ul><li>No free storage for SQLite Database and potentially even code</li><li>Must use external database (e.g. MongoDB) in tandem</li></ul> | <ul><li>Month-to-month expense in hosting time</li><li>Free storage until 100GB requires entering Credit Card information</li><li>Sans payment details, hosting service offers 1GB of storage</li></ul> |

### How to Decide on the Right Hosting Service

Now that you have enough knowledge to know the pros and cons behind each hosting service, it is now time to proceed with one method. This section of the article will help you decide which hosting service is right for you.

The following is a list of suggested steps and conversations you should have with both your team and your partner before deciding on which hosting platform to proceed with:

1) Discuss with your partner if they would be willing to pay for hosting, especially for security reasons (how much are they willing to pay? Is that enough for a domain to host on AWS over HTTPS? Or can they pay enough to host on Railway provided you are not limited by their storage limit?)
2) If you are using Django as a backend framework, discuss with the Frontend team on which web application protocol you will communicate over (HTTP or HTTPS?)
3) Discuss the benefits and downfalls of each service with your DevOps/Backend team to come to a consensus on which platform you want to proceed with (are you using SQLite or another database service such as MongoDB? Can you expect the code to grow beyond what Vercel has? Can you expect your SQLite database to go beyond Railway’s storage limits? Are you willing to put in the time and effort to learn Docker and AWS the right way?)

## Deploying a Django Project on AWS

### EC2 vs. Elastic Beanstalk (EB)


- AWS itself has two main methods that are the most favourable for beginners to deploy Django projects on. In this part of the article we will discuss the differences between the two to help you decide which one you want to proceed with (should you have decided on moving forward with AWS from the last section).

- The first key difference to note is the potential for automating your workflow. EB is known to be much more user friendly and serves much more as a personal deployment option rather than a developer’s choice. The main reasoning behind this is due to its inbuilt nature that favours a local repository rather than a group (GitHub) repository with proper workflow capabilities. On the other hand, EC2 itself does much more natively support GitHub repositories, making it a better option (for the general case).

- The second distinction is in their setup and deployment process. EC2 is much more hands on, and should you want your application to be accessible without your computer constantly having an AWS console open in a browser tab, it will require you to learn NGINX and Docker. Conversely, EB is easier to get started with, as it abstracts away much of the development process that would otherwise be required to set up an EC2 instance (e.g. configurations, load balancers).

- While both EC2 and EB have their own characteristics, it is important to note that the previously mentioned limitations to AWS applies to both of these.

### Deploying on AWS: The Hard (but Better) Way (EC2)

- To deploy on EC2, the following video is highly recommended. Note that the following assumptions are made throughout this video and it ensure you meet them before starting the tutorial:
	
	1) You have a GitHub repository with your Django project on it
	2) You have a GitHub Token that authorises the sharing and deploying of that repository, [click here for more information on how to set this up](https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
	3) You have an AWS account, click here for more information on how to set this up
	4) Install `pip` and `virtualenv` before you begin, [click here for more information on how to set this up](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/)

- Additionally, the following are tips that are recommended to encounter as little debugging as possible:

    1) Make your root directory for the project one level higher than the project files, as seen below:
    2) When making anything relating to your EC2 instance, ensure you note down the region of the AWS server you are working on (seen in the top right corner of the screen)
    3) You can generate a `requirements.txt` file after activating your virtual environment by using the `pipreqs` package, click here to learn more about `pipreqs`
    4) If you are encountering CORS/CSRF errors, [click here for potential solutions](https://stackoverflow.com/questions/38841109/csrf-validation-does-not-work-on-django-using-https)

&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <centre>[![](https://markdown-videos.deta.dev/youtube/7O1H9kr1CsA)](https://youtu.be/7O1H9kr1CsA)</centre>

### Deploying on AWS: The Easy Way (EB)

- To deploy on EB, the following video is highly recommended. Note that the following assumptions are made throughout this video and it ensure you meet them before starting the tutorial:
	
	1) You have an AWS account, click here for more information on how to set this up
	2) Install `pip` and `virtualenv` before you begin, [click here for more information on how to set this up](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/)

- Additionally, the following are tips that are recommended to encounter as little debugging as possible:

	1) When making anything relating to your EC2 instance, ensure you note down the region of the AWS server you are working on (seen in the top right of the screen)
	2) After making and activating your virtual environment, ensure you install `gunicorn` by running `pip install gunicorn` within the terminal
	3) You may need to set a third line on your `./ebextenstions/django.config` to the following line: `WSGIPath: <project_name>/wsgi.py`
	4) If you are encountering CORS/CSRF errors, [click here for potential solutions](https://stackoverflow.com/questions/38841109/csrf-validation-does-not-work-on-django-using-https)

&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <centre>[![](https://markdown-videos.deta.dev/youtube/51YwXvJ9LOE)](https://youtu.be/51YwXvJ9LOE)</centre>

## Deploying a Django Project on Railway

- To deploy on Railway, the following video is highly recommended. Note that the following assumptions are made throughout this video and it ensure you meet them before starting the tutorial:
	
	1) You have a GitHub repository with your Django project on it
	2) You have a GitHub Token that authorises the sharing and deploying of that repository, [click here for more information on how to set this up](https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
	4) Install `pip` and `virtualenv` before you begin, [click here for more information on how to set this up](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/)

- Additionally, the following are tips that are recommended to encounter as little debugging as possible:

    1) Ensure you set your root directory to the Django project in the settings, as shown here:
    2) Ensure you carefully follow the static files and directory process carefully, this is very important and you should ensure your static files are loading (by checking for common HTML/CSS elements in default Django error/admin panel web pages). This is key and necessary for CORS/CSRF and are vital should you be communicating with a Frontend
    3) If you are encountering CORS/CSRF errors, [click here for potential solutions](https://stackoverflow.com/questions/38841109/csrf-validation-does-not-work-on-django-using-https)

&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <centre>[![](https://markdown-videos.deta.dev/youtube/NUqtNglEcCU)](https://youtu.be/NUqtNglEcCU)</centre>

## Deploying a Django Project on Vercel

- To deploy on Railway, the following video is highly recommended. Note that the following assumptions are made throughout this video and it ensure you meet them before starting the tutorial:
	
	1) You have a GitHub repository with your Django project on it
	2) You have a GitHub Token that authorises the sharing and deploying of that repository, [click here for more information on how to set this up](https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
	4) Install `pip` and `virtualenv` before you begin, [click here for more information on how to set this up](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/)

	Additionally, the following are tips that are recommended to encounter as little debugging as possible:

	1) If you are encountering CORS/CSRF errors, [click here for potential solutions](https://stackoverflow.com/questions/38841109/csrf-validation-does-not-work-on-django-using-https)

&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; <centre>[![](https://markdown-videos.deta.dev/youtube/ZjVzHcXCeMU)](https://youtu.be/ZjVzHcXCeMU)</centre>
