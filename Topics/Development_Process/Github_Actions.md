# Automating Python Testing and Deployment with GitHub Actions and SSH
GitHub Actions is a powerful workflow automation tool that allows you to automate your software development workflows directly in your GitHub repository. In this guide, we'll walk through the process of setting up automated testing and deployment for a Python project using GitHub Actions and SSH.


# Table of Contents
- [Table of Contents](#table-of-contents)
- [Prerequisites](#prerequisites)
- [Setting up the remote server](#setting-up-the-remote-server)
    - [Installing Dependencies](#installing-dependencies)
    - [Cloning the project](#cloning-the-project)
    - [Creating a virtual environment](#creating-a-virtual-environment)
    - [Deployment Script](#deployment-script)
        - [What is tmux and why do we need it?](#what-is-tmux-and-why-do-we-need-it)
- [Setting up the GitHub repository](#setting-up-the-github-repository)
    - [Secrets](#secrets)
    - [Workflow](#workflow)
- [Testing the workflow](#testing-the-workflow)
- [Further Reading](#further-reading)
- [Conclusion](#conclusion)


## Prerequisites
Before you start, ensure you have the following:
- A python project hosted on GitHub.
    - Make sure your project has a requirements.txt file containing all of the project's dependencies.
    - This guide assumes that your tests have been written using the pytest framework.
- A remote server with SSH access. This can be a VPS, a dedicated server, or even a Raspberry Pi.
    - Keep the hostname, port, username, and private key for the remote server handy. You'll need them later.

## Setting up the remote server
First, we'll need to set up the remote server. We'll be using a VPS running Ubuntu for this guide, but the steps should be similar for other Linux distributions.

### Installing Dependencies
First, we'll need to install the dependencies for our project. We'll be using Python 3.10 for this guide, but you can use any version of Python that your project supports.

```bash
sudo apt update  # Update the package index
sudo apt install python3 python3-venv python3-pip tmux  # Install Python 3, venv, pip, and tmux
```

### Cloning the project
Now, we'll clone the project from GitHub. Make sure you replace the `URL` with the URL of your project and `PROJECT_NAME` with the name of your project.

```bash
git clone [URL]  # Clone the project from GitHub
cd [PROJECT_NAME]  # Change into the project directory
```

### Creating a virtual environment
Next, we'll create a virtual environment for our project. This will allow us to install our project's dependencies without affecting the rest of the system.

```bash
python3 -m venv venv  # Create a virtual environment named "venv"
source venv/bin/activate  # Activate the virtual environment
```

### Deployment Script
Next, we'll create a deployment script. This script will be run by GitHub Actions to deploy the project to the remote server. Make sure you replace `PROJECT_NAME` with the name of your project.

```bash
cd ..  # Change into the parent directory (leaving the project directory)
touch deploy.sh  # Create the deployment script
chmod +x deploy.sh  # Make the deployment script executable
```

Then, open the deployment script in your favorite text editor and add the following code:

```bash
#!/bin/bash

cd [PROJECT_NAME]  # Change into the project directory
source venv/bin/activate  # Activate the virtual environment

git pull  # Pull the latest changes from GitHub

pip install -r requirements.txt  # Install the project's dependencies
python -m pytest  # Run the project's tests

tmux kill-session -t [PROJECT_NAME]  # Kill the existing tmux session
tmux new-session -d -s [PROJECT_NAME]  # Create a new tmux session
tmux send-keys -t [PROJECT_NAME] "python3 main.py" ENTER  # Start the project
```

The deployment script will do the following:
1) Change into the project directory
2) Activate the virtual environment
3) Pull the latest changes from GitHub
4) Install the project's dependencies
5) Run the project's tests
6) Kill the existing tmux session
7) Create a new tmux session
8) Start the project

#### What is tmux and why do we need it?
tmux is a terminal multiplexer that allows you to run multiple terminal sessions in a single window. We'll be using tmux to run the project in the background so that we can close the SSH connection without stopping the project.

## Setting up the GitHub repository
Now that we've set up the remote server, we'll need to set up the GitHub repository. We'll be using the GitHub web interface for this guide, but you can also use the GitHub CLI if you prefer.

### Secrets
First, we'll need to add our SSH credentials to the repository as secrets. This will allow us to access the remote server without exposing our credentials in the workflow file. To do this, go to the repository settings and click on "Secrets" in the sidebar. Then, click on "New repository secret" and add the following secrets:
- `SSH_HOSTNAME`: The hostname of the remote server.
- `SSH_PORT`: The SSH port for the remote server. (Default: 22)
- `SSH_USERNAME`: The username for the remote server.
- `SSH_PRIVATE_KEY`: The private key for the remote server.

### Workflow
Next, we'll need to create a workflow file. This is a [YAML file](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html) that tells GitHub Actions what to do when certain events occur. To do this, create a new file named `.github/workflows/main.yml` and add the following code:

```yaml
name: Test and Deploy

on:
  push:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - name: Set up Python 3.10
      uses: actions/setup-python@v3
      with:
        python-version: "3.10"
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        python -m pip install pytest
        python -m pip install -r requirements.txt
    - name: Test with pytest
      run: |
        python -m pytest
    - name: Deploy
      uses: appleboy/ssh-action@v1.0.0
      with:
        host: ${{ secrets.SSH_HOSTNAME }}
        username: ${{ secrets.SSH_USERNAME }}
        key: ${{ secrets.SSH_PRIVATE_KEY }}
        port: ${{ secrets.SSH_PORT }}
        script: sh deploy.sh
```

This workflow will run the following steps when we push to the main branch:
1) Install Python 3.10 in a temporary environment
2) Install the project's dependencies from `requirements.txt`
3) Run the project's tests using pytest
4) Run the `deploy.sh` script on the remote server using SSH if the tests pass.

## Testing the workflow
Now that we've set up the workflow, we'll need to test it to make sure it works. To do this, push a commit to the main branch and check the Actions tab in the repository. If everything worked correctly, you should see a green checkmark next to the commit message like in [this image](https://i.imgur.com/PYAgSb9.png). If not, check the logs for the workflow to see what went wrong by clicking the commit message and then build.

## Further Reading
If you'd like to learn more about GitHub Actions, check out the [official documentation](https://docs.github.com/en/actions).

## Conclusion
In this guide, we walked through the process of setting up automated testing and deployment for a Python project using GitHub Actions and SSH. We also tested the workflow to make sure it works correctly.