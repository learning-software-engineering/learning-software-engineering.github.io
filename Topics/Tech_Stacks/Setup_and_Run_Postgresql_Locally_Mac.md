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
To be able to setup Postgresql locally we first need to download it. First we check to see if we already have Postgresql installed by running: ```psql --version``` This would return the version of Postgres if you have it installed already, if you already have Postgresql installed and don't want to use PgAdmin then please move onto the next section. If not continue reading.

To Install Postgresql we will be using an interactive installer that can be found on [Postgres's website](https://www.postgresql.org/download/macosx/). Click the "Download the installer" link under the **Interactive installer by EDB** section. (**NOTE: The installer is by EDB, and will redirect you to another site**)

After arriving to the site you can click the download icon for Mac OS X for your desired version of Postgresql. This will install the interactive installer on your computer, which includes postgres and pgAdmin4. Image below:
![alt text](https://github.com/michael-j-rubenstein/learning-software-engineering.github.io/blob/main/Topics/Tech_Stacks/Images/postgres_step1_1.png)
