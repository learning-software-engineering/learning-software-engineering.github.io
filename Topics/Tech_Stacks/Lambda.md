# Learning AWS Lambda

## Table of contents

### [Introduction](#introduction)

### [Why Use Lambda?](#)

## Introduction

<img src="./assets/image.png" width="100" height="100" style="float: right; margin-right: 10px;">

AWS Lambda is a [serverless compute](https://en.wikipedia.org/wiki/Serverless_computing) service by Amazon Web Services (AWS), enabling you to execute code without the need to manage underlying servers. This event-driven platform responds to various triggers, such as file uploads, HTTP requests, or database modifications, allowing for seamless execution of functions in response to these events.


Thanks to Lambda's simplicity, getting started is fairly simple. Explore the official AWS documentation and resources tailored to assist beginners in understanding Lambda and leveraging its capabilities effectively:

- [Getting Started with Lambda](https://docs.aws.amazon.com/lambda/latest/dg/getting-started.html)
- [AWS Lambda Resources](https://aws.amazon.com/lambda/resources/?aws-lambda-resources-blog.sort-by=item.additionalFields.createdDate&aws-lambda-resources-blog.sort-order=desc)


## Why Use Lambda?

- **Serverless Computing:** Eliminates server management, allowing focus solely on code development and execution.
- **Event-Driven Model:** Responds to various triggers like HTTP requests, database changes, or file uploads.
- **Scalability:** Scales automatically in response to the incoming workload or event-driven triggers.
- **Cost-Efficiency:** Pay only for the compute time consumed, with no charges during idle periods.
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



## Additional Resources

- [AWS Documentation](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)

- [AWS Lambda Pricing](https://aws.amazon.com/lambda/pricing/)

- [Serverless 101: AWS Lambda (A 9 min video intro to AWS)](https://aws.amazon.com/lambda/getting-started/)
- (https://www.serverless.com/examples/aws-python-simple-http-endpoint/)