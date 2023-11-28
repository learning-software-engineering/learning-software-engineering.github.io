# Learning AWS Lambda

## Table of contents

#### [Introduction](#Introduction-1)
#### [Why Use Lambda?](#why-use-aws-lambda-1)
#### [Limitations of AWS Lambda](#Limitations_of_AWS_Lambda-1)
#### [Example Use Cases](#example-use-cases-1)
#### [Getting Started](#getting-started-1)
#### [Additional Resources](#Additional-Resources-1)
## Introduction
<img src="https://miro.medium.com/v2/resize:fit:506/1*VKfs2PGyMm5FZfJD72kYCw.png" width="100" height="100" align="right">

AWS Lambda is a [serverless compute](https://en.wikipedia.org/wiki/Serverless_computing) service by Amazon Web Services (AWS), enabling you to execute code without the need to manage underlying servers. This event-driven platform responds to various triggers, such as file uploads, HTTP requests, or database modifications, allowing for seamless execution of functions in response to these events.


## Why Use AWS Lambda?

- **Serverless Computing:** Eliminates server management, allowing focus solely on code development and execution.
- **Event-Driven Model:** Responds to various triggers like HTTP requests, database changes, or file uploads.
- **Scalability:** Scales automatically in response to the incoming workload or event-driven triggers.
- **Cost-Efficiency:** Pay only for the compute time consumed, with no charges during idle periods (you won't waste money as your 301 project sits idle on a running EC2 server).
- **Multiple Language Support:** Allows coding in various languages like Python, Node.js, Java, C#, Go, and Ruby.
- **Integrations:** Seamlessly integrates with other AWS services for comprehensive cloud solutions.
- **Faster Time to Market:** Speeds up development cycles by focusing on code rather than infrastructure.
- **Microservices Architecture:** Ideal for building and deploying microservices-based applications.
- **Real-Time Processing:** Facilitates real-time data processing and analysis for various applications.
- **Flexibility and Versatility:** Suitable for a wide range of applications, from web backends to IoT and data processing.

## Limitations of AWS Lambda 

- **Long-Running Tasks:** Lambda has execution time limitations (currently 15 minutes). If your tasks consistently exceed this limit, an alternative computing solution might be more suitable.
- **Predictable Workloads:** For workloads with consistent, predictable traffic, where maintaining and managing a server might be more cost-effective, a traditional server approach could be preferred over the event-driven nature of Lambda.
- **Stateful Operations:** Lambda functions are stateless by design. If your application heavily relies on maintaining state between function invocations, it might not be well-suited for Lambda.
- **Resource-Intensive Workloads:** Applications with resource-intensive processes that demand high CPU, memory, or specialized hardware might face limitations within the constrained environment Lambda provides.
- **Cold Start Issues:** Lambda functions experience a "cold start" delay when invoked for the first time or after a period of inactivity. Applications sensitive to latency might find this initial delay unacceptable.


## Example Use Cases
### 1. Web Applications

A user clicks on the web app to get local weather information. Then the App makes a REST API call to an endpoint triggering the Lambda. The Lambda runs the necessary code to retrive the local weather information from the db and returns data back to the user. 

<img src="https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-WebApplications%202.c7f8cf38e12cb1daae9965ca048e10d676094dc1.png">

### 2. File Processing 
Solving cross-device development challenges typically involves high costs and manual tasks, slowing down development teams. Yet, AWS Lambda offers a solution: automate a multi-platform media and content delivery pipeline. For example, a photograph is taken, and is uploaded to a database like an S3 bucket. Then that triggers a Lambda which runs the image resizing code into sizes that fit mobile, tablet, and laptop. 


Netflix showcases an excellent use case, leveraging AWS Lambda to process over 70 billion hours of content across 60 million users, transforming media files into over 50 formats.

<img src="https://d1.awsstatic.com/product-marketing/Lambda/Diagrams/product-page-diagram_Lambda-RealTimeFileProcessing.a59577de4b6471674a540b878b0b684e0249a18c.png">


## Getting Started

Thanks to Lambda's simplicity, getting started is simple. 

#### 1. Create a Lambda function with the console


1. Go to the [Functions section](https://console.aws.amazon.com/lambda/home#/functions) within the Lambda console.
2. Click on **Create function.**
3. Choose **Author from scratch.**
4. Under **Basic information*:**
   - Enter **myLambdaFunction** as the Function name.
   - Select either Node.js 18.x or Python 3.11 as the Runtime.
   - Keep the architecture set to x86_64.
5. Click on **Create function.**


Lambda creates a function that returns the message `Hello from Lambda!`

#### 2. Invoke the Lambda 

To create the test event
1. In the **Code source** pane, choose **Test**.

2. Click the **Test** button. 

Just like that you have created your first hello world Lambda function and invoked it.


## Additional Resources

Explore the official AWS documentation and resources tailored to assist beginners in understanding Lambda and leveraging its capabilities effectively:

- [Getting Started with Lambda](https://docs.aws.amazon.com/lambda/latest/dg/getting-started.html)
- [AWS Lambda Resources](https://aws.amazon.com/lambda/resources/?aws-lambda-resources-blog.sort-by=item.additionalFields.createdDate&aws-lambda-resources-blog.sort-order=desc)
- [AWS Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)
- [AWS Lambda Pricing](https://aws.amazon.com/lambda/pricing/)
- [Serverless 101: AWS Lambda (A 9 min video intro to AWS)](https://aws.amazon.com/lambda/getting-started/)
