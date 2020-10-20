    _|_|_|_|          _|
    _|        _|_|_|  _|  _|      _|_|    _|  _|_|
    _|_|_|  _|    _|  _|_|      _|_|_|_|  _|_|
    _|      _|    _|  _|  _|    _|        _|
    _|        _|_|_|  _|    _|    _|_|_|  _|

Faker is a Python package that generates fake data for you.

Whether you need to bootstrap your database, create good-looking XML documents, fill-in your persistence to stress test it, or anonymize data taken from a production service, Faker is for you.

[See full documentation](https://github.com/joke2k/faker)

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Summary**

- [Prerequisites](#prerequisites)
- [Install](#install)
- [Usage](#usage)
  - [Command line](#command-line)
  - [Localization](#localization)
  - [Unique values](#unique-values)
  - [Seeding the Generator](#seeding-the-generator)
- [Pytest Fixtures](#pytest-fixtures)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Prerequisites

Starting from version 4.0.0, Faker dropped support for Python 2 and only supports Python 3.5 and above.
 If you still need Python 2 compatibility, please install version 3.0.1 in the meantime, and please consider updating your codebase to support Python 3 so you can enjoy the latest features Faker has to offer.

To install this tool, you will need:
- Python library >=3.5
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
pip install Faker
```

pip will install Faker in `C:\Users\<username>\AppData\Local\Programs\Python\Python39\Scripts`.

## Usage

Use `faker.Faker()` to create and initialize a faker generator, which can generate data by accessing properties named after the type of data you want.

```python
from faker import Faker

fake = Faker()

fake.name()
# 'Lucy Cechtelar'

fake.address()
# '426 Jordy Lodge
#  Cartwrightshire, SC 88120-6700'

fake.text()
# 'Sint velit eveniet. Rerum atque repellat voluptatem quia rerum. Numquam excepturi
#  beatae sint laudantium consequatur. Magni occaecati itaque sint et sit tempore. Nesciunt
#  amet quidem. Iusto deleniti cum autem ad quia aperiam.
#  A consectetur quos aliquam. In iste aliquid et aut similique suscipit. Consequatur qui
#  quaerat iste minus hic expedita. Consequuntur error magni et laboriosam. Aut aspernatur
#  voluptatem sit aliquam. Dolores voluptatum est.
#  Aut molestias et maxime. Fugit autem facilis quos vero. Eius quibusdam possimus est.
#  Ea quaerat et quisquam. Deleniti sunt quam. Adipisci consequatur id in occaecati.
#  Et sint et. Ut ducimus quod nemo ab voluptatum.'
```

Each call to method `fake.name()` yields a different (random) result.
This is because faker forwards `faker.Generator.method_name()` calls to `faker.Generator.format(method_name)`.

```python
from faker import Faker

fake = Faker()

for _ in range(10):
  print(fake.name())

# 'Adaline Reichel'
# 'Dr. Santa Prosacco DVM'
# 'Noemy Vandervort V'
# 'Lexi O'Conner'
# 'Gracie Weber'
# 'Roscoe Johns'
# 'Emmett Lebsack'
# 'Keegan Thiel'
# 'Wellington Koelpin II'
# 'Ms. Karley Kiehn V'
```

### Command line

When installed, you can invoke faker from the command-line:

```shell script
faker [-h] [--version] [-o output]
      [-l {bg_BG,cs_CZ,...,zh_CN,zh_TW}]
      [-r REPEAT] [-s SEP]
      [-i {package.containing.custom_provider otherpkg.containing.custom_provider}]
      [fake] [fake argument [fake argument ...]]
```

```shell script
faker address
# 968 Bahringer Garden Apt. 722
# Kristinaland, NJ 09890

faker -l de_DE address
# Samira-Niemeier-Allee 56
# 94812 Biedenkopf

faker profile ssn,birthdate
# {'ssn': u'628-10-1085', 'birthdate': '2008-03-29'}

faker -r=3 -s=";" name
# Willam Kertzmann;
# Josiah Maggio;
# Gayla Schmitt;
```

### Localization

`faker.Faker` can take a locale as an argument, to return localized data.
If no localized provider is found, the factory falls back to the default en_US locale.
You can check available Faker locales in the source code, under the providers package. 

```python
from faker import Faker

fake = Faker('it_IT')

for _ in range(10):
    print(fake.name())

# 'Elda Palumbo'
# 'Pacifico Giordano'
# 'Sig. Avide Guerra'
# 'Yago Amato'
# 'Eustachio Messina'
# 'Dott. Violante Lombardo'
# 'Sig. Alighieri Monti'
# 'Costanzo Costa'
# 'Nazzareno Barbieri'
# 'Max Coppola'
```

faker.Faker also supports multiple locales. New in v3.0.0.

```python
from faker import Faker

fake = Faker(['it_IT', 'en_US', 'ja_JP'])

for _ in range(10):
    print(fake.name())

# 鈴木 陽一
# Leslie Moreno
# Emma Williams
# 渡辺 裕美子
# Marcantonio Galuppi
# Martha Davis
# Kristen Turner
# 中津川 春香
# Ashley Castillo
# 山田 桃子
```

### Unique values

Through use of the .unique property on the generator, you can guarantee that any generated values are unique for this specific instance.

```python
from faker import Faker

fake = Faker()
names = [fake.unique.first_name() for i in range(500)]
assert len(set(names)) == len(names)
```

### Seeding the Generator

When using Faker for unit testing, you will often want to generate the same data set.
For convenience, the generator also provide a `seed()` method, which seeds the shared random number generator. Calling the same methods with the same version of faker and seed produces the same results.

```python
from faker import Faker

fake = Faker()
Faker.seed(4321)

print(fake.name())
# 'Margaret Boehm'
```

Each generator can also be switched to its own instance of `random.Random`, separate to the shared one, by using the `seed_instance()` method, which acts the same way.

For example:

```python
from faker import Faker

fake = Faker()
fake.seed_instance(4321)

print(fake.name())
# 'Margaret Boehm'
```

If you are using `pytest`, you can seed the faker fixture by defining a `faker_seed` fixture.
See the [Pytest Fixtures](#pytest-fixtures) section below.

## Pytest Fixtures

To run tests of an app, you might need reliable and clean data in your database. It is called fixtures.
`Faker` also has its own `pytest` plugin which provides a `faker` fixture you can use in your tests.
Please check out the [pytest fixture docs](https://docs.pytest.org/en/stable/fixture.html) to learn more.

To do this, use the plugin for Pytest [faker](https://github.com/pytest-dev/pytest-faker).

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
