[![Pre-commit](https://pre-commit.com/logo-top-shelf.png)](https://pre-commit.com/)

[See full documentation](https://pre-commit.com/)

Git hook scripts are useful for identifying simple issues before submission to code review.
Running hooks on every commit automatically point out issues in code such as trailing whitespace, and debug statements.
By pointing these issues out before code review allows a code reviewer to focus on the architecture of a change while not wasting time with trivial style nitpicks.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Summary**

- [Prerequisites](#prerequisites)
- [Install](#install)
- [Configuration](#configuration)
- [Usage](#usage)
- [Show your style](#show-your-style)

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

Before you can run hooks, you need to have the pre-commit package manager installed.

```shell script
pip install pre-commit
```

In a python project, add the following to your `requirements.txt` (or `requirements-dev.txt`):

```shell script
pre-commit
```

## Configuration

- create a file named `pre-commit-config.yaml` to the root of your project
- you can generate a very basic configuration using `pre-commit sample-config`
- the full set of options for the configuration are listed [here](https://pre-commit.com/#plugins)

Example `pre-commit-config.yaml`:

```yaml
repos:
-   repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v2.3.0
    hooks:
    -   id: check-yaml
    -   id: end-of-file-fixer
    -   id: trailing-whitespace
-   repo: https://github.com/psf/black
    rev: 19.3b0
    hooks:
    -   id: black
```

## Usage

Run `pre-commit install` to install pre-commit into your git hooks.
pre-commit will now run on every commit.

```shell script
pre-commit install
# pre-commit installed at .git/hooks/pre-commit
```

If you want to manually run all pre-commit hooks on a repository, run `pre-commit run --all-files`.
To run individual hooks use `pre-commit run <hook_id>`.

## Show your style

[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)

Place this badge at the top of your repository to let others know your project uses pre-commit.

For README.md:

```markdown
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)
```
