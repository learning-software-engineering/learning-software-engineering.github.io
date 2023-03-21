# Using Vercel to host your Frontend (Automated)

## Table of Contents
### [1. Introduction](#1-introduction)
### [2. The Issues](#2-the-issues)
### [3. Step by step solution to issues](#3-step-by-step-solution-to-issues)

## 1. Introduction

If you are building a frontend website for anything, you will eventually come across a time when you look to host it. There are many options out there, but Vercel looks like the best option for a few reasons. The main 2 being simiplicity and automation.

## 2. The Issues
The first issue is that sometimes you will be working in a GitHub Organization repo such as a GitHub Classroom. Although GitHub Classroom provides a lot of additional resources, it pulls you down when trying to deploy with 3rd party sites. 3rd party sites see that your repo is a part of an Organization and will enforce you to upgrade to a paid plan to continue using Vercel. This is an issue because although you are part of an Organization, it's GitHub Classroom and you are a student in the course and do not want to pay for the pro membership. This guide helps work around this issue.

The second issue is that Vercel is designed to automatically deploy when the branch that is linked to it is updated. This is great, but it can be a problem when you are working on a project with a team. This guide teaches you how to solve this probem also along the way using GitHub Actions.

## 3. Step by step solution to issues
First let's get the prerequisites out of the way. You will need:

- a GitHub account
- a Vercel account
- a GitHub Classroom account through your school. 
- a GitHub Classroom repo that you have access to
- a frontend project in the GitHub Classroom repo that you can deploy

If you do not have these, please create them now. 

First, lets solve the issue of deploying to Vercel using a GitHub Organization repo. This is actually quite easy. Just create a fork from the GitHub Classroom repo to your personal GitHub account. Then in Vercel, create a new project and link it to the **forked repo**. This will allow you to deploy the project without having to pay for a pro membership. This is a great solution for students who are working on projects in GitHub Classroom.

Great! Now we have a deployed project on Vercel. But what happens when we update the main repo in GitHub Classroom? Well, Vercel will not automatically update the project. This is because the project is linked to the forked repo and not the main repo. This is a problem because we want to be able to update the project on Vercel when we update the main repo. A manual way to update the project is to go to forked repo and sync with the main repo. Once the new commits are synced, Vercel will automatically deploy the project.

But who wants to do that manually? There must be a better way. Turns out there is!

We can use GitHub Actions to periodically sync the forked repo with the main repo. This way, when we update the main repo, the forked repo will periodically update and Vercel will automatically deploy the project.

