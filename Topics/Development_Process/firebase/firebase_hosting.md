# Using Firebase Hosting 
## Table of Contents:
### [Introduction](#introduction-1)
### [Step By Step Tips](#Step_By_Step_Tips-1)
### [External Resources](#External_Resources-1)

## Introduction

If you want a free and reliable resource to deploy you webapp, ios, android, etc. 
you can use firebase!

First, you will need to login to [Firebase](https://firebase.google.com/), click the console button on the top right corner, create a new project as instructed, under build, click on Hosting.

## Step By Step Tips

You can deploy your website using firebase, and have a URL that users can click on to access your website.


To set up firebase hosting for your project, in your local repository, run the following command in your terminal:

```
npm i firebase -tools -D
```
The above command is not what is given on the firebase console, but from experience, this results in no errors down the line. 

This creates a node_modules folder that you will use for later commands.

To initialize your project, run 

```
node_modules/.bin/firebase login
```
and later run:
```
node_modules/.bin/firebase init
```
To see your website on localhost, run

```
node_modules/.bin/firebase serve
```

When you are ready to deploy your website, run 
```
node_modules/.bin/firebase deploy
```
Using the node_modules folder will reduce many potential errors that may arise. Otherwise, you can follow the step by step guide that the firebase website provides itself. 

## External Resources
Below is a tutorial in learning the firebase Hosting. It goes through step by step, how to set up your hosted website.
[Firebase Hosting Tutorial](https://firebase.google.com/docs/hosting)