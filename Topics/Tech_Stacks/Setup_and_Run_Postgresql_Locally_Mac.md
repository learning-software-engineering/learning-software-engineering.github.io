# Postgresql local setup instructions for Mac Users

## Description
This document provides instructions on how to setup postgresql locally on your mac using two methods, the first being through pgAdmin4 and the second being through the terminal. Below please find an overview of what is covered in this document:
1. Downloading Postgresql and PgAdmin
2. Creation of a user in Postgresql
3. Creation of a database with owner of "user" in Postgresql 
4. Instructions on how to see tables / views in your database
5. Instructions on how to create tables / views in your database
6. Instructions on how to delete tables / views in your database

## Downloading Postgresql and PgAdmin
To be able to setup Postgresql locally we first need to download it. First we check to see if we already have Postgresql installed by running: ```psql --version``` in the command line. This would return the version of Postgres if you have it installed already, if you already have Postgresql installed and don't want to use PgAdmin then please move onto the next section. If not continue reading.

To Install Postgresql we will be using an interactive installer that can be found on [Postgres's website](https://www.postgresql.org/download/macosx/). Click the "Download the installer" link under the **Interactive installer by EDB** section. (**NOTE: The installer is by EDB, and will redirect you to another site**)

After arriving to the site you can click the download icon for Mac OS X for your desired version of Postgresql. This will install the interactive installer on your computer, which includes postgres and pgAdmin4. Image below:

<img src="https://github.com/michael-j-rubenstein/learning-software-engineering.github.io/blob/main/Topics/Tech_Stacks/Images/postgres_step1_1.png" width=500 />

Now you should have a ```.dmg``` file in the download folder, open it and follow the steps in their installer. **NOTE:** Make sure you select PostgreSQL Server and select pgAdmin and/or Command Line Tools in the "select Components" page based on your preference. I suggest to select all of the options as they are all pretty useful.

<img src="https://github.com/michael-j-rubenstein/learning-software-engineering.github.io/blob/2c530d7293dbf5234d45df54a4ac4c18d7e0a961/Topics/Tech_Stacks/Images/postgres_interactive_installer.png" width = 300 />

The port number of the server can be anything, but default is 5432.


## Creating a user in Postgresql
Now that you have Postgresql successfully installed, here are steps to create a new user:

### Using PgAdmin4
1. Launch up PgAdmin4
2. Insert the password you used in the installer in the previous section.
3. On the left side of the screen, go to ```Servers > Your wanted server (Default is PostgreSQL 15) > Login/Group Roles```
4. Right click and select the ```Create > Login/Group Role``` option
5. You can insert the information you want for the User, click the Save option and you're done!

Note that you area also able to set a password for the user and even superuser priviledges.

<img src="https://github.com/michael-j-rubenstein/learning-software-engineering.github.io/blob/main/Topics/Tech_Stacks/Images/postgres_pgadmin_user_setup.png" width=500 style="margin: 0 auto"/>
