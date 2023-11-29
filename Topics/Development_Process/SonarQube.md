# Developing with SonarQube

## Table of Contents
#### [Introduction](#introduction-1)
#### [Advantages of SonarQube](#advantages-of-sonarqube-1)
#### [Limitations and Considerations](#limitations-and-considerations-1)
#### [Example Workflow](#example-workflow-1)
#### [Getting Started](#getting-started-1)
#### [Additional Resources](#additional-resources-1)

## Introduction

<img src="https://miro.medium.com/v2/resize:fit:666/1*rn-sO9oWLn9lYO7jkVO6og.png" width="300" height="100" align="right">

[SonarQube](https://www.sonarsource.com/products/sonarqube/) is an open-source platform designed to continuously inspect code quality while easily integrating into the existing development workflow. It provides comprehensive code analysis and reporting, aiding developers and teams in maintaining code health, identifying bugs, vulnerabilities, and enhancing overall software quality. The solution performs checks at every stage of the development process. 

## Advantages of SonarQube

- **Code Quality Analysis:** Offers in-depth insights into code quality metrics, ensuring better maintainability and readability.
- **Language Support:** Provides support for various programming languages such as Java, JavaScript, Python, C#, and more.
- **Security Vulnerability Detection:** Detects security vulnerabilities, potential bugs, and code smells early in the development cycle.
- **Customizable Rules and Thresholds:** Allows customization of rules and thresholds according to project-specific requirements.
- **Integration with CI/CD:** Seamlessly integrates with Continuous Integration/Continuous Deployment (CI/CD) pipelines for automated code analysis.
- **Historical Analysis:** Tracks code quality trends over time, enabling teams to monitor improvements or regressions.
- **Community and Plugin Ecosystem:** Offers a rich community and plugin ecosystem, expanding functionality and analysis capabilities.

## Limitations and Considerations

- **Resource Intensiveness:** Running extensive code analysis can be resource-intensive and time-consuming.
- **Initial Setup Complexity:** Setting up SonarQube and configuring rules might require initial investment in time and expertise.
- **Maintenance Overhead:** Regular maintenance, including updating versions and plugins, is necessary for optimal performance.
- **Learning Curve:** Understanding and interpreting the analysis reports might require familiarity with code quality metrics and best practices.
- **False Positives/Negatives:** Like any automated analysis tool, SonarQube might sometimes generate false positives or miss certain issues.

## Example Workflow

[SonarLint](https://www.sonarsource.com/products/sonarlint/), alongside SonarQube, exemplifies this process. It initiates within your IDE, detecting issues as you code. Serving as an advanced linter, SonarLint acts as your primary safeguard. Once coding is complete and you open a PR, it triggers your CI workflow, prompting an automatic analysis of your PR in SonarQube.

<img src="https://assets-eu-01.kc-usercontent.com/ab5c5eb8-73f9-0195-1d55-9cb00242be02/4843cee9-af50-4284-8981-a8cdb4836c65/body-2548db75-1761-4a3b-bab7-5acd02bd5658_Diagram%2Bof%2BPR%2BDeco%2Bin%2Bthe%2BALM.png?w=1078&h=493&auto=format&fit=crop" width="75%" height="75%">

Using the Quality Gate profile you’ve already established for your acceptance criteria, SonarQube ‘grades’ your PR and returns either Pass or Fail. If your Quality Gate is green, you can confidently merge your code. If it’s red, you have some work to do! Below, you'll see a failed Quality Gate in a GitHub PR.

<div style="text-align:center">
  <img src="https://assets-eu-01.kc-usercontent.com/ab5c5eb8-73f9-0195-1d55-9cb00242be02/c1b11005-3155-4826-9ed0-2fccba11afde/body-36e5e290-7294-466e-8016-615ba287c123_GH%2BPR%2B-%2BFailed%2BQG.png?w=360&h=403&auto=format&fit=crop" alt="Centered Image">
</div>

We attain the following objectives:

###### 1. Continuous Code Quality Assurance

Integrate SonarQube into your CI/CD pipeline to continuously analyze code quality with every code commit. This ensures that issues are identified and addressed early in the development process.

###### 2. Security Vulnerability Detection

Leverage SonarQube to identify potential security risks like SQL injection, cross-site scripting (XSS), and other prevalent vulnerabilities within your codebase.

## Getting Started

To begin working with SonarQube:

#### 1. Install SonarLint
- Get SonarLint for free by downloading it for your preferred IDE [here](https://www.sonarsource.com/products/sonarlint/ide-login/).

#### 2. Installing a local instance of SonarQube
You can evaluate SonarQube using a traditional installation with the zip file or you can spin up a Docker container using one of our Docker images. Select the method you prefer below to expand the installation instructions:

- From the zip file
  1. Download and install [Java 17](https://adoptium.net/en-GB/temurin/releases/?version=17) on your system.
  2. [Download](https://www.sonarsource.com/products/sonarqube/downloads/) the SonarQube Community Edition zip file.
  3. As a **non-root user**, unzip it in, for example, `C:\sonarqube or /opt/sonarqube`.
  4. As a non-root user, start the SonarQube server: 
      ```
      # On Windows, execute:
      C:\sonarqube\bin\windows-x86-64\StartSonar.bat
 
      # On other operating systems, as a non-root user execute:
      /opt/sonarqube/bin/<OS>/sonar.sh console
      ```

- From the Docker image
  1. Find the Community Edition Docker image on [Docker hub](https://hub.docker.com/_/sonarqube/).
  2. Start the server by running:
      `$ docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9000:9000 sonarqube:latest`

  
Once your instance is up and running, Log in to http://localhost:9000 using System Administrator credentials:
- login: `admin`
- password: `admin`
  
#### 3. Analyzing a project

Now that you're logged in to your local SonarQube instance, let's analyze a project:

1. Choose **Create new project**.
2. Assign a **Project key** and a **Display name** for your project, then click **Set up**.
3. Navigate to **Provide a token**, click **Generate a token**, name your token, click **Generate**, and proceed by clicking **Continue**.
4. Pick the primary language for your project under **Run analysis on your project**, and follow the guidelines to analyze your project.
5. In this step, you will download and execute a scanner for your code (if you're using Maven or Gradle, the scanner is downloaded automatically).


After successfully analyzing your code, you'll see your first analysis on SonarQube:
<img src="https://assets-eu-01.kc-usercontent.com/b98b0e99-a92d-0140-c108-93833c7e1e31/3295cf34-f8d6-401c-b26e-5ba90cf2267f/analyze-projects.png?w=1733&h=838&auto=format&fit=crop" width="75%" height="75%">


#### 4. Review Analysis Reports

- Access the SonarQube dashboard to review analysis reports, identify issues, and track code quality metrics.
- Address identified issues and refactor code as necessary.

Ultimately, it's a significant gain for you: enhancing your skills as a developer, tackling issues, and ensuring you don't burden your team with future challenges. 'Clean as You Code' serves as a pathway to a greater goal — striving to become the finest developer possible!
 

## Additional Resources

Explore these resources to deepen your understanding and proficiency with SonarQube:

- [Official SonarQube Documentation](https://docs.sonarqube.org/latest/)
- [Community Plugins and Extensions](https://docs.sonarqube.org/latest/extend/adding-plugins/)
- [SonarQube Rule Set](https://rules.sonarsource.com/)
- [SonarQube Video Tutorial for Beginners](https://www.youtube.com/watch?v=y8zJOjsT4E8)
- [SonarQube User Groups and Forums](https://community.sonarsource.com/)
  
