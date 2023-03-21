# Postgresql local setup instructions for Mac Users

## Description
This document provides instructions on how to setup postgresql locally on your mac using two methods, the first being through pgAdmin4 and the second being through the terminal. Below please find an overview of what is covered in this document:
1. [Downloading Postgresql and PgAdmin](#one)
2. [Creation of a user in Postgresql](#two)
3. [Creation of a database with owner of "user" in Postgresql](#three)
4. [Instructions on how to see tables in your database](#four)
5. [Instructions on how to create tables in your database](#five)
6. [Instructions on how to delete tables in your database](#six)

<a name="one" />
## Downloading Postgresql and PgAdmin
To be able to setup Postgresql locally we first need to download it. First we check to see if we already have Postgresql installed by running: ```psql --version``` in the command line. This would return the version of Postgres if you have it installed already, if you already have Postgresql installed and don't want to use PgAdmin then please move onto the next section. If not continue reading.

To Install Postgresql we will be using an interactive installer that can be found on [Postgres's website](https://www.postgresql.org/download/macosx/). Click the "Download the installer" link under the **Interactive installer by EDB** section. (**NOTE: The installer is by EDB, and will redirect you to another site**)

After arriving to the site you can click the download icon for Mac OS X for your desired version of Postgresql. This will install the interactive installer on your computer, which includes postgres and pgAdmin4. Image below:

<img src="https://github.com/michael-j-rubenstein/learning-software-engineering.github.io/blob/main/Topics/Tech_Stacks/Images/postgres_step1_1.png" width=500 />

Now you should have a ```.dmg``` file in the download folder, open it and follow the steps in their installer. **NOTE:** Make sure you select PostgreSQL Server and select pgAdmin and/or Command Line Tools in the "select Components" page based on your preference. I suggest to select all of the options as they are all pretty useful.

<img src="https://github.com/michael-j-rubenstein/learning-software-engineering.github.io/blob/2c530d7293dbf5234d45df54a4ac4c18d7e0a961/Topics/Tech_Stacks/Images/postgres_interactive_installer.png" width = 300 />

The port number of the server can be anything, but default is 5432.

<a name="two" />
## Creating a user in Postgresql
Now that you have Postgresql successfully installed, here are steps to create a new user:

### Using PgAdmin4
1. Launch up PgAdmin4
2. Insert the password you used in the installer in the previous section.
3. In the tab on the left side of the screen, go to ```Servers > Your wanted server (Default is PostgreSQL 15) > Login/Group Roles```
4. Right click and select the ```Create > Login/Group Role``` option
5. You can insert the information you want for the User, click the Save option and you're done!

Note that you area also able to set a password for the user and even superuser priviledges.

<img src="https://github.com/michael-j-rubenstein/learning-software-engineering.github.io/blob/main/Topics/Tech_Stacks/Images/postgres_pgadmin_user_setup.png" width=500 />

### Using Postgresql Shell
1. Open up the Mac Terminal
2. Run ```sudo -u postgres psql``` to open up the Postgresql Shell using the default postgres user
3. Insert the password you used in the installer in the previous section
4. If successful you should see that the prompt for the terminal looks something like this: ```postgres=#```
5. Now to create a new user write ```CREATE USER your_users_name;```
6. A prompt will show to insert password for the user, after setting the password you're done!

Note that if you want to create a superuser you can use ```CREATE USER your_users_name SUPERUSER;``` instead in step 5.

More information and additional methods can be found here: [How to create a Postgres User](https://phoenixnap.com/kb/postgres-create-user)

<a name="three" />
## Creating a database in Postgresql
Now that you have a custom user, you can now create a database!

### Using PgAdmin4
1. Launch the app and insert your passwords
2. In the tab on the left side of the screen go to ```Servers > Your wanted server (Default is PostgreSQL 15) > Databases```
3. Right click and select the ```Create > Database...``` option
4. Insert the name of the database in ```Database``` field
5. If you want to change the Owner to your created owner, you can aswell in the ```Owner``` field

### Using Postgresql Shell
1. Open up the Mac Terminal
2. Run ```sudo -u postgres psql``` to open up the Postgresql Shell using the default postgres user and insert password
3. Now to create a new database write ```CREATE DATABASE database_name;```

Note that this makes the owner of database_name as the default postgres user. You can specify the owner by using ```CREATE DATABASE database_name OWNER your_users_name;```

You can also find more information here: [Postgresql Database: CREATE](https://www.tutorialspoint.com/postgresql/postgresql_create_database.htm)

<a name="four" />
## Viewing tables in Postgresql
This section is about how to see tables and what they contain in your Postgres database. I will be using ```database_name``` as a placeholder for your database name, and ```wanted_table``` for the table you want to inspect.

### Using PgAdmin4
1. Launch the app and insert your passwords
2. In the tab on the left side of the screen go to ```Servers > Your wanted server (Default is PostgreSQL 15) > Databases > database_name > public > Tables```
3. Now you see a list of the existing tables.
4. To see the columns in the ```wanted_table```, find it in the list of tables, click on it to expand its options, and click the ```Columns``` option. This shows all the attribute names for the table.

### Using Postgresql Shell
1. Open up the Mac Terminal
2. Run ```sudo -u postgres psql``` to open up the Postgresql Shell using the default postgres user and insert password
3. You can use ```\list``` to see the databases you have, postgres usually comes with the default databases "postgres", "template0" and "template1"
4. Now to view the tables in ```database_name``` you need to first run ```\c database_name``` to connect to it
5. If successful your shell prompt should look like the following: ```database_name=#```
6. Now to show all tables you have, you can run ```\dt```
7. To see the columns of the table you can run ```\d wanted_table```

You can also find more information here: [How to List Databases and Tables in PostgreSQL Using psql](https://chartio.com/resources/tutorials/how-to-list-databases-and-tables-in-postgresql-using-psql/) and [PostgreSQL Describe Table](https://www.postgresqltutorial.com/postgresql-administration/postgresql-describe-table/)