To do this, we will need some things:
- A GitHub Student Account. This gives you access to 3,000 GitHub Action minutes for free (which in my experience is more than enough). Visit [here](https://education.github.com/pack) to sign up.
- A GitHub Personal Access Token for the main repo. This is needed so GitHub Actions can access the main repo.
- A GitHub Personal Access Token for the forked repo. This is needed so GitHub Actions can access the forked repo.

### 3.1. Creating a GitHub Personal Access Token for a repo
Go to your account settings by clicking on your profile picture in the top right corner and clicking on `settings`. Then click on `Developer Settings`. Then click on `Personal Access Tokens`. Or you can just click [here](https://github.com/settings/tokens?type=beta) to go to the page. Then click on `Generate New Token`. Then give it a name and set **resource owner** to your GitHub Classroom Organization. Then for `repository access` select `Only Select Repositories` and select the main repo. Then give it the permissions. For testing purposes, give it all the permissions for now, then turn off the permissions you don't use later. Then click on Generate Token. Then copy the token and save it somewhere safe. You will need it later.

**Do this for both the main repo and the forked repo.**

### 3.2. Creating repository secrets
Now that we have the tokens, we need to add them to the forked repo. Go to the forked repo and click on `Settings`. Then click on `Secrets and Variables`. Then Click on `Actions`. Then click on `New Repository Secret`. Then give it a name and paste the token you created for the forked repo. Then click on Add Secret. Then do the same for the main repo. Make sure the names are distinct for each repo.

### 3.3. Creating a GitHub Action
Now that we have the tokens, we are ready to create a GitHub Action. Go to the forked repo and click on `Actions` tab. Then click on `New Workflow`. Then click on `Set up a workflow yourself`. Then paste the following code into the editor:

```yaml
name: Auto update and deploy from upstream

on:
  schedule:
    - cron:  '*/30 * * * *'
    # scheduled for every 30 mins
  workflow_dispatch:
    # manual trigger

jobs:
  sync_latest_from_upstream:
    runs-on: ubuntu-latest
    name: Sync latest commits from upstream repo

    steps:
    # REQUIRED step
    # Step 1: run a standard checkout action, provided by github
    - name: Checkout target repo
      uses: actions/checkout@v2
      with:
        # optional: set the branch to checkout,
        # sync action checks out your 'target_sync_branch' anyway
        ref:  main
        # REQUIRED if your upstream repo is private (see wiki)
        persist-credentials: false

    # REQUIRED step
    # Step 2: run the sync action
    - name: Sync upstream changes
      id: sync
      uses: aormsby/Fork-Sync-With-Upstream-action@v3.4
      with:
        target_sync_branch: main # this is the branch you want to sync to in forked repo
        # REQUIRED 'target_repo_token' exactly like this!
        target_repo_token: ${{ secrets.YOUR_FORKED_REPO_PAT }}
        upstream_sync_branch: main # this is the branch you want to sync FROM in upstream repo
        upstream_sync_repo: your-organiation/your-main-repo # this is the repo you want to sync FROM
        upstream_repo_access_token: ${{ secrets.YOUR_MAIN_REPO_PAT }}

        # Set test_mode true to run tests instead of the true action!!
        # test_mode: true
      
    # Step 3: Display a sample message based on the sync output var 'has_new_commits'
    - name: New commits found
      if: steps.sync.outputs.has_new_commits == 'true'
      run: echo "New commits were found to sync."
    
    - name: No new commits
      if: steps.sync.outputs.has_new_commits == 'false'
      run: echo "There were no new commits."
      
    - name: Show value of 'has_new_commits'
      run: echo ${{ steps.sync.outputs.has_new_commits }}
```

- Firstly change the cron job to run when you want it to. I have it set to run every 30 minutes. I feel that is reasonable enough, but you can bring it as down as 5 minutes according to GitHub. 

- Then change the `target_sync_branch` to the branch you want to sync to in the forked repo. 

- Then change the `upstream_sync_branch` to the branch you want to sync from in the main repo.

- Then change the `upstream_sync_repo` to the repo you want to sync from.

- Then change the `YOUR_FORKED_REPO_PAT` to the name of the secret you created for the forked repo. Then change the `YOUR_MAIN_REPO_PAT` to the name of the secret you created for the main repo. Then save the file.

- If you have experience working with GitHub Actions, you can change stuff in step 3 for customized messages. I have left it as is for now.

- Then save the file.

### 3.4. Testing the GitHub Action
Go to the `Actions` tab on your forked repo and click on the workflow you just created. Then click on `Run workflow`. Then click on `Run workflow`.

After the action runs, check to make sure its running corrcetly. If it is, then you are good to go! The action is triggered and will run every 30 minutes (or whatever time you've set it to).

### 3.5. Looking forward
This was nice, but the deployment only deploys after x minutes depending on the cron job. What if we want to deploy immediately after the main repo is updated? We can do this too. We can use a webhook to trigger the GitHub Action. This way, when the main repo is updated, the webhook will trigger the GitHub Action and the forked repo will be updated and deployed immediately. You can learn more about webhooks [here](https://docs.github.com/en/get-started/exploring-integrations/about-webhooks) and learn how to create them [here](https://docs.github.com/en/webhooks-and-events/webhooks/webhook-events-and-payloads).

Another note, deploying off of your main branch (as shown in sample code above) may be a bad idea. If you are working on a project with other people, you may want to deploy off of a different branch. Developers do this in the industry all the time. They have a deployment branch that is different from the main or development branch. After they have enough features to deploy, they merge their code into the deployment branch. Then, they deploy off of the deployment branch. This way, they can deploy whenever they want without worrying about breaking the main branch.
