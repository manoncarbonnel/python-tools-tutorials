[![isort - isort your imports, so you don't have to.](https://raw.githubusercontent.com/pycqa/isort/develop/art/logo_large.png)](https://pycqa.github.io/isort/)

[See full documentation](https://github.com/PyCQA/isort)

isort your imports, so you don't have to.

isort is a Python utility / library to sort imports alphabetically, and automatically separated into sections and by type.
it provides a command line utility, Python library and plugins for various editors to quickly sort all your imports.

*isort requires Python 3.6+ to run but supports formatting Python 2 code too.*

**Summary**

- [Prerequisites](#prerequisites)
- [Install](#install)
- [Configuration](#configuration)
  - [From a file](#from-a-file)
    - [Configuration format](#configuration-format)
  - [PyCharm](#pycharm)
    - [File watcher](#file-watcher)
    - [External tool](#external-tool)
- [Usage](#usage)
- [Version control integration](#version-control-integration)
- [Show your style](#show-your-style)

## Prerequisites

To install this tool, you will need:
- Python library >=3.6
    - [local](https://www.python.org/downloads/)
    - from a Docker container
- [pip](https://pip.pypa.io/en/stable/installing/) (already installed if you are using Python 2 >=2.7.9 or Python 3 >=3.4))

*isort requires Python 3.6+ to run but supports formatting Python 2 code too.*

**Windows**

- [Docker for windows](https://docs.docker.com/docker-for-windows/)
- [Visual C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

Microsoft Visual C++ 14.0 (2015) with C++ Build Tools is required before installing `pip`.
Note that while the error is calling for vc++ 14.0 - everything will work with newer versions of visual C++.

## Install

```shell script
pip install isort
```

Install isort with requirements.txt support:

```shell script
pip install isort[requirements_deprecated_finder]
```

Install isort with Pipfile support:

```shell script
pip install isort[pipfile_deprecated_finder]
```

Install isort with both formats support:

```shell script
pip install isort[requirements_deprecated_finder,pipfile_deprecated_finder]
```

pip will install isort in `C:\Users\<username>\AppData\Local\Programs\Python\Python39\Scripts`.

## Configuration

### From a file

isort supports various standard config formats to allow customizations to be integrated into any project quickly.
When applying configurations, isort looks for the closest supported config file, in the order files are listed below.
You can manually specify the settings file or path by setting `--settings-path` from the command-line.
Otherwise, isort will traverse up to 25 parent directories until it finds a suitable config file.
As soon as it finds a file, it stops looking.
The config file search is done relative to the current directory if `isort .` or a file stream is passed in, or relative to the first path passed in if multiple paths are passed in.
isort never merges config files together due to the confusion it can cause.

You can always introspect the configuration settings isort determined, and find out which config file it picked up, by running:

 ```shell script
isort . --show-config
```

#### Configuration format

**Preferred format**

The first place isort will look for settings is in dedicated .isort.cfg files.
The advantage of using this kind of config file, is that it is explicitly for isort and follows a well understood format.

Example `.isort.cfg`:

```cfg
[settings]
profile=hug
src_paths=isort,test
```

**Second preferred format**

The second place isort will look, and an equally excellent choice to place your configuration, is within a `pyproject.toml` file.
The advantage of using this config file, is that it is quickly becoming a standard place to configure all Python tools. This means other developers will know to look here and you will keep your projects root nice and tidy.

*This config file is the same for configuring [Black](../Black/README.md) plugin*

Example `pyproject.toml`:

```toml
[tool.isort]
profile = "hug"
src_paths = ["isort", "test"]
```

### PyCharm

#### File watcher

Locate your `isort` installation path.

On macOS / Linux / BSD:
```shell script
$ which isort
/home/user/venv/bin/isort  # Possible location
```

On Windows:
```shell script
> where isort
C:\Users\User\venv\Scripts\isort.exe  # Possible location
```

Go to `Preferences or Settings > Tools > File Watchers` and click `+` to add a new watcher:
- Name: isort
- File Type: Python
- Scope: Project Files
- Program: <isort_location_from_previous_step>
- Arguments: `$FilePath$`
- Output paths to refresh: `$FilePath$`
- Working directory: `$ProjectFileDir$`
- Uncheck "Auto-save edited files to trigger the watcher"

#### External tool

By installing the tools globally on a development machine, it is possible to create an [external tool](https://www.jetbrains.com/help/pycharm/settings-tools-external-tools.html) in Pycharm

In `Settings > Tools > External Tools`, create a new tool with the following settings:

| Key | Value |
| ------ | ------ |
| Program | C:\Users\<username>\AppData\Local\isort |
| Arguments | -e -m 4 -w 120 $ProjectFileDir$\src |
| Working directory | $ProjectFileDir$ |

## Usage

**From the command line**:

```shell script
isort mypythonfile.py mypythonfile2.py
```

or recursively:

```shell script
isort .
```

*which is equivalent to:*

```shell script
isort **/*.py
```

or to see the proposed changes without applying them:

```shell script
isort mypythonfile.py --diff
```

Using isort to verify code:

```shell script
isort -c -v .
```

Finally, to atomically run isort against a project, only applying
changes if they don't introduce syntax errors do:

```shell script
isort --atomic .
```

(Note: this is disabled by default as it keeps isort from being able to
run against code written using a different version of Python)

**From within Python**:

```python
import isort

isort.file("pythonfile.py")
```

or:

```python
import isort

sorted_code = isort.code("import b\nimport a\n")
```

## Version control integration

isort provides a hook function that can be integrated into your Git
pre-commit script to check Python code before committing.

To cause the commit to fail if there are isort errors (strict mode),
include the following in `.git/hooks/pre-commit`:

```python
#!/usr/bin/env python
import sys
from isort.hooks import git_hook

sys.exit(git_hook(strict=True, modify=True, lazy=True, settings_file=""))
```

If you just want to display warnings, but allow the commit to happen
anyway, call `git_hook` without the strict parameter. If you want to
display warnings, but not also fix the code, call `git_hook` without the
modify parameter.
The `lazy` argument is to support users who are "lazy" to add files
individually to the index and tend to use `git commit -a` instead.
Set it to `True` to ensure all tracked files are properly isorted,
leave it out or set it to `False` to check only files added to your
index.

If you want to use a specific configuration file for the hook, you can pass its
path to settings_file. If no path is specifically requested, `git_hook` will
search for the configuration file starting at the directory containing the first
staged file, as per `git diff-index` ordering, and going upward in the directory
structure until a valid configuration file is found or `MAX_CONFIG_SEARCH_DEPTH`
directories are checked.
The settings_file parameter is used to support users who keep their configuration
file in a directory that might not be a parent of all the other files.

## Show your style

[![Imports: isort](https://img.shields.io/badge/%20imports-isort-%231674b1?style=flat&labelColor=ef8336)](https://pycqa.github.io/isort/)

Place this badge at the top of your repository to let others know your project uses isort.

For README.md:

```markdown
[![Imports: isort](https://img.shields.io/badge/%20imports-isort-%231674b1?style=flat&labelColor=ef8336)](https://pycqa.github.io/isort/)
```
