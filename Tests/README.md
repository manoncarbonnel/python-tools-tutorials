# Tests

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Summary**

- [Prerequisites](#prerequisites)
- [Test tools](#test-tools)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

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

## Test tools

- Unit tests
    - [Unittest](Unit/unittest/README.md)
    - [Pytest](Unit/Pytest/README.md)
- End to end tests
    - [Behave](EndToEnd/Behave/README.md)
-Data Fixtures
    - [Faker](DataFixtures/Faker/README.md)
