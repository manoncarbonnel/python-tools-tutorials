[![Behave](https://behave.readthedocs.io/en/latest/_static/behave_logo1.png)](https://github.com/behave/behave)

behave is behavior-driven development, Python style.

Behavior-driven development (or BDD) is an agile software development technique that encourages collaboration between developers, QA and non-technical or business participants in a software project.
We have a page further describing this philosophy.

behave uses tests written in a natural language style, backed up by Python code.

[See full documentation](https://behave.readthedocs.io/en/latest/)

**Summary**

- [Prerequisites](#prerequisites)
- [Install](#install)
- [Configuration](#configuration)
    - [PyCharm](#pycharm)
    - [Form a file](#from-a-file)
        - [Configuration format](#configuration-format)
- [Usage](#usage)
    - [Write your tests](#write-your-tests)
        - [Features](#features)
    - [Enhance your tests](#enhance-your-tests)
    - [Running the tests](#running-the-tests)
    - [Generate a report](#generate-a-report)
        - [HTML report](#html-report)
    
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

## Install

```shell script
pip install behave
```

pip will install Behave in `C:\Users\<username>\AppData\Local\Programs\Python\Python39\Scripts`.

## Configuration

### PyCharm

See [full documentation](https://www.jetbrains.com/help/pycharm/bdd-frameworks.html) to integrate Behave into Jetbrains PyCharm IDE.

### From a file

Configuration files for behave are called either `.behaverc`, `behave.ini`, `setup.cfg` or `tox.ini` (your preference) and are located in one of these places:

1. the current working directory (good for per-project settings),
2. your home directory ($HOME), or on Windows, in the %APPDATA% directory

If you are wondering where behave is getting its configuration defaults from you can use the `-v` command-line argument.

#### Configuration format

Configuration files must start with the label `[behave]` and are formatted in the Windows INI style, for example:

```ini
[behave]
format=plain
logging_clear_handlers=yes
logging_filter=-suds
```

## Usage

### Write your tests

You can now write your tests.

Example `features/example.feature`:

```gherkin
Feature: Showing off behave

  Scenario: Run a simple test
    Given we have behave installed
     When we implement 5 tests
     Then behave will test them for us!
```

Make a new directory called `features/steps`.
In that directory create a file called `tutorial.py` containing:

```python
from behave import *

@given('we have behave installed')
def step_impl(context):
    pass

@when('we implement a test')
def step_impl(context):
    assert True is not False

@then('behave will test it for us!')
def step_impl(context):
    assert context.failed is False
```

See the [full tutorial](https://behave.readthedocs.io/en/latest/tutorial.html) on how to write complex tests.

#### Features

Behave operates on directories containing:

1. `feature files` (written by your Business Analyst / Sponsor / whoever with your behaviour scenarios in it)
2. a `steps` directory with Python step implementations for the scenarios.

You may optionally include some environmental controls (code to run before and after steps, scenarios, features or the whole shooting match).

The minimum requirement for a features directory is:

```
features/
features/everything.feature
features/steps/
features/steps/steps.py
```

A more complex directory might look like:

```
features/
features/signup.feature
features/login.feature
features/account_details.feature
features/environment.py
features/steps/
features/steps/website.py
features/steps/utils.py
```

If you’re having trouble setting things up and want to see what behave is doing in attempting to find your features use the `-v` (verbose) command-line switch.

### Enhance your tests

[Softwares that Enhances behave](https://behave.readthedocs.io/en/latest/related.html)

### Running the tests

```shell script
behave
```

### Generate a report

#### HTML report

You can generate [Allure report](http://allure.qatools.ru/) for your Behave tests.

First you need to install Allure Behave formatter:

```shell script
pip install allure-behave
```

Then specify the formatter when run your tests:

```shell script
behave -f allure_behave.formatter:AllureFormatter -o %allure_result_folder% ./features
```

This will generate JSON report to `%allure_result_folder%`.

Then, to view HTML report you can use Allure Command line:

```shell script
allure serve %allure_result_folder%
```

For more details about Allure report you can see the [documentation](http://allure.qatools.ru/).

[![Allure test report view](http://allure.qatools.ru/img/overview.png)](http://allure.qatools.ru/)

[![Allure test report view](http://allure.qatools.ru/img/graph.png)](http://allure.qatools.ru/)
