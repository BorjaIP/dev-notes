---
id: oo65lf1fyvshu00tqre9avx
title: Python
desc: ''
updated: 1675793521946
created: 1655321005187
---

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

## Sphinx

Useful [extensions](https://sphinx-extensions.readthedocs.io/en/latest/index.html).

```bash
# autobuild sphinx documentation
sphinx-autobuild docs/source docs/build/html
```
