[![Pylint](https://www.pylint.org/pylint.svg)](https://github.com/PyCQA/pylint)

[See full documentation](http://pylint.pycqa.org/en/latest/)

Pylint is a Python static code analysis tool which looks for programming errors, helps enforcing a coding standard, sniffs for code smells and offers simple refactoring suggestions.

It's highly configurable, having special pragmas to control its errors and warnings from within your code, as well as from an extensive configuration file.
It is also possible to write your own plugins for adding your own checks or for extending pylint in one way or another.

*Pylint is used by Pylama so consider using Pylama instead and use the PyCharm plugin only*

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Summary**

- [Prerequisites](#prerequisites)
- [Install](#install)
- [Configuration](#configuration)
  - [From a file](#from-a-file)
    - [Configuration format](#configuration-format)
  - [PyCharm](#pycharm)
    - [Plugin](#plugin)
    - [External tool](#external-tool)
- [Usage](#usage)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Prerequisites

To install this tool, you will need:
- Python library >=3.6
    - [local](https://www.python.org/downloads/)
    - from a Docker container
- [pip](https://pip.pypa.io/en/stable/installing/) (already installed if you are using Python 2 >=2.7.9 or Python 3 >=3.4))

**Windows**

- [Docker for windows](https://docs.docker.com/docker-for-windows/)
- [Visual C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

Microsoft Visual C++ 14.0 (2015) with C++ Build Tools is required before installing `pip`.
Note that while the error is calling for vc++ 14.0 - everything will work with newer versions of visual C++.

## Install

```shell script
pip install pylint
```

If you are using Python 3.6+, upgrade to get full support for your version:

```shell script
pip install pylint --upgrade
```

If you want to install from a source distribution, extract the tarball and run the following command

```shell script
python setup.py install
```

pip will install isort in `C:\Users\<username>\AppData\Local\Programs\Python\Python39\Scripts`.

## Configuration

### From a file

You can specify a configuration file on the command line using the `--rcfile` option.

Otherwise, Pylint searches for a configuration file in the following order and uses the first one it finds:

1. `pylintrc` in the current working directory
2. `.pylintrc` in the current working directory
3. `pyproject.toml` in the current working directory, providing it has at least one `tool.pylint`. section.
4. `setup.cfg` in the current working directory, providing it has at least one pylint. section
5. If the current working directory is in a Python module, Pylint searches up the hierarchy of Python modules until it finds a pylintrc file.
This allows you to specify coding standards on a module-by-module basis.
Of course, a directory is judged to be a Python module if it contains an `__init__.py` file.
6. The file named by environment variable PYLINTRC
7. if you have a home directory which isn't /root:
    1. `.pylintrc` in your home directory
    2. `.config/pylintrc` in your home directory
8. `/etc/pylintrc`

#### Configuration format

The `--generate-rcfile` option will generate a commented configuration file on standard output according to the current configuration and exit.
This includes:

- Any configuration file found as explained above
- Options appearing before `--generate-rcfile` on the Pylint command line

Of course you can also start with the default values and hand-tune the configuration.

Example `pyproject.toml`:

```cfg
[tool.pylint]
profile=hug
src_paths=isort,test
```

### PyCharm

#### Plugin

Remember the path at which it's installed:

On macOS / Linux / BSD:
```shell script
$ which pylint
/home/user/venv/bin/pylint  # Possible location
```

On Windows:
```shell script
> where pylint
C:\Users\User\venv\Scripts\pylint.exe  # Possible location
```

Go to `Settings > Plugins > Marketplace` and search for "Pylint" plugin.

Go to `Settings > Editor > Inspections > Pylint` enable `Pylint real-time scan`.

#### External tool

By installing the tools globally on a development machine, it is possible to create an [external tool](https://www.jetbrains.com/help/pycharm/settings-tools-external-tools.html) in Pycharm

In `Settings > Tools > External Tools`, create a new tool with the following settings:

| Key | Value |
| ------ | ------ |
| Program | C:\Users\<username>\AppData\Local\pylint |
| Arguments | -e -m 4 -w 120 $ProjectFileDir$\src |
| Working directory | $ProjectFileDir$ |

## Usage

**From the command line**:

```shell script
pylint [options] modules_or_packages
```
