# Deploying a Web Application on DigitalOcean

## Introduction
This tutorial will guide you step-by-step through the process of deploying a web application using DigitalOcean's hosting platform. DigitalOcean, a cloud service provider, provides a straightforward and user-friendly environment for hosting applications, making it an excellent choice for developers to use.

## Prerequisites
Before you begin, ensure you have the following:

1. **DigitalOcean Account**: Sign up for a DigitalOcean account if you don't have one already. (https://cloud.digitalocean.com/registrations/new)

2. **Web Application Code**: Have your web application code ready for production. This could be a Node.js, Python, Ruby on Rails, or any other type of application.

Now that you have these two prerequisites, you're ready to launch your web app into the world! Follow these steps:

### Step 1: Create a Droplet
In digital ocean, a "Droplet" refers to a virtual private server (VPS) that you can deploy and manage on DigitalOcean's cloud infrastructure. It's essentially a scalable compute platform with add-on storage, where you can run applications, websites, and other services.

1. Log in to your DigitalOcean account.
2. On the left panel, click on "Droplets" under "Manage" and press "Create Droplet".

Note that droplets do have a price per month to host on their platform, but DigitalOcean provides a free $200 budget for 60 days to newly created accounts.

2. Choose a data center region. If you'd like the fastest speeds between your device and the web app, choose the closest region to you.
3. Choose your operating system. Ubuntu is a popular choice for operating systems, as it is known to be fast.
4. Select a plan based on your application's requirements. The CPUs and sizes that the platform offers differ in price.
5. Optionally, you can also add an authentication method to your droplet to make it a private web app.
6. Click "Create Droplet."

<img src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/103388045/f45f232d-6eb4-4857-9e05-98e600d66791" height="500"/>

### Step 2: Access Your Droplet
Once the droplet is created, you will receive an email with login details.

Use an SSH client to connect to your droplet. For example, run `ssh root@your_droplet_ip` in the terminal.

### Step 3: Update System Packages
After logging in, update the system packages:

```bash
   sudo apt update
   sudo apt upgrade
```

This ensures that your droplet's operating system is up-to-date with the latest security patches and software updates.

### Step 4: Install Dependencies
Install any dependencies required for your web application, such as Node.js, Python, or database drivers.

For example, if you're using Node.js, you could run the following command in the terminal:

```bash
   sudo apt install nodejs npm
```

Adjust the command based on the requirements of your specific application.

### Step 5: Transfer your files
Transfer your application files to the droplet using SCP or any other method. To do this with SCP, follow these steps:

1. Open a new terminal and use the cd command to navigate to the directory containing your application code.

```bash
   cd /path/
```

2. Use the scp command to copy the files into the newly created droplet.

```bash
   scp -r your_application_directory user@droplet_ip:/remote/path
```

Replace the following:
  your_application_directory: The local path to your application code.
  user: The username used to log in to your droplet.
  droplet_ip: The IP address of your droplet. You can get this on the webpage of the droplet.
  /remote/path: The path on your droplet where you want to copy the files.

3. Enter your password. You'll be prompted to enter the password using the login details from the email previously.

### Step 6: Configure Environment Variables
Configure your application settings, such as environment variables and database connections. 

Some applications use configuration files to store settings. These files can be in various formats, such as JSON, YAML, or INI. For example, in a Node.js application, you might have a config.json file like this:

```json
   {
     "database": {
       "url": "your_database_connection_string"
     },
     "api_key": "your_api_key"
   }
```

If your application interacts with a database, you'll need to configure the connection details. This includes the database type (e.g., MySQL, PostgreSQL), host, port, username, password, and database name. Here's an example of a PostgreSQL connection string:

```bash
   postgres://username:password@localhost:5432/database_name
```

Depending on your application, there may be other settings you need to configure, such as the listening port for your web server, the location of static files, logging options, etc. Make sure to do this before running your application on the droplet.

### Step 7: Deploy your Application
Execute the command to start your application. The command will depend on the programming language and framework used by your application.

For example, if you have a Node.js application, the command might be:

```bash
   node app.js
```

### Step 8: Verify Your Application is Running
Once your application is started, you can verify that it's running by accessing it through a web browser or using tools like curl or wget to make HTTP requests.

```bash
   curl http://localhost:your_application_port
```

Running this command in your terminal will check to see if the application is up and running.

### Step 9: Extend!
Congratulations! You have successfully deployed your web application on DigitalOcean. With your web app deployed, there are several things you can do to enhance, optimize, and manage your application, such as:
- Set up monitoring tools to track the performance of your web application. DigitalOcean provides monitoring graphs and alerts that can help you identify performance issues.
- Scale your infrastructure. This might involve upgrading your droplet, adding more droplets, or implementing load balancing.
- Regularly back up your application data and configurations to prevent data loss. DigitalOcean provides snapshot and backup features for your droplets.
- Enhance the security of your web application by regularly updating software, implementing firewalls, and following security best practices. Monitor your application logs for any suspicious activities.

This tutorial covered the essential steps, but keep in mind that each application may have specific requirements. Refer to DigitalOcean's documentation for more advanced configurations and optimizations. (https://docs.digitalocean.com/)

Happy coding!
