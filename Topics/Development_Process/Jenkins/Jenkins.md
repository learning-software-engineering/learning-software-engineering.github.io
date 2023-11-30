# Introduction to Jenkins
## What is Jenkins?
Jenkins is an open source tool used for automated CI/CD. With it, you are able to trigger builds and automated testing with any change to your code repository.

<br>

## Terminology
**Jenkins Master**
<br>
This is the main Jenkins server. It is responsible for scheduling and delegating builds to Jenkins agents (or slaves). This allows for the distribution of tasks and speeds up and improves performance. It also supervises the health of the agents and will stop delegating tasks to an agent if it is too busy.
<br>
<br>

**Jenkins Slave**
<br>
A Jenkins slave is an excutable that runs on a machine used to execute builds. 
<br>
<br>

**Jenkins Pipeline**
<br>
A pipeline is a series of steps that the user defines and which Jenkins will run when the pipeline is triggered. There are multiple ways to create a pipeline including through a Jenkinsfile in your repository, through the Jenkins UI or through Blue Ocean. 
<br>
<br>

**Jenkins Architecture**
- Jenkins checks if repository has been changed. If there has been a change, then a build is triggered.
- Some builds require different environments than others which may not be possible on some machines. Thus, Jenkins delegates the job of building to different slaves and asks them to generate logs. 

<br>
<br>

# Setting up Jenkins with Github
## Setting up Jenkins Server
To begin working, we need a Jenkins server that is up and running with the Github plugin. If you already have this feel free to skip to the next step. 

Follow instructions on the Jenkins documentation for installation information specific to your machine:
https://www.jenkins.io/doc/book/installing/
- For MacOS: you will have to install Homebrew if you don’t have it already: 
    - https://docs.brew.sh/Installation
    - If you have an apple silicon machine, you may need to add homebrew to your PATH. This stack overflow answer has a fantastic step by step:
    - https://stackoverflow.com/questions/66666134/how-to-install-homebrew-on-m1-mac

<br>
Once you have installed Jenkins and have unlocked your server, you should enter the customize Jenkins page:

<img src="Assets/plugins.png" alt="plugin-options" width="60%"/>

<br>

Select **Install suggested plugins**. This will install the github plugins necessary to connect Jenkins to your repository. Jenkins will now prompt you to create an admin user. Ensure to save this login information in a secure location.

<br>

## Creating a Jenkins Job
1. Click on **new Item**. 
2. Enter a name and select **Pipeline**.
3. In the Build Triggers section, select **Github hook trigger for GITScm polling**. This will ensure that this job will be triggered after any change to your Github repository.

    <img src="Assets/github-hook.png" alt="github-hook" width="50%"/>

4. In the **Pipeline** section, select **Pipeline script from SCM**. For the **SCM**, select **Git**. Then add your repository URL. In the **script path**, add the path to your Jenkinsfile in your repository. 
    - If you are unfamiliar with what a Jenkinsfile is check out the documentation for some more information: https://www.jenkins.io/doc/book/pipeline/jenkinsfile/. If you want to get started right away, create a file in your repo called Jenkinsfile and copy the script from the section <em>Creating a Jenkinsfile, Jenkinsfile (Declarative Pipeline)</em> in the documentation.
    - **Note**: the default value for the option for the branch to build is <em>master</em>, but the default Github branch is called <em>main</em> now. Make sure to select the correct branch. 
    <img src="Assets/jenkins-pipeline-settings1.png" alt="pipeline-settings" width="70%"/>
    <img src="Assets/jenkins-pipeline-settings2.png" alt="pipeline-settings" width="70%"/>


5. If your Jenkins server is:

    - **hosted remotely:**
        You can add a webHook to Github. In your Github repository navigate to **Settings** then **Webhooks**. Click **Add webhook**. You will need your Jenkins endpoints (must be publicly available over the internet) to enter into the Payload URL section.

    - **hosted locally:**
        Select the **Poll SCM** option instead. Adding H \* \* \* \* \* will poll your github repository every hour for changes in your github or alternatively when you input \* \* \* \* \* github will be polled every minute (which is not a good idea in reality since polling is expensive, but can be good for testing).

        <img src="Assets/poll-SCM.png" alt="poll-SCM" width="70%"/>


Hooray, now any changes you make to your repository will trigger your job to run!

<br>

## Sources:
- Trapani, K. (2023, March 3). How to Integrate Jenkins with GitHub. Cprime. https://www.cprime.com/resources/blog/how-to-integrate-jenkins-github/
- ProgrammingKnowledge. (2021, March 7). Jenkins Tutorial is For Beginners, DevOps and Software Developers [Video]. YouTube. https://www.youtube.com/watch?v=EYA2YNHHPls
- Team, C. O. (2023, August 30). Jenkins. Codefresh. https://codefresh.io/learn/jenkins/
- Arvind. (2020, November 25). Jenkins Master and Slave Architecture – a complete guide. Edureka. https://www.edureka.co/blog/jenkins-master-and-slave-architecture-a-complete-guide/