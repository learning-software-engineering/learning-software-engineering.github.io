# Apache Superset

## Table of contents
### [Prerequisites](#prerequisites-1)
### [Introduction](#introduction-1)
### [Set-up](#set-up-1)
### [Extra Resources](#extra-resource-1)

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


## Extra Resources:

* [Installing Apache Superset on Kubernetes](https://superset.apache.org/docs/installation/running-on-kubernetes)
* [Additional Network Settings](https://superset.apache.org/docs/installation/networking-settings)
* [Apache Superset GitHub Page](https://github.com/apache/superset/)
* [GitHub Issues for Apache Superset](https://github.com/apache/superset/issues)
