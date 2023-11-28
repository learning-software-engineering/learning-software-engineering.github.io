# MongoDB in Docker

A quick-start tutorial for using MongoDB in a Docker container.

## Table of Contents
### [The Official Image](#using-the-official-image)
### [Alongside Your Application](#setup-alongside-application)
### [Additional Information](#additional-information-1)

## Using the Official Image

You can find [MongoDB's official images](https://hub.docker.com/u/mongodb) for both MongoDB community and enterprise on docker hub. 

Using the community edition for this example, pull the image by using this command: 

```console
docker pull mongodb/mongodb-community-server
```

Alternatively you can also find MongoDB's and other images through Docker Desktop's search bar. 

If you just want to get a database server up and running, the easiest way is to use Docker Desktop's GUI. Navigate to the 'Images' tab on the left hand tab, and find the 'mongodb-community-server' image that you just pulled. Under actions click the run button and it will open up a popup prompting you to input optional settings. The only absolutely necessary field to input to get up and running is the 'Ports' field. [Read about ports here.](./MongoDB_in_Docker.md#a-quick-summary-about-ports) 

In the port field, you can see that Docker Desktop already fills in the container port and control protocol for you (27017/tcp), so all we have to do is input the host port. We can use the same port (27017) as common.

If you have multiple MongoDB containers running at once, using 27016 or other numbers around is also possible. 

If you have other images running as well, docker will not allow multiple images to use the same port.

Now that you have gotten your first MongoDB container up and running, lets explore the other optional settings.

- Container name is self explanatory, this makes it easier to find and manage running containers
- Volumes allows for data to persist even when the container is removed/not running. 
    - This is often ideal when having to make changes to the image and recomposing, as you wouldn't want to lose your databases' data.
    - In MongoDB's case, the container path MUST be '/data/db'
        - This corresponds to which folder in the container you want to be externally mounted
    - The Host path can then be any folder you like. This is where the data will live in your local machine. 
        - If you want to use this data in an another MongoDB container, you can simply remount the host path to the same container path.
    - The environment variables for MongoDB are generally the root user and password.
        - MONGO_INITDB_ROOT_USERNAME, MONGO_INITDB_ROOT_PASSWORD are the variables
        - You can set the value of these to be whatever you want

In a final summary, what we have done so far is setup a MongoDB server in a docker container. Following the steps in the NoSQL page about MongoDB, using MongoDB compass, you can access your database through 'localhost:27017' and putting username and password that you have set using the environment variables.

In one command line, you can use:

```console
docker run --name containername -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=user -e MONGO_INITDB_ROOT_PASSWORD=pass mongodb/mongodb-community-server:latest
```

From what we discussed above, you can infer that -p is publish port, -e is an environment variable, and the final argument is the image. MongoDB recommends specifying the version instead of latest to ensure the version used is the same as expected. 

Congratulations! You have created your first MongoDB container!

### A quick summary about ports: 

The publish port argument generally looks like: XXXX:YYYY. 

The XXXX portion is the port that is used/exposed by the localhost. i.e. if the database was exposed on port 12345, to access the database you would use 'mongodb://localhost:12345/'

The YYYY portion is the port that is used/exposed within the docker container. This port cannot be accessed from localhost, unless published and mapped to an XXXX port. 

Sometimes the publish port argument also has /tcp or /http, these signify the protocol used by that port. 

There are reserved ports that cannot be used as well as unofficial ports that most people agreed to be reserved. For example, most commonly 8000 or 8080 is used for http servers. There is a lot of inormation that can be said about this, so for the sake of this tutorial it is common to use the same port exposed in the container for database images. For the complete list of reserved ports see: [IANA](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml)

## Setup Alongside Application

If you want to use MongoDB with another image, continuing on the example presented on the Docker page: 

```yml
version: "3.9"

services:
  app:
    image: YOUR_IMAGE_NAME_HERE:latest
    restart: always
    ports:
      - 80:80  # Expose any ports you need
    depends_on:
      - mongodb
    environment: 
      # The connection string containing the corresponding user and password as
      # provided in the mongodb environment variables
      - CONN_STR=mongodb://user:pass@mongodb

  mongodb:
    image: mongodb/mongodb-community-server:7.0.0-ubi8 # Use the version of your choosing
    restart: always
    ports:
      - 27017:27017 # This will expose the database outside the container, only do so if you need to access the database outside of just this application. 
    environment: 
      - MONGO_INITDB_ROOT_USERNAME=user # Username and password of your choosing
      - MONGO_INITDB_ROOT_PASSWORD=pass
    volumes:
      - type: bind
        source: ./data  # Use the folder of your choosing
        target: /data/db
      
```



## Additional Information

For more in depth information MongoDB provides a list of [Runtime Environments](https://www.mongodb.com/compatibility) compatible with MongoDB including more information about MongoDB in docker. [This tutorial](https://www.mongodb.com/compatibility/docker) from MongoDB is what this tutorial is based from. 

For more information about MongoDB itself you can check out the [NoSQL page](../Tech_Stacks/NoSQL_databases_JSON_interactions.md) in this wiki. 
