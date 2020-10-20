# Static Analysis

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Summary**

- [Prerequisites](#prerequisites)
- [Static analysis tools](#static-analysis-tools)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Prerequisites

To install those tools, you will need:
- Python library (minimum required version may vary)
    - [local](https://www.python.org/downloads/)
    - from a Docker container
- [pip](https://pip.pypa.io/en/stable/installing/) (already installed if you are using Python 2 >=2.7.9 or Python 3 >=3.4))

**Windows**

- [Docker for windows](https://docs.docker.com/docker-for-windows/)
- [Visual C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

Microsoft Visual C++ 14.0 (2015) with C++ Build Tools is required before installing `pip`.
Note that while the error is calling for vc++ 14.0 - everything will work with newer versions of visual C++.

Some of those tools are compatibles with an IDE:
- [PyCharm](https://www.jetbrains.com/pycharm/)

## Static analysis tools

- [Black](https://github.com/psf/black) see [README.md](Black/README.md)
- [Flake8](https://github.com/psf/black) see [README.md](Flake8/README.md)
- [isort](https://github.com/psf/black) see [README.md](isort/README.md)
- [Pylama](https://github.com/psf/black) see [README.md](Pylama/README.md)
- [PyLint](https://github.com/PyCQA/pylint) see [README.md](PyLint/README.md)
