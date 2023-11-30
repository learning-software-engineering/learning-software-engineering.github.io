# Introduction to Azure Functions

This tutorial will help you get started with Azure Functions.

## What are Azure Functions

Azure Functions are a serverless computation service offered by Azure. They allow developers to build and deploy event-driven business logic. Benefits include:

- Very easy to set up and deploy (as we will soon see). Also has options to integrate with CI/CD
- Flexible on the language of choice
- Responds to different types of triggers; HTTP, time scheduler, Event from Azure CosmosDB, etc.
- Automatically scales
- Pay for what you consume, more cost effective than paying for a VM

Some cons:

- Azure Functions on the Consumption plan will have some latency when invoked for the first time in a while ("cold start")
- You're tied to a specific vendor (i.e. Microsoft)
- Azure Functions have a set execution time, it will stop running if execution is taking too long

## Azure Setup

Here we will go through everything we need to do in the [Azure Portal](https://portal.azure.com/).

### Account Signup

First, you will need an Azure account. If you don't have one, sign up for [Azure](https://azure.microsoft.com/).

**Disclaimer**: You will need a credit card. If you are new to Azure, you are eligible for a free tier. Moreover, you can link your UofT email to your Azure account to be for further credit. Microsoft will only put a small holding fee to verify your identity.

With that out of the way, once you create your account, you should now have a brand new Azure subscription.

### Create a Resource Group

We will be creating some resources in Azure, and every resource needs to go in a Resource Group. On the Home page, select "Resource Group", then select "Create resource group".

Make sure that it's using the correct subscription, give your resource group any name you want, and chooser region you want. Select "Review + Create" then "Create".

### Create a Storage Account

Azure Functions require that you have a storage account set up.

Go back to the Azure Portal Home page. In the navigation, search for "Storage Account". Select the "Storage Account" result and then select "Create Storage Account".

In the "Create a Storage Account" menu:

- Ensure subscription and resource group matches what you configured above
- Name your storage account `storfuncdemo` (feel free to change it)
- Region - East US
- Performance - Standard
- Redundancy - Locally Redundant Storage

Select "Advanced" and tick "Allow enabling anonymous access on individual containers". This is for the purpose of the demo, otherwise you'll wound up with 401 UNAUTHORIZED errors upon trying to connect to your deployed Azure Function.

Click on "Review" followed by "Create". This will deploy a brand new storage account for Azure. You should then see a "Go to Resource" button. Click it to be taken to the Overview page of your new storage account.

There is a section for "Access Keys" on the left hand side of the Resource Overview page, underneath "Security + Networking". Click it, and reveal the key and connection string for either key. Put these values in a Notepad.

### Create Azure Function App

Go back to the Azure Portal Home and search "Function App" in the Navigation. Select the resulting "Function App" and click "Create Function App".

Inside the Create Function App menu, we will configure the following:

- Subscription and Resource Group the same as above
- Function app name will be `yournamehere-func-demo`
- Runtime stack will be .NET 6 (choose your own if desired)
- Region is US East
- OS will be Windows
- Hosting will be Consumption

Select "Review + Create" and ensure your configuration for the Azure Function App is correct. Then select "Create".

## System Setup

First, install the [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli). I am on MacOS using Homebrew, so I will open up a terminal and run the following:

```bash
brew update && brew install azure-cli
```

Since we will be developing our functions in our local machine, go ahead and install the [Azure Functions Core Tools](https://learn.microsoft.com/en-us/azure/azure-functions/functions-run-local). Again, I will install using Homebrew:

```bash
brew tap azure/functions
brew install azure-functions-core-tools@4
```

Finally, this tutorial will be using C# as language of choice. Install the dotnet framework:

```bash
brew install dotnet@6
```

and add to your path:

```bash
echo 'export PATH="/opt/homebrew/opt/dotnet@6/bin:$PATH"' >> ~/.zshrc
```

Azure Functions can be developed in other languages like Python and JavaScript, so feel free to choose a different language if you'd like.

_Optional_: If you are using VS Code, go ahead and install the Azure Functions extension as well. This extension (and other Azure extensions) work really well with VS Code.

## Create an Azure Function

Open up a terminal and `cd` into a directory you'd like to create our Azure Function project. Once there, run `func init`. Select `dotnet` followed by `c#`, and your Azure Functions project will be initialized.

We will be creating an Azure Function that responds to HTTP triggers. If you installed the Azure Functions extension in VS Code:

1. Click the Azure extension button
2. Hover over "WORKSPACE" and select the Azure Function button
3. Select Create Function
4. Select HTTP Trigger template
5. Name your Function `funcHttp`
6. Provide a namespace `Example.Demo`
7. Select Anonymous for access rights

Alternatively, I have provided the generated example below. Create a `funcHttp.cs` file inside the top-level directory of the project, and add the following:

```cs
using System;
using System.IO;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;

namespace Example.Demo
{
    public static class funcHttp
    {
        [FunctionName("funcHttp")]
        public static async Task<IActionResult> Run(
            [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)] HttpRequest req,
            ILogger log)
        {
            log.LogInformation("C# HTTP trigger function processed a request.");

            string name = req.Query["name"];

            string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
            dynamic data = JsonConvert.DeserializeObject(requestBody);
            name = name ?? data?.name;

            string responseMessage = string.IsNullOrEmpty(name)
                ? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
                : $"Hello, {name}. This HTTP triggered function executed successfully.";

            return new OkObjectResult(responseMessage);
        }
    }
}
```

Finally, inside a terminal `cd` into the project and run `func start`. This will run all your defined Azure functions locally. In our case, we just have this single function that responds to HTTP requests. To test out your function, you can:

- Open a browser and enter the url http://localhost:7071/api/funcHttp?name=MyName
- Use a tool like `curl` or Postman to make a POST request to the server with a request body containing a "name".

That's it! You've created your first Azure function.

## Deploy an Azure Function

First, change the `AzureWebJobsStorage` property inside `local.settings.json` to the value of the connection string you copied when creating the Storage account.

Now, open up a terminal and run `az login`. This will open a browser page and prompt you to sign in to your Azure account.

`cd` into your project directory and run:

```
func azure functionapp publish myname-func-demo
```

Ensuring that `myname-func-demo` matches the name of the Function App resource you created earlier.

Give it some time, and your Azure function should now be deployed! The output of the deployment should contain a URL where you can actually invoke your function.
