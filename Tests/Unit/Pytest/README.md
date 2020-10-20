[![Pytest](https://docs.pytest.org/en/stable/_static/pytest1.png)](https://github.com/pytest-dev/pytest)

The pytest framework makes it easy to write small tests, yet scales to support complex functional testing for applications and libraries.

[See full documentation](https://docs.pytest.org/en/stable/contents.html)

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Summary**

- [Prerequisites](#prerequisites)
- [Install](#install)
- [Configuration](#configuration)
  - [PyCharm](#pycharm)
    - [Test frameworks](#test-frameworks)
- [Usage](#usage)
  - [Write your tests](#write-your-tests)
  - [Data fixtures](#data-fixtures)
  - [Running the tests](#running-the-tests)
  - [Generate a report](#generate-a-report)
    - [XML report](#xml-report)
    - [HTML report](#html-report)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
    
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

```shell script
pip install -U pytest
```

pip will install Pytest in `C:\Users\<username>\AppData\Local\Programs\Python\Python39\Scripts`.

## Configuration

### PyCharm

See [full documentation](https://www.jetbrains.com/help/pycharm/pytest.html) to integrate PyTest into Jetbrains PyCharm IDE.

#### Test frameworks

In `Settings > Preferences > Tools > Python Integrated Tools`, in the "Default test runner" field select `pytest` and save settings.

## Usage

### Write your tests

You can now write your tests. Example:

```python
# content of test_sample.py
def func(x):
    return x + 1

def test_answer():
    assert func(3) == 5
```

### Data fixtures

To run tests of an app, you might need reliable and clean data in your database.
It is called [fixtures](https://pytest.org/en/stable/fixture.html).

To do this, use [Faker](https://faker.readthedocs.io/en/master/) or its plugin for Pytest [faker](https://github.com/pytest-dev/pytest-faker).

```shell script
pip install pytest-faker
```

Example `tests/test_faker.py`:

```python
from faker.generator import Generator

def test_faker(faker):
    """Faker factory is a fixture."""
    assert isinstance(faker, Generator)
    assert isinstance(faker.name(), str)
```

### Running the tests

Pytest finds the tests because of the "test_" prefix.

```shell script
pytest
```

with “quiet” reporting mode:

```shell script
pytest -q test_sample.py # --quiet
```

### Generate a report

#### XML report

It is possible to generate a text report by adding those parameters to the command `--junitxml`:

```shell script
py.test test_sample.py --junitxml=report.xml
```

#### HTML report

It is possible to generate an HTML report by using [pytest-html](https://pypi.org/project/pytest-html/) plugin and adding those parameters to the command `--html`:

Install it:

```shell script
pip install pytest-html
```

and then generate report:

```shell script
pytest test_sample.py --html=report.html
```

or generate a self-contained report:

```shell script
pytest --html=report.html --self-contained-html
```

customize your report:

```shell script
pytest --html=report.html --css=highcontrast.css --css=accessible.css
```
