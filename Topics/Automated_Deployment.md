# Resources for GitHub Actions Automated Deployment

<!-- &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; is being used to create tabs -->

 ### What is Automated Deployment? Why is it Important?
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; According to the Google Cloud Automation Center, Automated Deployment is "what enables you to deploy your software to testing and production environments with the push of a button." Automated deployment is a set of scripts that perform the following actions: prepare the target environment (installing/configuring any software needed), deploying the build packages created by continuous integration (this will be discussed more in the next part), run deployment tasks such as migrating databases, perform tests on the deployment to ensure it is functioning and accessable.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This prevents programming teams from having to manually perform these tasks for every deployment, which save teams hours over the course of a project. It reduces the risk of production deployments, since it ensures that all environments are the same. It also allows developers to deploy to production environments more frequently, which will lead to fast user feedback. In short, automated deployment is important, since it saves software teams time, prevents any errors in deployments, and allows teams to more easily ensure new features are working properly.
 
 
 
 ### How is Automated Deployment Used
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Automated Deplyment requires CI/CD to be used. CI stands for continuous integration, and CD stands for continuous delivery _or_ continuous deployment (note, there is a difference between these two). Continuous Integration ensures that the new code is ready to be deployed, and continuous delivery or deployment uses automated deployment to deploy to either staging/testing environments or a production environment, respectively.
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Continuous integration typically consists of developers continously merging their code into the main branch. Upon merging, code executes to create a build of the new code and run automated tests against this build. This is a followed by either continuous delivery or continuous deployment. Continuous delivery consists of automated deployment of the build packages from continuous ingration to a testing or staging environment. Deployment to production can be triggered whenever the team needs. Meanwhile, continuous deployment automatically deploys new code through testing and into production and requires zero human input. 
 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; There are many benefits to each step in this process. Continuous integration will lead to fewer bugs in production and easies release building as all issues with integration have already been found and solved. Furthermore, testing costs less since it is run on the CI server and less time is spent running the tests manually. However, CI requires writing automated testing for each new feature (Test Driven Development), as well as having a server where the automated tests are run. Furthermore, it requires developers to merge their work as often as possible, which may cause issues if some features or fixes take more time.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; The benefits of continuous delivery are that your team releases more often and deploying software is less complex since it is automated. Most importantly, it releases pressure on small changes, since they can always be quickly undone or fixed with future releases. However, it requires automated deployment, which takes time to set up, and the team needs to "embrace" flaging features so that incomplete features are not released. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The benefits of continuous deployment are faster development, less risky releases (since there are fewer changes per release), and constant improvements for customers. Issues with releases can be fixed more quickly, since development does not need to pause for releases. Releases are also not scheduled, so there is less pressure to finish everything by a certain deadline. However, just like delivery, feature flags **must** be a part of the coding culture, and application documentation must stay up to date with deployments. This is in order to ensure clarity on the included features in each release.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;However, most importantly, both continuous delivery and continuous deployment can only occur if the new changes pass all the tests from continuous integration. This means that in order to successfully implement continuous delivery or deployment, you need to have an extensive set of test for your code that can verify that the changes are suitable for these environments. Otherwise, continuous delivery or deployment can lead to issues within staging and testing environments, or, worse, issues for customers.
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;To summarize, automated deployment is used for continous deliver or deployment. In order for this to work, continuous integration needs to be used in order to extensively test the code and ensure it is acceptable to deploy to whichever environment (depending on if delivery or deployment is used). Although it requires a strong CI, it leads to faster development, less risky releases, and more customer feedback. 



 ### Examples of Common Automated Deployment Software
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Atlassian recommends using Bitbucket Pipelines, which is their "CI/CD tool that's integrated into Bitbucket Cloud," their version of GitHub. BitBucket provides extended CI/CD features that allow you to integrate with Jira, a task management software by Atlassian. However, you can implement CI/CD fairly easily with GitHub Actions.
 
 
 ### How to Set Up Automated Deployment with GitHub Actions
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; In order to set up automated deployment, you need to know the following: when do you want deployments to occur (on pull request, on push, on workflow dispatch, etc), where do you want the deployment to be (staging or production, continuous delivery vs continuous deployment), and what are the requirements for your environment (what packages do you need to set install or software do you need to set up to deploy).

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Once you know these things, you can start setting up your GitHub Action using a yaml file. Start with the `on:` command and put all the situations where you want deployment to occur (and on what branches). Then, under `jobs:`, create a `deployment:` section and set the environment, what os it runs on, and the steps necessary to deploy.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;For example, for Heroku, you need to specify the Heroku key (this is the login key) and the application you are deploying to. Meanwhile, for Expo, you may need to setup node, EAS (Expo Application Services), sign into EAS, install yarn dependencies, and then use EAS to deploy. An alternate method you could use is writing a shell script that performs these actions and simply having GitHub run this shell script with a GitHub Action.

To learn more specifics, please see the resources below.
 
 
 ## Resources:
 
 To learn more about DevOps in general, please see the Google Cloud Automation Center DevOps article referenced in the above writing: https://cloud.google.com/architecture/devops
 - To learn more about deployment automation specifically: https://cloud.google.com/architecture/devops/devops-tech-deployment-automation
 
 To learn more about CI/CD, please see the following article from Atlassian, an established software company from Australia: https://www.atlassian.com/continuous-delivery/principles/continuous-integration-vs-delivery-vs-deployment
 - To learn more about the difference between continous delivery and continuous deployment, see the following article: https://docs.github.com/en/actions/deployment/about-deployments/deploying-with-github-actions
 
 To learn more about how to set up automated deployment with GitHub actions, please see the following articles:
 
 - Deploying with GitHub Actions: 
   - https://docs.github.com/en/actions/deployment/about-deployments/deploying-with-github-actions
   - https://techblog.geekyants.com/github-actions-for-automating-builds-for-your-app
 
 - Deployment to Expo: 
   - https://github.com/marketplace/actions/expo-github-action
   - https://levelup.gitconnected.com/seamlessly-deploying-react-native-apps-with-expo-and-github-actions-3fd8157132bb

 - Deployment to Heroku:
  - https://github.com/marketplace/actions/deploy-to-heroku
  - https://devcenter.heroku.com/articles/git#for-an-existing-app
