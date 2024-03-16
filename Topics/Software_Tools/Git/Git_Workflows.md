# Git Workflows

## External Resources for Git Workflows
* [5 Different Git Workflows](https://medium.com/javarevisited/5-different-git-workflows-50f75d8783a7)
* [5 Git Workflows to Improve Development](https://rovitpm.com/5-git-workflows-to-improve-development/)
* [Comparing Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)

## What are Git Workflows?
Git workflows are different strategies that project development teams can utilize and emulate to collaborate on a project while leveraging [Git as their version control system](https://www.knowledgehut.com/tutorials/git-tutorial/introduction-to-git). It is extremely critical for any team to be able to build something together without disrupting the team’s codebase.

A successful Git workflow integrates the consideration of several factors such as the team culture, the project scalability, the team’s [release schedules](https://asana.com/resources/release-management), the team size, the easiness to fix mistakes and [merge conflicts](https://www.simplilearn.com/tutorials/git-tutorial/merge-conflicts-in-git), etc.

The following are the most common workflows that have been used.

## Variations of Git Workflows:

### 1. Centralized (Basic) Workflow
As the name suggests, there is one repository with only one central branch, or the “master” branch. Hence, this workflow blends the staging and production environment into just 1 branch. Each developer clones this central repository to their local machine and makes changes locally. When they are ready to push their changes, they commit them to their local branch and then push them to the “master” branch directly. Other developers can then pull these changes from “master” to their own local machines.

[Example of a Centralized Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows#centralized-workflow)

**Pros**: Simple, straightforward

**Cons**: High likelihood of merge conflicts when multiple programmers are working on the same files simultaneously, difficult to scale up, difficult to add complexity, difficult to maintain code cleanliness

**When to Use**: Small teams, simple projects with minimal collaboration required.

### 2. Feature Branch Workflow
With this workflow, developers create separate branches from the “master” branch for separate new features. This “master” branch still serves as the staging and production environment. As developers work on the features, they can make changes and commit to these separate feature branches individually. Once a feature is complete, the developers can create a pull request to merge with the “master” branch again. These pull requests will be reviewed by other developers who can provide feedback and make suggestions before the changes are approved and merged.

[Example of a Feature Branch Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)

**Pros**: Easier collaboration, reduces risk or merge conflicts, still relatively simple, “master” branch should not contain broken code

**Cons**: Requires discipline to manage and review feature branches correctly, not recommended if various versions of production or release plans are demanded, production code (the code in the “master” branch) can turn unstable 

**When to Use**: Ideal for multiple developers to work on numerous features without disturbing the main codebase.

### 3. Gitflow Workflow (Most Common)
This workflow is the combination of the feature branch workflow with an additional “develop” branch as well as smaller release branches and hot-fix branches. With the “develop” branch, that is created from the “master” branch, it represents the staging environment, while the “master” branch serves as the stable production environment. 

Here, developers will create specific branches from the “develop” branch. These specific branches include the feature branches that we discussed previously. Once the “develop” branch has acquired enough features for a release, release branches are forked off the “develop” branch to finalize documentation, bug fixes, and other tasks related to this release only. No new features are made in these release branches. Once ready, these release branches will be merged into both the “master” branch and the “develop” branch with version numbers tagged.

There also exist hot-fix branches, which are the only branches forked off the “master” branch. These branches are utilized to quickly patch production releases without disrupting other branches’ workflow. Once done, these branches are also merged into both the “master” branch and the “develop” branch with updated version numbers tagged too.

[Example of a Gitflow Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)

**Pros**: Reduces risk of introducing bugs to the stable main codebase, allows for release plans as well as multiple versions in production, flexibility in managing releases (teams can polish current release and work on new features for the next release simultaneously) and hotfixes, structured

**Cons**: More complex, requires discipline to follow the rules and structure of the workflow, releases cannot be done quickly, multiple iterations of checking and testing can slow the building process down

**When to Use**: Ideal for larger teams or more complex projects where a structured approach to development is needed.

### 4. Forking Workflow
Used usually for public open-source projects, this workflow doesn’t have a central server-side repository. Developers will have to fork off the original and official server-side repository, giving themselves their own server-side repository. They will then clone the repository into their local machines to work on the projects. Features and changes are then committed to their own server-side repository. Developers can then make pull requests to the official repository for the manager of the official repository to review, suggest, and approve. 

[Example of a Forking Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/forking-workflow)

**Pros**: Easy for multiple developers to contribute to the same project, reduces the risk of introducing bugs into the official repository

**Cons**: High fragmentation since there are no collaboration between developers, possible duplicate efforts, likelihood of excessive contributions for the original owner(s) of the official repository to maintain and keep track

**When to Use**: Ideal for open source projects where there are many contributors who may not be part of the same organization or team, and where there is a need for strict access controls or a clear separation between the main repository and individual developers' repositories.


### 5. Linear Git Flow
A linear git flow, as the name suggests, maintains commits and changes to the repository in a linear fashion. It supports easy rollbacks in a chronological manner. This makes it easier to understand the development history of the project and how it has evolved over time. A linear git flow is useful and most applicable for projects with a simple development process which includes solo projects or small-membered projects. It is most beneficial when the primary focus of the project is stability and clarity in changes. It also faciliates development where frequent code reviews are required. A linear git flow is also beneficial to easily identify changes that have caused bugs as it forces users to thoroughy review code and test each commit.

[More on Linear Git FLows and how to get started](https://www.bitsnbites.eu/a-tidy-linear-git-history/)

**Pros** Easy rollbacks and code reviews for small teams, identifying bugs in code becomes easy given the clean chronological organisation, produces high quality maintainability code

**Cons** Not suitable for teams with many members or those with independent developers. Rolling back to a commit can also mean completely erasing later commits, setting up a clean rebase work flow can be difficult

**When to Use**: Most ideal for teams with a highly streamlined development process or for projects prone to bugs over time
