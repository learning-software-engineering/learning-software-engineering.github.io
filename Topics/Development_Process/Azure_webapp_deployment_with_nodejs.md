# Learning Azure for Deployment

## Table of Contents
### [Introduction](#introduction)
### [Getting Started](#getting-started)
### [Installation](#installation)
### [Deployment](#deployment)
### [CI/CD with Github Actions](#ci/cd-with-github-actions)
### [Budgets](#budgets)
### [Azure Terminology](#azure-terminology)
### [References](#references)

## Introduction

This article will help users be able to get an idea of what Azure is, and how to get started with it to use with their own applications in personal projects, hackathons, assignments, or more! 

Azure is a [cloud service provider](#azure-terminology) by Microsoft that provides extensive services, including application hosting, messaging, data, storage, and more, for developers to leverage when building applications. 

It is one of the most popular [cloud service providers](#azure-terminology), including Amazon Web Services and Google Cloud Platform, and if you're an 18+ year old student, you can get $100 in Azure credit with the [Github Student Developer Pack](https://education.github.com/pack). 😁

You can read more about the most popular [cloud service providers](#azure-terminology) and comparisons between them [here]([cloud service providers](https://www.digitalocean.com/resources/article/comparing-aws-azure-gcp)).

## Getting Started

Before being able to work with Azure, you must first create an account [here](https://azure.microsoft.com/en-ca/get-started/azure-portal). As mentioned earlier, after creating your account, you can get $100 in Azure credit with the [Github Student Developer Pack](https://education.github.com/pack) if you're an 18+ year old student.

After creating an account, make sure you have an Azure subscription (such as Azure for Students above) to use.

## Installation

The Azure Portal is simple, and easy to use to interact with and create Azure services. Aside from your Azure account, no other setup is necessary.

For the examples in this article, you'll also require the Azure CLI. Instructions to install it on your computer can be found [here](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) 

Although not covered in this article, other alternatives for interacting with Azure can be found [here](https://learn.microsoft.com/en-us/azure/developer/intro/azure-developer-create-resources).

While we won't be going into too much detail here, you will need to have Node.js and npm installed to follow along and get a basic Node.js web app with Express running (install Node.js and npm together for your system [here](https://nodejs.org/en/download/current)). If you're working with another tech stack, links to help you find appropriate documentation and examples will be provided.

## Deployment

Azure has a variety of ways to host your application, including Azure App Service, Azure Functions, Azure Container Instances, Azure Kubernetes Service, and more, which you can choose to suit your specific usecase. 

See more about the different kinds of hosting options and reasons to choose one over the other [here](https://learn.microsoft.com/en-us/azure/developer/intro/hosting-apps-on-azure).

The following will detail how one would deploy a Node.js Web App using Azure App service, and integrate it with Github Actions for CI/CD.

### Azure App Service

Azure application service allows you to build and host web applications, mobile backends and RESTful APL in the selected programming language without managing the infrastructure. It provides automatic scaling and high availability, supports Windows and Linux, and supports automatic deployment from GitHub, Azure Devops or any Git repository. You can refer to our quick start, tutorials and examples to learn how to use Azure application services.

#### Create Web app on Azure

From Microsoft's official documentation, here is a quick tutorial to get an example Node.js project deployed:

[deploy web app with node js on Azure](https://learn.microsoft.com/en-us/azure/app-service/quickstart-nodejs?tabs=linux&pivots=development-environment-vscode)

Alternatively, and possibly easier, you can make a very basic web app with Node.js and Express by doing the following:

Note: Learn more about Node.js and Express apps [here](../Tech_Stacks/Express.md).

1. Create a project directory for the Node.js web app
2. In the root of your project directory, run `npm init` in the terminal (you should have npm and Node.js installed).
3. In the terminal, run `npm install express`.
4. Write the following in the directory in a new file, `server.js` (or whatever name you entered as the entry point during `npm init`).
    ```javascript
        const express = require("express");

        const app = express();

        const PORT = 3000

        app.get("/", (req, res) => {
            res.send(`
            <h1>CSC301 A2 Demo successfully deployed!</h1>
            <h2>You did it!</h2>
            `)
        });

        // Set up server to listen on port 3000
        app.listen(PORT, () => {
            console.log(`Listening on port ${PORT}`);
        });
    ```

Note that the file structure inside your project directory should currently look something like this:

```
├── node_modules
├── package.json
├── package-lock.json 
├── server.js 
└── .gitignore
```

Have this code in a Github repository to later integrate with Github actions.

Now, you have two options:

1. Deploy your Web App with the Azure portal (if you proceed with this option, the Azure portal will immediately integrate CI/CD with Github Actions)

    On the Azure Portal, navigate to **App Services**: 

    - Click on the **Create** dropdown and select **Web App**. 
    - For this simple example, you'll only need to fill out the first tab, **Basics**.
    - Choose a subscription (Azure for Students if you've used the Github Student Developer Pack), a resource group (or create one), and create a name for your Web App.
    - Choose `Code` for `Publish`, and the appropriate version of Node for your runtime stack.
    - The default region and Linux plan defaults should suffice, but make sure to **change the Pricing Plan to Free F1 (Shared infrastructure)**.
    - Select **Review + Create** and then **Create**.
    
    
    After you get a notification that the deployment succeeded, navigate to your web app on the Azure portal. 
    
    - On the sidebar, select **Deployment Center**.
    - As the code source, select Github under **Continuous Deployment** in the dropdown (you should have your code in a Github repository).
    - Select the appropriate organization, repository, and branch to deploy.
    - Click **Save** and wait.
    - After a couple minutes, confirm that you can access the deployed URL, and that there's a workflow file in your Github repository.

    Congratulations, you've deployed a web app using Azure, and integrated it with Github Actions too!


2. Deploy your Web App with the Azure CLI (if you proceed with this option, you'll need to follow along with the [CI/CD with Github Actions](#cicd-with-github-actions) instructions to integrate Github Actions)

    In your terminal:

    - If you haven't already, follow the instructions in [Installation](#installation) to install the Azure CLI
    - Ensure that you've followed the setup instructions in the [official documentation](https://learn.microsoft.com/en-us/cli/azure/get-started-with-azure-cli)
    - Enter the following command **while in your project directory's root folder**: `az webapp up --sku F1 --name <your_webapp_name>` (learn about the parameters [here](https://learn.microsoft.com/en-us/cli/azure/webapp?view=azure-cli-latest))
    - Once the command successfully executes, visit the URL in the response object you got. If you see your web app (note that it may take a minute or two), congratulations, you've successfully deployed your web app on Azure!

## CI/CD with Github Actions

You can use Github Actions with Azure to automate workflows during your software development. Given the different hosting and deployment options mentioned above, there is a different way to use Github Actions to work with whichever hosting option you've chosen.

Below, we'll continue with our previous example of a Node.js Web App using Azure App Service, but you can find examples for different hosting options [here](https://learn.microsoft.com/en-us/azure/developer/github/deploy-to-azure).

Note that before continuing with implementing CI/CD with Github Actions, you should have a working [Azure App Service](#azure-app-service) app.

### Using Github Actions to Deploy to Azure App Service

The workflow can be set up in 1 of 2 ways:  using the Deployment Center to generate the workflow file for your Azure App service and tech stack in a Github repository, or manually.

If you deployed your web app using the Azure portal, congratulations, the workflow file was set up automatically for you! You're all done! If you deployed your web app using the Azure CLI, follow along, there's a couple more steps!

I found the official documentation (found at the link below) to be a clear and quick tutorial for how to set up Github Actions for your Azure App Service web app, which guides you through whichever workflow setup method you've chosen, with instructions for the various supported programming languages you may be using.

[Using Github Actions with Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/deploy-github-actions?tabs=applevel)

Some issues that I've seen occur in this process include:

- The workflow script not being able to find a file, in which case you may want to modify your file structure or the workflow file itself to properly reference the location.
- Npm script errors if you haven't set up a test script. You can fix this by removing the calls to these scripts (ie. remove `npm run test` and `npm run build` from the workflow file if you don't have these)

Once you've completed the steps in the documentation and see that the Github Actions workflow ran successfully, congratulations, you've deployed a web app on Azure integrated with Github Actions for CI/CD!

## Cost Management with Azure

There are multiple scary stories of people learning to use cloud service providers, like Google Cloud Platform or AWS, and as they set up different services, when the bill comes around, they're faced with a staggeringly large bill. 

It can be scary to learn something new when such consequences are possible, but to avoid that, Azure provides a handful of tools to use to ensure that you are in control of what you spend.

### Cost Analysis

In the Azure portal at **Billing** > **Cost Management** > **Cost Analysis**, you're able to view a breakdown of your costs and spending over time, and either with respect to your entire account, or if you want to be more specific, you can also scope to specific resource groups. With this, you're able to analyze your spending to be more aware of where most of your costs are going.

A more detailled look at cost analysis can be found [here](https://learn.microsoft.com/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis).

### Budgets & Alerts

While it is useful to be able to analyze your spending, you won't be doing this around the clock, so you still need a way to be informed of your spending if it starts getting out of hand. In come budgets and alerts. 

A budget allows you to track your spending across your services, set a limit, and be notified as the cost across your services approaches this limit. In the **Cost Management + Billing** > **Cost Management** > **Budgets** page, you are able to create a new budget. 

When creating a new budget, you're able to choose some important fields, including the **reset period** (the time period for the budget), the **creation date** (when the budget begins), the **expiration date** (when the budget expires), and the **amount** (the limit amount you're willing to spend).

After filling these in, you're able to set up alerts for this budget. Alerts can be triggered either by the actual usage of your budget, or the forecasted usage, and they can be triggered at certain portions of your budget being used (ex. 30%, 50%, 80%). When these alerts are triggered, you (and other recipients) that you indicated as the alert recipients, will receive email notifications.

See more about cost management in Azure's official [documentation](https://learn.microsoft.com/en-us/azure/cost-management-billing/costs/).

## Azure Terminology

- **Cloud Service Provider**: An organization providing cloud services, such as storage, security, databases, and  applications, typically appealing for its flexibility to pay only for what you use. Examples include Azure, Amazon Web Services and Google Cloud Platform.

- **Resource Group**: A logical grouping of resources, typically by application, so pretty much a box of resources (ex. databases, storage, app service) that are grouped together for a solution or application.

See other keywords in Azure's official [documentation](https://learn.microsoft.com/en-us/azure/developer/intro/azure-developer-key-concepts).

## References and Helpful Resources

- [Hosting Apps on Azure](https://learn.microsoft.com/en-us/azure/developer/intro/hosting-apps-on-azure)
- [Deploy Node.js Web App with Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/quickstart-nodejs?tabs=linux&pivots=development-environment-vscode)
- [Deploy App Service with Github Actions](https://learn.microsoft.com/en-us/azure/app-service/deploy-github-actions?tabs=applevel)
- [Azure Cost Management](https://www.youtube.com/watch?v=7w88KBVesPI&t=320s)