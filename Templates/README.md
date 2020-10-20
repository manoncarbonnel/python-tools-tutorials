# PROJECT NAME
![pipeline](https://github.com/<projetc_path>/badges/develop/pipeline.svg)
![coverage](https://github.com/<projetc_path>/badges/develop/coverage.svg)

[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Imports: isort](https://img.shields.io/badge/%20imports-isort-%231674b1?style=flat&labelColor=ef8336)](https://pycqa.github.io/isort/)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)

*Project description*

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Summary**

- [Getting Started](#getting-started)
- [Prerequisites](#prerequisites)
- [Installing](#installing)
  - [Configuration](#configuration)
  - [Docker compose usage](#docker-compose-usage)
  - [Dependencies install](#dependencies-install)
  - [Data import](#data-import)
  - [Source files](#source-files)
- [Environment](#environment)
  - [Code quality](#code-quality)
- [Python commands usage](#python-commands-usage)
- [Running the tests](#running-the-tests)
  - [Unit testing](#unit-testing)
  - [End to end tests testing](#end-to-end-tests-testing)
- [Delivery](#delivery)
- [Deployment](#deployment)
  - [Test environment](#test-environment)
  - [Production environment](#production-environment)
- [Built With](#built-with)
- [Versioning](#versioning)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.
See deployment for notes on how to deploy the project on a live system.
You can plug any of this tools to your favourite IDE.

## Prerequisites

You need to have the following softwares installed on your local machine:
- Python library
    - [local](https://www.python.org/downloads/)
    - from a Docker container
- [pip](https://pip.pypa.io/en/stable/installing/) (already installed if you are using Python 2 >=2.7.9 or Python 3 >=3.4))

**Windows**

- [Docker for windows](https://docs.docker.com/docker-for-windows/)
- [Visual C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

Microsoft Visual C++ 14.0 (2015) with C++ Build Tools is required before installing `pip`.
Note that while the error is calling for vc++ 14.0 - everything will work with newer versions of visual C++.


## Installing

Clone project using ssh (you will need to set a SSH key in your Gitlab profile) 
```shell script
git clone git@github.com
```

### Configuration

- Each `./Dockerfile` contains a basic configuration for developing with [Python](https://www.python.org/) and deploying in a production environment
- The file `.env` allows to set the name of the Docker project's stack as well as basic Python image version for Docker
- The file `.env.dev.local` must be created (and git ignored) to fill in empty parameters from the `/.env` file 

### Docker compose usage

- Run / init: `docker-compose up`
- Stop: `docker-compose stop`
- Destroy: `docker-compose down`
- Cleanup: `docker-compose rm -vsf`
- Reset:  `docker system prune -af --volumes`

### Dependencies install

When starting the `backend` container, [pip](https://pypi.org/project/pip/) will download and install dependencies in the dedicated directory

### Data import

We use *name and link to the SGBDR documentation* for this project.

*Explain how to import data when you start working on this project*

### Source files

*Explain where your source code is located*

## Environment

### Code quality

We use code quality tools which you can plug in your favourite IDE:

*List which code quality tools are used and mandatory in this project*
*For each tool: name, link to documentation and path to the associated config file*

## Python commands usage

Use this *pattern*
```shell script
docker-compose exec backend <entrypoint> <command> <args>
```

## Running the tests

### Unit testing

Launch tests with associated config file in `` *Path to the test config file*

```shell script
docker-compose exec backend <entrypoint> <command> <args>
```

### End to end tests testing

Launch tests with associated config file in `` *path to the test config file*

```shell script
docker-compose exec backend <entrypoint> <command> <args>
```

## Delivery

*Explain how do you deliver the project to the client*

## Deployment

### Test environment

*Explain how do you deploy in test environment*

### Production environment

*Explain how do you deploy in production environment*

## Built With

*List which code and test frameworks and libraries are used in this project*
*For each one: name and link to documentation*

![Python](https://www.python.org/static/img/python-logo.png)

- [Docker](https://www.docker.com/) - Virtualization and container management

## Versioning

We use [Git](https://git-scm.com/) and [Gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) with [conventional commits](https://www.conventionalcommits.org/) for versioning.
