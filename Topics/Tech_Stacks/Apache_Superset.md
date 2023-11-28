# Apache Superset


## Prerequisites:
* [React](https://react.dev/) for Frontend-related knowledge.
* [Node.js](https://nodejs.org/en/about) for Backend-related knowledge.
* [PostgreSQL](https://www.postgresql.org/) for SQL and Databases knowledge as well as writing queries.
* [Python](https://www.python.org/) for writing scripts as well as changing parts of the configuration files.


## Introduction:

Apache Superset is a modern, enterprise-ready business intelligence web application. It is fast, lightweight, intuitive, and loaded with options that make it easy for users of all skill sets to explore and visualize their data, from simple pie charts to highly detailed deck.gl geospatial charts.


## Set-up:

**The easiest way to set up Apache Superset is by using Docker Desktop. To install Docker Desktop, follow the instruction [HERE](https://www.docker.com/products/docker-desktop/). You can find more details about installing Superset by Docker Desktop [HERE](https://superset.apache.org/docs/installation/installing-superset-using-docker-compose).**


### Potential Issues with Docker Desktop:

1. The container named `superset_init` may exit with a code one due to a thread deadlock. To fix this issue, simply kill the process using `CTRL + C`, and re-compose it again.
2. While Apache Superset is being composed, the following method can show up:
```
 --------------------------------------------------------------------------------
                                     WARNING
 --------------------------------------------------------------------------------
 A Default SECRET_KEY was detected, please use superset_config.py to override it.
 Use a strong complex alphanumeric string and use a tool to help you generate 
 a sufficiently random sequence, ex: openssl rand -base64 42
 --------------------------------------------------------------------------------
 --------------------------------------------------------------------------------
```
This message shows up due to an update in version 2.1.0 to force secure configurations. It is fine to ignore it, but if you want to remove the warning, follow the instruction **[HERE](https://superset.apache.org/docs/installation/configuring-superset/)** to remove the warning.


**Alternatively, you can also install Apache Superset from scratch. You can find more details about this installation method [HERE](https://superset.apache.org/docs/installation/installing-superset-from-scratch).**

### Potential Issues with Installing from Scratch:

1. The command `pip install apache-superset` doesn't work. This is because Apache Superset currently supports python version 3.8 and 3.9. Any python versions that's lower or higher will result in a failure.


## Creating a Custom Plugin:

**To get started on creating a custom plugin, you can follow the instruction [HERE](https://superset.apache.org/docs/contributing/creating-viz-plugins/)** 

Note that while MacOS or Linux systems are more suitable, Windows is also a viable option if you have docker installed.

There are example plugins [example](https://github.com/preset-io/superset-plugin-chart-liquid) which you can reference. Furthermore, this [youtube tutorial](https://www.youtube.com/watch?v=LDHFY9xTzls) can help you as well.

**To set up for the plug-in, you would need to have the following in your system:**
1) apache-superset 3.0.0
2) python 3.9.7 or above
3) node version 16
4) npm version 7 or 8

### Potential Issues Creating a Custom Plugin:

Note that one may get errors from `npm run build`, but those errors do not affect the actual building of the plugin. `npm` is a large package manager, and thus it yields irrelevant errors when trying to build the plugin. In case of version conflict errors with other tools under `npm`, it is recommended to use the `--force` flag, again due to the nature of `npm`.

**IMPORTANT** : You can put the your-plugin folder anywhere in your machine EXCEPT in the superset/superset-frontend/plugins folder. The custom plugin will fail to run and cause errors if it is in that folder. This is because those are default plugins by Apache Superset and Apache Superset runs some processes on all folders in the plugin folder, which may cause errors for your plugin as your custom plugin does not have the same configurations as the default plugins provided. 

To add the package to Superset, go to the `superset-frontend` subdirectory in your Superset source folder (assuming both the `your-plugin` plugin and `superset` repos are in the same root directory) and run
```
npm i -S ../../your-plugin
```

If your Superset plugin exists in the `superset-frontend` directory and you wish to resolve TypeScript errors about `@superset-ui/core` not being resolved correctly, add the following to your `tsconfig.json` file:

```
"references": [
  {
    "path": "../../packages/superset-ui-chart-controls"
  },
  {
    "path": "../../packages/superset-ui-core"
  }
]
```

You may also wish to add the following to the `include` array in `tsconfig.json` to make Superset types available to your plugin:

```
"../../types/**/*"
```

Finally, if you wish to ensure your plugin `tsconfig.json` is aligned with the root Superset project, you may add the following to your `tsconfig.json` file:

```
"extends": "../../tsconfig.json",
```

## Connect to external database:

1. Visit the Aiven cloud website at https://aiven.io/.

2. If you don't have an account, create one.

3. Log in to your account.

4. On the left side, click on "Services."

5. Choose "Create Service."

6. Select the type of database you want to create; for this demo, choose "PostgreSQL."

7. This takes you to the database setup page.

8. Choose the "Free plan."

9. In "1. Select service region," go to North America and choose a server location.

10. In "2. Select service plan," pick "free-1-5-gb."

11. In "3. Name and tag this service," create a name for your database.

12. After completing the previous steps, select "Create Free Service."

13. Once the database is created, click on it to view details.

14. In the overview section, find the service URL and copy it; you'll use this for connecting to the database.

15. Now, go to Apache Superset, click on "Settings" in the top-right corner.

16. Click "Database Connection."

17. Click the "+ Database" button.

18. Choose the database type; for demo purposes, select "PostgreSQL."

19. Scroll to the bottom of the page and click on the blue line that says "Connect this database with an SQLAlchemy URL string instead."

20. In the display name section, fill in the name for this database.

21. In the SQLAlchemy URL section, paste the URL copied from the Aiven cloud platform.

22. Change "postgres" to "postgresql" in the URL.

23. Click "Test Connection"; it should show a "Connection looks good!" prompt in the bottom right corner.

24. Click "Connect."

Congratulations! You have successfully connected to the online database. You can now upload and extract data as needed in the future.


### How to setup preferred database options and images:

Added a new configuration option where the admin can define their preferred databases, in order:

You can change the setting of "engine_name" attribute in `superset/db_engine_specs/` as following:

```
PREFERRED_DATABASES: list[str] = [
    "PostgreSQL",
    "Presto",
    "MySQL",
    "SQLite",
]
```

### Setting images:

To set the images of your preferred database, admins must create a mapping in the superset_text.yml file with engine and location of the image. The image can be host locally inside your static/file directory or online.

```
DB_IMAGES:
  postgresql: "path/to/image/postgres.jpg"
  bigquery: "path/to/s3bucket/bigquery.jpg"
  snowflake: "path/to/image/snowflake.jpg"
```

### How to add new database engines to available endpoint:

When the user selects a database not in this list they will see the old dialog asking for the SQLAlchemy URI. New databases can be added gradually to the new flow. In order to support the rich configuration a DB engine spec needs to have the following attributes:

1. `parameters_schema`: a Marshmallow schema defining the parameters needed to configure the database. For Postgres this includes username, password, host, port, etc.

2. `default_driver`: the name of the recommended driver for the DB engine spec. Many SQLAlchemy dialects support multiple drivers, but usually one is the official 
recommendation. For Postgres we use "psycopg2".

3. `sqlalchemy_uri_placeholder`: a string that helps the user in case they want to type the URI directly.

4. `encryption_parameters`: parameters used to build the URI when the user opts for an encrypted connection. For Postgres this is `{"sslmode": "require"}`.
In addition, the DB engine spec must implement these class methods:

`build_sqlalchemy_uri(cls, parameters, encrypted_extra)`: this method receives the distinct parameters and builds the URI from them.

`get_parameters_from_uri(cls, uri, encrypted_extra)`: this method does the opposite, extracting the parameters from a given URI.

`validate_parameters(cls, parameters)`: this method is used for `onBlur` validation of the form. It should return a list of `SupersetError` indicating which parameters are missing, and which parameters are definitely incorrect 

For databases like MySQL and Postgres that use the standard format of `engine+driver://user:password@host:port/dbname`, you need to do is add the `BasicParametersMixin` to the DB engine spec, and then define the parameters 2-4 (`parameters_schema` is already present in the mixin).



## Extra Resources:

* [Installing Apache Superset on Kubernetes](https://superset.apache.org/docs/installation/running-on-kubernetes)
* [Additional Network Settings](https://superset.apache.org/docs/installation/networking-settings)
* [Apache Superset GitHub Page](https://github.com/apache/superset/)
* [GitHub Issues for Apache Superset](https://github.com/apache/superset/issues)
* [Aiven cloud]  (https://aiven.io/)
* [Apache Superset: Using Database Connection UI] (https://superset.apache.org/docs/databases/db-connection-ui/#setting-images)
