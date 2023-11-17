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

There are example plugins [example](https://github.com/preset-io/superset-plugin-chart-liquid) which you can reference. Furthermore, this [youtube tutorial](https://www.youtube.com/watch?v=LDHFY9xTzls) can help you as well.

**To set up for the plug-in, you would need to have the following in your system:**
1) apache-superset 3.0.0
2) python 3.9.7 or above
3) node version 16
4) npm version 7 or 8

### Potential Issues Creating a Custom Plugin:

Note that one may get errors from `npm run build`, but those errors do not affect the actual building of the plugin. `npm` is a large package manager, and thus it yields irrelevant errors when trying to build the plugin. In case of version conflict errors with other tools under `npm`, it is recommended to use the `--force` flag, again due to the nature of `npm`.

**IMPORTANT** : You can put the mapbox-plugin folder anywhere in your machine EXCEPT in the superset/superset-frontend/plugins folder. The custom plugin will fail to run and cause errors if it is in that folder. This is because those are default plugins by Apache Superset and Apache Superset runs some processes on all folders in the plugin folder, which may cause errors for your plugin as your custom plugin does not have the same configurations as the default plugins provided. 

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

## Extra Resources:

* [Installing Apache Superset on Kubernetes](https://superset.apache.org/docs/installation/running-on-kubernetes)
* [Additional Network Settings](https://superset.apache.org/docs/installation/networking-settings)
* [Apache Superset GitHub Page](https://github.com/apache/superset/)
* [GitHub Issues for Apache Superset](https://github.com/apache/superset/issues)
