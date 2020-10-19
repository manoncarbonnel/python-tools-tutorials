![Black](https://raw.githubusercontent.com/psf/black/master/docs/_static/logo2-readme.png)

[See full documentation](https://github.com/psf/black)

Black is the uncompromising Python code formatter.
By using it, you agree to cede control over minutiae of hand-formatting.
In return, Black gives you speed, determinism, and freedom from `pycodestyle` nagging about formatting.
You will save time and mental energy for more important matters.

Blackened code looks the same regardless of the project you're reading.
Formatting becomes transparent after a while and you can focus on the content instead.

Black makes code review faster by producing the smallest diffs possible.

**Summary**

- [Prerequisites](#prerequisites)
- [Install](#install)
- [Configuration](#configuration)
  - [From a file](#from-a-file)
    - [Where Black looks for the file](#where-black-looks-for-the-file)
    - [Configuration format](#configuration-format)
    - [Plugin compatibility](#plugin-compatibility)
  - [PyCharm](#pycharm)
    - [External tool](#external-tool)
- [Usage](#usage)
- [Version Control integration](#version-control-integration)
- [Show your style](#show-your-style)

## Prerequisites

To install this tool, you will need:
- Python library
    - [local](https://www.python.org/downloads/)
    - from a Docker container
- [pip](https://pip.pypa.io/en/stable/installing/) (already installed if you are using Python 2 >=2.7.9 or Python 3 >=3.4))

**Windows**

- [Docker for windows](https://docs.docker.com/docker-for-windows/)
- [Visual C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

Microsoft Visual C++ 14.0 (2015) with C++ Build Tools is required before installing `pip`.
Note that while the error is calling for vc++ 14.0 - everything will work with newer versions of visual C++.

## Install

``` shell
pip install black
```

pip will install Black in `C:\Users\<username>\AppData\Local\Programs\Python\Python39\Scripts`.

## Configuration

### From a file

Black is able to read project-specific default values for its command line options from a `pyproject.toml` file.
This is especially useful for specifying custom `--include` and `--exclude` patterns for your project.

#### Where Black looks for the file

By default Black looks for `pyproject.toml` starting from the common base directory of all files and directories passed on the command line.
If it's not there, it looks in parent directories.
It stops looking when it finds the file, or a `.git` directory, or a `.hg` directory, or the root of the file system, whichever comes first.

If you're formatting standard input, Black will look for configuration starting from the current working directory.

You can also explicitly specify the path to a particular file that you want with `--config`.
In this situation Black will not look for any other file.

If you're running with `--verbose`, you will see a blue message if a file was found and used.

#### Configuration format

Example `pyproject.toml`:

```toml
[tool.black]
line-length = 88
target-version = ['py37']
include = '\.pyi?$'
exclude = '''

(
  /(
      \.eggs         # exclude a few common directories in the
    | \.git          # root of the project
    | \.hg
    | \.mypy_cache
    | \.tox
    | \.venv
    | _build
    | buck-out
    | build
    | dist
  )/
  | foo.py           # also separately exclude a file named foo.py in
                     # the root of the project
)
'''
```

### Plugin compatibility

Black can behave according to different standards than [isort](../isort/README.md), [Flake8](../Flake8/README.md) or [Pylint](https://github.com/PyCQA/pylint/).
To ensure compatibility, you can check the documentation here:
[Black compatible configurations](https://black.readthedocs.io/en/stable/compatible_configs.html)

### PyCharm

#### External tool

By installing the tools globally on a development machine, it is possible to create an [external tool](https://www.jetbrains.com/help/pycharm/settings-tools-external-tools.html) in Pycharm

In `Settings > Tools > External Tools`, create a new tool with the following settings:

| Key | Value |
| ------ | ------ |
| Program | C:\Users\<username>\AppData\Local\black\black |
| Arguments | $ProjectFileDir$\src |
| Working directory | $ProjectFileDir$ |

## Usage

To get started right away with sensible defaults:

```shell script
black {source_file_or_directory}
```

You can run Black as a package if running it as a script doesn't work:

```shell script
python -m black {source_file_or_directory}
```

Black is a well-behaved Unix-style command-line tool:

- it does nothing if no sources are passed to it;
- it will read from standard input and write to standard output if `-` is used as the filename;
- it only outputs messages to users on standard error;
- exits with code 0 unless an internal error occurred (or `--check` was used).

## Version control integration

Use [pre-commit](https://pre-commit.com/). Once you
[have it installed](https://pre-commit.com/#install), add this to the
`.pre-commit-config.yaml` in your repository:

```yaml
repos:
  - repo: https://github.com/psf/black
    rev: 19.10b0 # Replace by any tag/version: https://github.com/psf/black/tags
    hooks:
      - id: black
        language_version: python3 # Should be a command that runs python3.6+
```

Then run `pre-commit install` and you're ready to go.

Avoid using `args` in the hook. Instead, store necessary configuration in
`pyproject.toml` so that editors and command-line usage of Black all behave consistently
for your project. See _Black_'s own
[pyproject.toml](https://github.com/psf/black/blob/master/pyproject.toml) for an
example.

If you're already using Python 3.7, switch the `language_version` accordingly. Finally,
`stable` is a branch that tracks the latest release on PyPI. If you'd rather run on
master, this is also an option.

## Show your style

Use the badge in your project's README.md:

```md
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
```

Using the badge in README.rst:

```
.. image:: https://img.shields.io/badge/code%20style-black-000000.svg
    :target: https://github.com/psf/black
```

Looks like this:
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
