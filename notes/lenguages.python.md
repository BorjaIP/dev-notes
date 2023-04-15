---
id: oo65lf1fyvshu00tqre9avx
title: Python
desc: ''
updated: 1681576076223
created: 1655321005187
---

- [Libraries](#libraries)
- [Pytest](#pytest)
- [Setuptools](#setuptools)
- [Sphinx](#sphinx)
- [Pre-commit](#pre-commit)

[Awesome](https://github.com/carlosperate/awesome-pyproject/)

```bash
pip install pipdeptree 
pipdeptree > result.txt

# licenses
pip install pip-licenses
pip-licenses --from=classifier --with-description --order=license --format=html --output-file=/result.html

# si peta por ModuleNotFoundError: No module named 'keyring.util.escape'
pip3 install --upgrade keyrings.alt

# show pip config
pip config list -v

# FLASK
flask routes
```

## Libraries

[Pipdeptree](https://github.com/naiquevin/pipdeptree) - Display dependencies tree
[Databases](https://www.encode.io/databases/) - Conector multiple databases
[Vulture](https://pypi.org/project/vulture/) - Dead code
[Hatch](https://github.com/pypa/hatch) - Modern, extensible Python project management 
[Towncrier](https://github.com/twisted/towncrier) - Manage the release notes for your project
[Gitlin](https://github.com/jorisroovers/gitlint) - Linting for your git commit messages
[python-license-check](https://github.com/dhatim/python-license-check) - Check python packages from requirement.txt and report issues
[Pycln](https://github.com/hadialqattan/pycln) - A formatter for finding and removing unused import statements
[Typeshed](https://github.com/python/typeshed) - Collection of library stubs for Python, with static types
[Safety](https://github.com/pyupio/safety) - Checks Python dependencies for known security vulnerabilities

## Pytest

- HTML report [pytest-html-reporter](https://github.com/prashanth-sams/pytest-html-reporter).
- Coverage test [pytest-cov](https://github.com/pytest-dev/pytest-cov).
- Understanding [fixtures](https://betterprogramming.pub/understand-5-scopes-of-pytest-fixtures-1b607b5c19ed).
- Scopes [fixtures](https://docs.pytest.org/en/latest/how-to/fixtures.html#fixture-scopes).

```bash
# list fixtures availables
pytest --fixtures
# run single function
pytest test_mod.py::test_func

# Marker tests
@pytest.mark.unit
def test_get()
pytest -m unit -v

# coverage instructions
--cov package --cov-branch --cov-report term-missing
```

## Setuptools

Distribution package for Python

[Setup](https://setuptools.pypa.io/en/latest/setuptools.html)

[Classifiers](https://pypi.org/classifiers/) por **pytroject.toml**  and display in Pypi.

## Sphinx

Useful [extensions](https://sphinx-extensions.readthedocs.io/en/latest/index.html).

```bash
# autobuild sphinx documentation
sphinx-autobuild docs/source docs/build/html
```

## Pre-commit

pre-commit run --files client/example.py