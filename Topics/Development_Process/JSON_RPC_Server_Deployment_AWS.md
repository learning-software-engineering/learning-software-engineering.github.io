# JSON RPC Server Deployment on Amazon Web Services

## Introduction

After implementing some functions, you may wonder how others in the public domain can call your functions remotely and receive outputs on their end. This is usually accomplished by building an API server such as a JSON-RPC server and running it on cloud hosting services like Amazon Web Services (AWS), Microsoft Azure, and Google Cloud Platform. This documentation will walk you through how to prepare for the deployment of a JSON-RPC server, and how to run it on AWS.

## Prerequisites

### 1. Access to AWS

- Register an account at https://aws.amazon.com/. You will also be asked to add a payment method. However, unless your API server is used for commercial purposes such that it requires extra storage or it will receive a lot of requests, your usage will not lead to charges. 

### 2. Server code 

- In addition to your API functions, you will also need to write some JSON-RPC server code that allows your program to receive requests and respond with API functions output. This typically includes:
  - Handling incoming JSON-RPC requests: The server code must be able to parse incoming JSON-RPC requests and determine which method is being requested.
  - Implementing the JSON-RPC methods: The server code must implement the methods defined in the JSON-RPC API. This typically involves calling a specific function or method based on the requested JSON-RPC method.
  - Generating JSON-RPC responses: Once the requested method has been executed, the server code must generate a JSON-RPC response and send it back to the client.
  - Error handling: The server code must handle any errors that occur during the processing of JSON-RPC requests and return appropriate error responses to the client.
  - Configuration and setup: The server code may also include configuration and setup logic, such as setting up the server to listen on a specific port or initializing any required libraries or data structures.
  
  The specifics of the JSON-RPC server code will depend on the requirements of your application and the tools and programming language you are using to create the server. 
  
## Procedures

### Step 1: Setting up the virtual machine on AWS

- After acquiring an account on AWS, we will need to create and launch an EC2 instance, which is a web service that provides resizable compute capacity in the cloud (a virtual machine). It is essentially a server, and you can upload your code for the JSON-RPC server code onto EC2 and run it using AWS console or SSH on your terminal. To initialize and launch the EC2 instance, please follow this guide as it provides step-by-step procedures and explanations of different options during the setup. https://www.analyticsvidhya.com/blog/2023/01/launching-your-first-linux-ec2-instance/

### Step 2: Connecting to the virtual machine

- After successfully launching the EC2 instance, we need to connect to it to upload our code and run it. There are multiple ways, and here are the two easiest ways to do it:
  - Connect to it using AWS Management Console, the same website where you launched your EC2 instance.
    - On the Console home page, select EC2 > Instances
    - Click on your EC2 instance that was just launched. On the top right corner, click the “Connect” button. It should launch a console on the webpage, and you can use it like a Linux terminal
  - Connect to it using SSH
    - Open the terminal or command prompt on your local machine.
    - Use the ```cd command``` to navigate to the directory where you have stored the private key file for your instance.
    - Use the ```chmod``` command to change the permissions of the private key file. The command syntax is ```chmod 400 [private-key-file]```. For example, if your private key file is named my-key-pair.pem, the command would be ```chmod 400 my-key-pair.pem```.
    - Use the ```ssh``` command to connect to the instance. The syntax for the ```ssh command is ssh -i [path-to-private-key-file] [user]@[public-ip-address]```. Replace ```[path-to-private-key-file]``` with the path to your private key file, ```[user]``` with the user name for your instance (such as ec2-user for Amazon Linux instances), and ```[public-ip-address]``` with the public IP address of your instance. For example, the command might look like this: 
    
      ```ssh -i ~/.ssh/my-key-pair.pem ec2-user@54.12.34.56```

    Note that the exact steps for connecting to an EC2 instance using SSH may vary depending on your specific configuration and the type of instance you're using. Additionally, if you're using Windows, you may need to use a tool like PuTTY to connect to the instance instead of the ssh command.

### Step 3: Uploading and running the server described in Prerequisites on the virtual machine

- After connecting to the instance, you can upload your code using commands like ```scp```. Then, you can run your code just like how you run it on your local machine.
- Install the necessary dependencies on the EC2 instance. This includes any libraries and tools required to run your JSON-RPC server code. You can use a package manager like ```apt-get``` or ```yum``` to install these dependencies.
- Run your JSON-RPC server code on the EC2 instance. You can use a command like ```node server.js``` or ```python server.py``` to start the server.
- Test the JSON-RPC server to ensure that it is working properly. You can use a tool like ```curl``` to send requests to the server and check the responses.


### Step 4: How to keep the EC2 instance running after SSH is terminated using the “screen” command?

As long as the SSH terminal is open, the server will keep waiting for requests and will respond. However, once the SSH is terminated, the server will shut down along with it. We can use a scheduler on AWS to keep the instance running. In addition, we can also use the following simple method on SSH:

1. Connect to your EC2 instance.
2. Install "screen" by running the command (if ```apt-get``` doesn't work, try ```yum```): 
    ```
     sudo apt-get update
     sudo apt-get install screen
    ```
4. Start a new "screen" session by running the command:
    ```
     screen
    ```
6. Run your command or application as normal within the "screen" session.
7. Detach from the "screen" session by pressing the key combination "Ctrl-d". This will return you to your SSH session.
8. To reconnect to the "screen" session and continue working on your application, log back into your EC2 instance and run the command:
     ```
     screen -r
    ```
    This will reattach you to your "screen" session, allowing you to resume your work.

With this setup, your application will continue running even after your SSH session is terminated, as long as your EC2 instance is still running.

### Step 5: How to end a screen session?

If you want to shut down your server without stopping the EC2 instance, here's the procedure:

- Make sure you are in the "screen" session that you want to end. You can list your active "screen" sessions by running the command: ```screen -ls```
- Once you are in the "screen" session you want to end, you can terminate it by using the "exit" command. You can do this by:
  - Pressing the key combination "Ctrl-d". This will send an "end of file" (EOF) signal to the shell running in the "screen" session, which will exit the session.
- Or, if you have started other processes or sessions inside "screen", you can use ```exit``` command to exit all of them in sequence, and finally exit the "screen" session.

That's it! After you use the ```exit``` command, the "screen" session will terminate and you will be returned to your regular command prompt.

