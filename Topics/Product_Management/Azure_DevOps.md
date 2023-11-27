## Introduction to Azure DevOps
Azure DevOps is a product management tool provided by Microsoft that helps teams manage projects by providing a set of services to support the entire software development life cycle of a product from planning to deployment. For CSC301 teams, two very useful tools are Azure Boards and Azure Test Plans.
### Azure Boards for task management
For task management, Azure DevOps provides Azure Board for teams to create work items and assign them to team members. The status of these work items can then be updated during the development phase. 
A really useful feature of Azure Board is that it allows teams to create work items of different work types and group related work items into a hierarchical structure. Teams can define and customize their own work item types and create a work item hierarchy. A common work item hierarchy for agile process is:  
>├── feature 
>>├── user story 
>>>├── task
>>>>├── test case
>>>>├── bug

Using this set of work item types, we can then group related work items by linking a parent work item to children work items. For example, a feature item can be divided into and linked to user stories items.
Teams can then choose to view all work items in a hierarchical view instead of just a list of work items which really helps with tracking tasks for large projects. 

### Azure Test Plans for testing
For testing, Azure DevOps provides Azure Test Plans for teams to create their own plans for testing. A common practice (for agile development) is to create a test plan for each sprint. In the test plan, the team can add a test suite for each user story that they will work on in the sprint. Within each test suite, the team can then create a test case for each task that is related to the user story. At the end of each sprint, teams can run the test plan and check off all the tasks that pass their associated test case and create and report bugs for the tasks that failed.

### Azure Pipelines for automated building
Besides Azure Boards and Test Plans, Azure Pipelines may also be useful to CSC301 teams for deployment and github integration. Teams can create a new pipeline for their project and link their github repo to the pipeline, then depending on the application the team is building, Azure Pipelines will generate a template yml file which the team can then modify by selecting the commands they want to automatically run(build, test, etc) and add this file to their repo. With that the team now have a pipeline that can automatically build and test their project. Azure Pipelines also provides automated deployment for web apps to Azure App Services if the team uses Azure App Services for deployment.

### Resources
More about Azure Boards: https://learn.microsoft.com/en-us/azure/devops/boards/get-started/what-is-azure-boards?view=azure-devops 

More about Azure Test Plans: https://learn.microsoft.com/en-us/azure/devops/test/overview?view=azure-devops 

More about Azure Pipelines: https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/what-is-azure-pipelines?view=azure-devops

Read more about Azure DevOps services: https://learn.microsoft.com/en-us/azure/devops/user-guide/services?view=azure-devops 