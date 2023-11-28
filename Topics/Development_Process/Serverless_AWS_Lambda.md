# Serverless Computing with AWS Lambda

## Table of Contents

### [Introduction](#introduction-1)

### [Benefits of Serverless Computing](#benefits-of-serverless-computing-1)

### [Disadvantages of Serverless Computing](#disadvantages-of-serverless-computing-1)

### [AWS Lambda](#aws-lambda-1)

#### [Creating Lambda Functions in the AWS Console](#creating-lambda-functions-in-the-aws-console-1)

#### [Invoking Lambda Functions from the AWS Console](#invoking-lambda-functions-from-the-aws-console-1)

### [Additional Resources](#additional-resources-1)

## Introduction

It can be hard to set up and maintain your backend services. There are a ton of hosting options to choose from, and they can get pretty pricey.

Serverless computing allows you to to build and run applications without needing to manage servers. Cloud providers such as AWS, Azure, Google Cloud automatically provision servers based on demand.

## Benefits of Serverless Computing

As a developer, using serverless computing for your backend services has many benefits.

1. **Lower cost**: With serverless computing, you only pay for what you use. Traditional cloud computing typically requires you to pay for a fixed server, which often results in you having to pay for idle time and unused space.
2. **Scalability**: Because it is not up to the developer to allocate and maintain servers, developers do not have to worry about scaling servers up or down, as it is up to the cloud provider to do so.
3. **Easier maintenance**: The developer/user does not need to manage their backend services, as it is up to the cloud provider to maintain the servers. With containers or other deployment options, developers are responsible for updating and maintaining them.
4. **Deployment time**: Serverless functions finish deploying as soon as their code is updated, making them generally faster than containers, or virtual machines.

## Disadvantages of Serverless Computing

There are some situations where you might not want to use serverless computing.

1. **Boot-up time**: Serverless services are not constantly running, so when you make a request to code that hasn't been used in a while, you could face performance impacts.
2. **Long running processes**: Since you pay for what you use, it is usually not cost-effective to use serverless for longer running processes. In these cases, you might want to consider other options to run your backend services on.

## AWS Lambda

Lambda is a serverless compute service offered by Amazon Web Services (AWS). It allows you to run backend code triggered by events, such as other AWS services or your own services, without needing to provision or manage servers. And, you only pay for each request you make. In the free tier for AWS Lambda, you have access to 1 million free requests per month.

### Creating Lambda Functions in the AWS Console

To use Lambda, you must have an AWS account with an administrative user. Follow the instructions [here](https://portal.aws.amazon.com/billing/signup) on how to sign up.

To create a simple 'Hello World' function using Node.js or Python, see the tutorial, see the tutorial, [Create a Lambda Function with the console](https://docs.aws.amazon.com/lambda/latest/dg/getting-started.html#getting-started-create-function). Interpreted languages are easier to start off with since you can edit the code directly in the AWS console's code editor.

### Invoking Lambda Functions from the AWS Console

Once you have created your function in the console, there are many ways to invoke it. To invoke your function through the AWS console, see the tutorial, [Invoking the Lambda Function using the console](https://docs.aws.amazon.com/lambda/latest/dg/getting-started.html#get-started-invoke-manually). You can also invoke it through the AWS CLI, HTTPs endpoints, AWS SDK, other AWS services, and more. See [Invoking Lambda Functions](https://docs.aws.amazon.com/lambda/latest/dg/lambda-invocation.html).

Overall, Lambda functions are very versatile and can be a great alternative for running backend code.

## Additional Resources

Here are some more detailed resources to help you understand serverless as well as resources on how to use AWS Lambda to its fullest extent!

[Serverless computing vs. containers](https://www.cloudflare.com/learning/serverless/serverless-vs-containers/#:~:text=In%20a%20container%2Dbased%20architecture,automatically%20scales%20to%20meet%20demand.)

[AWS Lambda](https://aws.amazon.com/lambda)

[AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)

[Using AWS Lambda with other services](https://docs.aws.amazon.com/lambda/latest/dg/lambda-services.html)

Building Lambda functions with [Node.js](https://docs.aws.amazon.com/lambda/latest/dg/lambda-nodejs.html), [Typescript](https://docs.aws.amazon.com/lambda/latest/dg/lambda-typescript.html), [Python](https://docs.aws.amazon.com/lambda/latest/dg/lambda-python.html), [Ruby](https://docs.aws.amazon.com/lambda/latest/dg/lambda-ruby.html), [Java](https://docs.aws.amazon.com/lambda/latest/dg/lambda-java.html), [Go](https://docs.aws.amazon.com/lambda/latest/dg/lambda-golang.html), [C#](https://docs.aws.amazon.com/lambda/latest/dg/lambda-csharp.html), [Rust](https://docs.aws.amazon.com/lambda/latest/dg/lambda-rust.html)
