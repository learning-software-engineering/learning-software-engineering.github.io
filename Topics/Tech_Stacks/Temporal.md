# Temporal For Workflow Orchestration

## Table of contents
### [Introduction to Temporal](#introduction-to-temporal)
### [How does Temporal work](#how-does-temporal-work)
### [Your first workflow](#your-first-workflow)
### [Additional Resources](#additional-resources)

## Introduction to Temporal
Temporal is an open-source, stateful, distributed application orchestration platform that allows you to build scalable and resilient applications. 
It simplifies the development of complex, long-running workflows and helps you manage the state and execution of various processes within your application. 
Temporal is designed to handle the challenges of building mission-critical, distributed systems by providing a powerful way to model, manage, and execute your business logic.

- Stateful Workflows: 
Temporal enables the development of stateful workflows that can run for an extended period, coordinating various tasks and activities.

- Resilience: 
It helps you build highly resilient applications by managing retries, timeouts, and error handling, ensuring that your workflows can withstand failures in a distributed environment.

- Language Agnostic: 
Temporal is language-agnostic, allowing you to write workflows in the programming language of your choice.

- Durability: 
It ensures the durability of your application state by persisting it in a reliable storage system, making it possible to recover and resume workflows even after system failures.

- Scalability: 
Temporal is built to scale horizontally and handle high loads, making it suitable for applications of all sizes, from small projects to large, enterprise-grade systems.

## How does Temporal work
Temporal operates by decoupling the application's business logic from the execution environment. It does this through the following components and principles:

- Workflows: 
Workflows are long-running, stateful processes that encapsulate the application's business logic. 
They can wait for events, make decisions, and coordinate various activities. Temporal ensures that workflows continue to execute reliably, even in the face of failures.

- Activities: 
Activities are individual units of work that the workflow can execute. They can be short-lived functions or services, and Temporal manages their execution and retries.

- Temporal Server: 
The Temporal Server is responsible for managing workflow and activity execution. It maintains a history of events for each workflow and ensures that they are executed correctly.

- Durable State: 
Temporal stores the durable state of workflows and activities in a persistent storage system, allowing it to recover and resume them even after system outages.

- Workers: 
Workers are application components that interact with the Temporal Server to execute workflows and activities. They listen for tasks, execute them, and report the results back to the server.

- Execution Semantics: 
Temporal provides guarantees about the execution of workflows, ensuring that they remain deterministic and predictable, even when executed across different environments or after failures.

## Your first workflow
To create a simple "Hello, World!" program using Temporal in TypeScript, you need to set up a basic workflow and use the Temporal API to execute it. Here's how you can do it:
#### Setup Your TypeScript Project
Before you begin, make sure you have TypeScript installed. You can create a new TypeScript project using a tool like `npm` or `yarn`. First, create a new directory for your project, navigate to it in the terminal, and then initialize a new TypeScript project:

```bash
mkdir temporal-hello-world
cd temporal-hello-world
npm init -y
npm install --save @temporalio/sdk
npm install --save typescript
```
#### Create a TypeScript Workflow
Create a new TypeScript file, e.g., hello-world.ts, and write your Temporal workflow code in it.

```typescript
import { Connection, Worker } from '@temporalio/sdk';

// Define your workflow function
async function helloWorld(): Promise<void> {
  console.log('Hello, World!');
}

// Create a Temporal Connection
const connection = new Connection();

// Create a Worker that listens for workflow tasks
const worker = new Worker(connection, 'your-namespace');
worker.registerWorkflow('hello-world', helloWorld);

// Start the worker
worker.run();
```

In this code, we import the necessary Temporal SDK components, define a simple workflow function helloWorld that logs "Hello, World!", create a connection to Temporal, create a worker for your specific namespace, register the hello-world workflow, and start the worker.

#### Compile and Execute the Workflow
To compile your TypeScript code and execute the workflow, you can use the TypeScript compiler (tsc) to transpile the TypeScript code into JavaScript and then execute the JavaScript code. Run the following commands:

```bash
tsc hello-world.ts
node hello-world.js
```

This will compile your TypeScript code into JavaScript and run the workflow. You should see "Hello, World!" printed to the console.

#### Start a Temporal Server
To run Temporal workflows, you'll need a Temporal server running. You can set up a local server using the Temporal Docker image or use a hosted service. Ensure you have Docker installed using installation instructions [here](https://www.docker.com/get-started/).

To run a local Temporal server using Docker, you can execute the following command:

```bash
docker run --rm -p 7233:7233 --name temporal-server --network host temporalio/temporal:latest
```

With this setup, you have created a simple "Hello, World!" Temporal workflow using TypeScript. You can expand on this by adding more complex workflow logic and interacting with external services or resources as needed.


## Additional Resources
- Read more about how temporal works behind the scenes [here](https://temporal.io/how-temporal-works).
- Additional documentaion can be found [here](https://docs.temporal.io/concepts/).
- Check out the developers guide for your prefered programming language, including [Go](https://docs.temporal.io/dev-guide/go), [Java](https://docs.temporal.io/dev-guide/java), [PHP](https://docs.temporal.io/dev-guide/php), [Python](https://docs.temporal.io/dev-guide/python) and [Typescript](https://docs.temporal.io/dev-guide/typescript) here.
- [This is a great video](https://www.youtube.com/watch?v=LliBP7YMGyA) on how a company like Netflix uses temporal to build thier systems.
