[![Pylama](https://camo.githubusercontent.com/c5c30dbd9e9a5149e889cdec0d7ced981d7bcceb/68747470733a2f2f7261772e6769746875622e636f6d2f6b6c656e2f70796c616d612f646576656c6f702f646f63732f5f7374617469632f6c6f676f2e706e67)](https://github.com/klen/pylama)

[See full documentation](https://pylama.readthedocs.org/)

Code audit tool for Python and JavaScript.
Pylama wraps these tools:

- [pycodestyle](https://github.com/PyCQA/pycodestyle) (formerly pep8) © 2012-2013, Florent Xicluna;
- [pydocstyle](https://github.com/PyCQA/pydocstyle/) (formerly pep257 by Vladimir Keleshev) © 2014, Amir Rachum;
- [PyFlakes](https://github.com/pyflakes/pyflakes) © 2005-2013, Kevin Watters;
- [Mccabe](http://nedbatchelder.com/blog/200803/python_code_complexity_microtool.html) © Ned Batchelder;
- [Pylint](http://pylint.org/) © 2013, Logilab (should be installed 'pylama_pylint' module);
- [Radon](https://github.com/rubik/radon) © Michele Lacchia
- [gjslint](https://developers.google.com/closure/utilities) © The Closure Linter Authors (should be installed 'pylama_gjslint' module);
- [eradicate](https://developers.google.com/closure/utilities) © Steven Myint;
- [Mypy](https://github.com/python/mypy) © Jukka Lehtosalo and contributors;

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Summary**

- [Prerequisites](#prerequisites)
- [Install](#install)
- [Configuration](#configuration)
  - [From a file](#from-a-file)
    - [Configuration format](#configuration-format)
  - [PyCharm](#pycharm)
    - [External tool](#external-tool)
- [Usage](#usage)
  - [PyTest integration](#pytest-integration)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Prerequisites

To install this tool, you will need:
- Python library 2.7 or >=3.4
    - [local](https://www.python.org/downloads/)
    - from a Docker container
- [pip](https://pip.pypa.io/en/stable/installing/) (already installed if you are using Python 2 >=2.7.9 or Python 3 >=3.4))

**Windows**

- [Docker for windows](https://docs.docker.com/docker-for-windows/)
- [Visual C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

Microsoft Visual C++ 14.0 (2015) with C++ Build Tools is required before installing `pip`.
Note that while the error is calling for vc++ 14.0 - everything will work with newer versions of visual C++.

** JavaScript checker **

To use JavaScript checker (`gjslint`) you need to install `python-gflags`:

```shell script
pip install python-gflags
```

If your tests are failing on Win platform you are missing `curses`.
The [curses](http://www.lfd.uci.edu/~gohlke/pythonlibs/) library supplies a terminal-independent screen-painting and keyboard-handling facility for text-based terminals

## Install

```shell script
pip install pylama
```

pip will install pylama in `C:\Users\<username>\AppData\Local\Programs\Python\Python39\Scripts`.

## Configuration

### From a file

Pylama looks for a configuration file in the current directory.

The `--option` / `-o` argument can be used to specify a configuration file.

Pylama searches for sections whose names start with pylama.

The "pylama" section configures global options like linters and skip.

#### Configuration format

The program searches for the first matching ini-style configuration file in the directories of command line argument.
Pylama looks for the configuration in this order:

1. pylama.ini
2. setup.cfg
3. tox.ini
4. pytest.ini

Example `pylama.ini`:

```ini
[pylama]
format = pylint
skip = */.tox/*,*/.env/*
linters = pylint,mccabe
ignore = F0401,C0111,E731
```

**Set Code-checkers' options**

You could set options for special code checker with pylama configurations.

```ini
[pylama:pyflakes]
builtins = _

[pylama:pycodestyle]
max_line_length = 100

[pylama:pylint]
max_line_length = 100
disable = R
```

See code-checkers' documentation for more info.
Let's notice that dashes are replaced by underscores (e.g. Pylint's "max-line-length" becomes "max_line_length").

**Set options for file (group of files)**

You could set options for special file (group of files) with sections:

The options have a higher priority than in the pylama section.

```ini
[pylama:*/pylama/main.py]
ignore = C901,R0914,W0212
select = R

[pylama:*/tests.py]
ignore = C0110

[pylama:*/setup.py]
skip = 1
```

### PyCharm

#### External tool

By installing the tools globally on a development machine, it is possible to create an [external tool](https://www.jetbrains.com/help/pycharm/settings-tools-external-tools.html) in Pycharm

In `Settings > Tools > External Tools`, create a new tool with the following settings:

| Key | Value |
| ------ | ------ |
| Program | C:\Users\<username>\AppData\Local\pylama |
| Arguments | $ProjectFileDir$\src |
| Working directory | $ProjectFileDir$ |

## Usage

Pylama is easy to use and really fun for checking code quality.
Just run pylama and get common output from all pylama plugins ([pycodestyle](https://github.com/PyCQA/pycodestyle), [PyFlakes](https://github.com/pyflakes/pyflakes) and etc)

Recursive check the current directory.
```shell script
pylama
```

Recursive check a path.
```shell script
pylama <path_to_directory_or_file>
```

Ignore errors
```shell script
pylama -i W,E501
```

**Note**

*You could choose a group errors D, \`E1\` and etc or special errors C0312*

Choose code checkers

```shell script
pylama -l "pycodestyle,mccabe"
```

Choose code checkers for JavaScript:

```shell script
pylama --linters=gjslint --ignore=E:0010 <path_to_directory_or_file>
```

### PyTest integration

Pylama has [Pytest](http://pytest.org/) support.
The package automatically registers itself as a pytest plugin during installation.
Pylama also supports `pytest_cache` plugin.

Check files with pylama

```shell script
pytest --pylama ...
```

Recommended way to set pylama options when using pytest — configuration files (see below).
