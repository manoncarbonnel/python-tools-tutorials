# Unittest

The unittest unit testing framework was originally inspired by JUnit and has a similar flavor as major unit testing frameworks in other languages.

The unittest module provides a rich set of tools for constructing and running tests.

It supports:
 - test automation
 - sharing of setup and shutdown code for tests
 - aggregation of tests into collections
 - independence of the tests from the reporting framework

[See full documentation](https://docs.python.org/3/library/unittest.html)

**Summary**

- [Prerequisites](#prerequisites)
- [Install](#install)
- [Configuration](#configuration)
  - [PyCharm](#pycharm)
    - [Test frameworks](#test-frameworks)
- [Usage](#usage)
  - [Write your tests](#write-your-tests)
    - [Use mocks](#use-mocks)
  - [Data fixtures](#data-fixtures)
  - [Running the tests](#running-the-tests)
  - [Test Discovery](#test-discovery)
  - [Generate a report](#generate-a-report)
    - [With unittest.main()](#with-unittestmain)
    - [With Test Suites](#with-test-suites)
    - [Combining Reports into a Single Report](#combining-reports-into-a-single-report)
    - [Setting a filename](#setting-a-filename)
    
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

Unittest is already installed with Python

## Configuration

### PyCharm

Unittest is the default test runner chosen by [Jetbrains' PyCharm IDE](https://www.jetbrains.com/help/pycharm/choosing-your-testing-framework.html)

#### Test frameworks

In `Settings > Preferences > Tools > Python Integrated Tools`, in the "Default test runner" field select `unittest` and save settings.

## Usage

### Write your tests

You can now write your tests. Example:

```python
import unittest

class TestStringMethods(unittest.TestCase):

    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')

    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())

    def test_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        # check that s.split fails when the separator is not a string
        with self.assertRaises(TypeError):
            s.split(2)

if __name__ == '__main__':
    unittest.main()
```

#### Use mocks

`unittest.mock` is a library for testing in Python.
It allows you to replace parts of your system under test with mock objects and make assertions about how they have been used.

`unittest.mock` provides a core `Mock` class removing the need to create a host of stubs throughout your test suite.
After performing an action, you can make assertions about which methods / attributes were used and arguments they were called with.
You can also specify return values and set needed attributes in the normal way.

Mock is very easy to use and is designed for use with unittest.
Mock is based on the ‘action -> assertion’ pattern instead of ‘record -> replay’ used by many mocking frameworks.

`Mock` and `MagicMock` objects create all attributes and methods as you access them and store details of how they have been used.
You can configure them, to specify return values or limit what attributes are available, and then make assertions about how they have been used:e

```python
from unittest.mock import MagicMock

thing = ProductionClass()
thing.method = MagicMock(return_value=3)
thing.method(3, 4, 5, key='value') #will return 3
thing.method.assert_called_with(3, 4, 5, key='value')
```

side_effect allows you to perform side effects, including raising an exception when a mock is called:

```python
mock = Mock(side_effect=KeyError('foo'))
mock()

#Traceback (most recent call last):
# ...
#KeyError: 'foo'
```

Mock supports the mocking of Python `magic methods`.
The easiest way of using magic methods is with the MagicMock class.
It allows you to do things like:

```python
mock = MagicMock()
mock.__str__.return_value = 'foobarbaz'
str(mock) # will return 'foobarbaz'
mock.__str__.assert_called_with()
```

The following is an example of using magic methods with the ordinary Mock class:

```python
mock = Mock()
mock.__str__ = Mock(return_value='wheeeeee')
str(mock) # will return 'wheeeeee'
```

### Data fixtures

To run tests of an app, you might need reliable and clean data in your database.

To do this, use [Faker](https://faker.readthedocs.io/en/master/)

### Running the tests

```shell script
python -m unittest test_module1 test_module2
python -m unittest test_module.TestClass
python -m unittest test_module.TestClass.test_method
python -m unittest tests/test_something.py
```

You can run tests with more detail (higher verbosity) by passing in the -v flag:

```shell script
python -m unittest -v test_module
```

### Test Discovery

Unittest supports simple test discovery.
In order to be compatible with test discovery, all of the test files must be modules or packages (including namespace packages) importable from the top-level directory of the project (this means that their filenames must be valid identifiers).

```shell script
python -m unittest discover
python -m unittest discover -s project_directory -p "*_test.py" #--start-directory --pattern
python -m unittest discover project_directory "*_test.py"
```

### Generate a report

To generate an HTML report with Unittest you need [HtmlTestRunner](https://github.com/oldani/HtmlTestRunner) plugin:

```shell script
pip install html-testRunner
```

#### With unittest.main()

```python
import HtmlTestRunner
import unittest

class TestStringMethods(unittest.TestCase):
    """ Example test for HtmlRunner. """

    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')

    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())

    def test_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        # check that s.split fails when the separator is not a string
        with self.assertRaises(TypeError):
            s.split(2)

    def test_error(self):
        """ This test should be marked as error one. """
        raise ValueError

    def test_fail(self):
        """ This test should fail. """
        self.assertEqual(1, 2)

    @unittest.skip("This is a skipped test.")
    def test_skip(self):
        """ This test should be skipped. """
        pass

if __name__ == '__main__':
    unittest.main(testRunner=HtmlTestRunner.HTMLTestRunner())
```

Just import HtmlTestRunner from package, then pass it to unittest.main with the testRunner keyword.
Tests will be saved under a reports/ directory by default (the output kwarg controls this.).

#### With Test Suites

HtmlTestRunner can also be used with `test suites`; just create a runner instance and call the run method with your suite.
Here an example:

```python
from unittest import TestLoader, TestSuite
from HtmlTestRunner import HTMLTestRunner
import ExampleTest
import Example2Test

example_tests = TestLoader().loadTestsFromTestCase(ExampleTest)
example2_tests = TestLoader().loadTestsFromTestCase(Example2Test)

suite = TestSuite([example_tests, example2_tests])

runner = HTMLTestRunner(output='example_suite')

runner.run(suite)
```

#### Combining Reports into a Single Report

By default, separate reports will be produced for each TestCase.
The combine_reports boolean kwarg can be used to tell HTMLTestRunner to instead produce a single report:

```python
import HtmlTestRunner
h = HtmlTestRunner.HTMLTestRunner(combine_reports=True).run(suite)
```

#### Setting a filename

By default the name of the HTML file(s) produced will be created by joining the names of each test case together.
The report_name kwarg can be used to specify a custom filename.

For example, the following will produce a report file called `MyReport.html`:

```python
import HtmlTestRunner
h = HtmlTestRunner.HTMLTestRunner(combine_reports=True, report_name="MyReport", add_timestamp=False).run(suite)
```


