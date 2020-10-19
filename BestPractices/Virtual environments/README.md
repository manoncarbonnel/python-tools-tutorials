# Virtual environments

Python applications will often use packages and modules that don’t come as part of the standard library.
Applications will sometimes need a specific version of a library, because the application may require that a particular bug has been fixed or the application may be written using an obsolete version of the library’s interface.

This means it may not be possible for one Python installation to meet the requirements of every application.
If application A needs version 1.0 of a particular module but application B needs version 2.0, then the requirements are in conflict and installing either version 1.0 or 2.0 will leave one application unable to run.

The solution for this problem is to create a virtual environment, a self-contained directory tree that contains a Python installation for a particular version of Python, plus a number of additional packages.

Different applications can then use different virtual environments.
To resolve the earlier example of conflicting requirements, application A can have its own virtual environment with version 1.0 installed while application B has another virtual environment with version 2.0.
If application B requires a library be upgraded to version 3.0, this will not affect application A’s environment.

[Here](https://docs.python.org/3/tutorial/venv.html) is the full Python documentation about virtual environments.

**Summary**

- [Prerequisites](#prerequisites)
- [virtualenvwrapper](#virtualenvwrapper)
    - [Install](#install)
    - [Configuration](#configuration)
    - [Usage](#usage)

## Prerequisites

To install those tools, you will need:
- Python library
    - [local](https://www.python.org/downloads/)
    - from a Docker container
- [pip](https://pip.pypa.io/en/stable/installing/) (already installed if you are using Python 2 >=2.7.9 or Python 3 >=3.4))

**Windows**

- [Docker for windows](https://docs.docker.com/docker-for-windows/)
- [Visual C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

Microsoft Visual C++ 14.0 (2015) with C++ Build Tools is required before installing `pip`.
Note that while the error is calling for vc++ 14.0 - everything will work with newer versions of visual C++.

## virtualenvwrapper

See full documentation [here](https://virtualenvwrapper.readthedocs.io/en/latest/index.html)

### Install

```shell script
sudo pip install virtualenvwrapper
```

Then add the following lines to your shell startup file :

```shell script
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/workspace/
source /usr/local/bin/virtualenvwrapper.sh
```

### Configuration

virtualenvwrapper can be customized by changing environment variables.

Set the variables in your shell startup file before loading `virtualenvwrapper.sh`.

### Usage

List environments:

```shell script
workon
```

Create a virtualenv:

```shell script
mkvirtualenv my_env #A new environment, `my_env` is created and activated
mkvirtualenv my_env -a project_path #attach virtualenv to project path
mkvirtualenv my_env -r requirements.txt #specify a text file listing packages to be installed
```

Activate a specific virtualenv:

```shell script
workon my_env
```

Deactivate current running environment:

```shell script
deactivate
```

Remove a virtualenv *(You must use deactivate before removing the current environment)*:

```shell script
rmvirtualenv my_env
```

You can find all available commands [here](https://virtualenvwrapper.readthedocs.io/en/latest/command_ref.html)
