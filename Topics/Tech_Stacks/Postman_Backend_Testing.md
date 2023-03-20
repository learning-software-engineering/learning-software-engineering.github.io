#Postman Backend Testing

In this  Postman application overview, We will go over how to 
install the application and the details of how to tests your API endpoints.

## Downlaad and instalation
the following link will take you to the postman website where you can
download the application if you do not have it already installed:
https://www.postman.com/downloads/
download the specific version for your compute.

After the donalod the following video will help you install the application:
https://www.youtube.com/watch?v=pBo_oClYjjM&ab_channel=GeekyScript
https://www.youtube.com/watch?v=sriayOzVaMM&ab_channel=Postman
https://www.youtube.com/watch?v=9ZZdl4CQbCg&ab_channel=OSTechHelp

## Testing with Postman
#Creating a workspace
Before starting testing your API, it is best to create a workspace for the 
specific project that you are working on. This way team members can access
and contribute to the test cases.
In order to do this, click on the the workspace tab and then click on the 
'Create Workspace' button and name your workspace.
then click on the newly created workspace to work within it.
###Creating a Collection
In order to send request within this workspace. You need to create a new
collection which will contain all the different requests to your API endpoint.
Create a new Collection by clicking on the '+' that is location next to the 
collection section. **********
###Sending requests
Once you have created the Collection, you can now create your request. 
Do this by expanding the newly created collection and clicking on add request
which is highlighted. Copy and paste the request URL of your API into the URL bar.

To add any new requests to your collection, right click on your collection and 
select a add request. Alternativly, you can right click on the previously created request
and click Duplicate. This also helps preserve the request variables.
#### POST requests
For POST requests, the request body is required, therefore to include all the data
you must fill the request body.
#### GET requests
For GET requests, the request needs to have header variables included. Click on the 
header tab within the request and add the keys and values. 
###Downloading collection
To export your work, you can right click on the Collection that you have been working on and 
click Export which will promt you to the version you would like to export. Once finished you can
download the exported file.

###Conclusion
This summary of Postman application showed the basics of creating a collection of requests to test
an API endpoint. After reading this, you should be able to create a workspace and collection of 
requests, sending POST and GET requests to your desired API endpoint. If there are additional 
information you would like to learn about, there are some useful articles and resources provided below.

### Articles and Resources

