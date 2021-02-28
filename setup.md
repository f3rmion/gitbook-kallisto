# Setup and Installation

This guide deal with the general setup and local installation of the `kallisto` program.

### Dependencies

We list all dependencies of `kallisto` \(v1.0.4\)

```markup
black 19.10b0 The uncompromising code formatter.
├── appdirs *
├── attrs >=18.1.0
├── click >=6.5
├── pathspec >=0.6,<1
├── regex *
├── toml >=0.9.4
└── typed-ast >=1.4.0
click 7.1.2 Composable command line interface toolkit
codecov 2.1.11 Hosted coverage reports for GitHub, Bitbucket and Gitlab
├── coverage *
│   └── toml *
└── requests >=2.7.9
    ├── certifi >=2017.4.17
    ├── chardet >=3.0.2,<5
    ├── idna >=2.5,<3
    └── urllib3 >=1.21.1,<1.27
coverage 5.4 Code coverage measurement for Python
└── toml *
flake8 3.8.4 the modular source code checker: pep8 pyflakes and co
├── importlib-metadata *
│   ├── typing-extensions >=3.6.4
│   └── zipp >=0.5
├── mccabe >=0.6.0,<0.7.0
├── pycodestyle >=2.6.0a1,<2.7.0
└── pyflakes >=2.2.0,<2.3.0
flake8-bandit 2.1.2 Automated security testing with bandit and flake8.
├── bandit *
│   ├── colorama >=0.3.9
│   ├── gitpython >=1.0.1
│   │   └── gitdb >=4.0.1,<5
│   │       └── smmap >=3.0.1,<4
│   ├── pyyaml >=5.3.1
│   ├── six >=1.10.0
│   └── stevedore >=1.20.0
│       ├── importlib-metadata >=1.7.0
│       │   ├── typing-extensions >=3.6.4
│       │   └── zipp >=0.5
│       └── pbr >=2.0.0,<2.1.0 || >2.1.0
├── flake8 *
│   ├── importlib-metadata *
│   │   ├── typing-extensions >=3.6.4
│   │   └── zipp >=0.5
│   ├── mccabe >=0.6.0,<0.7.0
│   ├── pycodestyle >=2.6.0a1,<2.7.0
│   └── pyflakes >=2.2.0,<2.3.0
├── flake8-polyfill *
│   └── flake8 *
│       ├── importlib-metadata *
│       │   ├── typing-extensions >=3.6.4
│       │   └── zipp >=0.5
│       ├── mccabe >=0.6.0,<0.7.0
│       ├── pycodestyle >=2.6.0a1,<2.7.0
│       └── pyflakes >=2.2.0,<2.3.0
└── pycodestyle *
flake8-black 0.2.1 flake8 plugin to call black as a code style validator
├── black *
│   ├── appdirs *
│   ├── attrs >=18.1.0
│   ├── click >=6.5
│   ├── pathspec >=0.6,<1
│   ├── regex *
│   ├── toml >=0.9.4
│   └── typed-ast >=1.4.0
└── flake8 >=3.0.0
    ├── importlib-metadata *
    │   ├── typing-extensions >=3.6.4
    │   └── zipp >=0.5
    ├── mccabe >=0.6.0,<0.7.0
    ├── pycodestyle >=2.6.0a1,<2.7.0
    └── pyflakes >=2.2.0,<2.3.0
flake8-bugbear 20.11.1 A plugin for flake8 finding likely bugs and design problems in your program. Contains warnings that don't belong in pyflakes and pycodestyle.
├── attrs >=19.2.0
└── flake8 >=3.0.0
    ├── importlib-metadata *
    │   ├── typing-extensions >=3.6.4
    │   └── zipp >=0.5
    ├── mccabe >=0.6.0,<0.7.0
    ├── pycodestyle >=2.6.0a1,<2.7.0
    └── pyflakes >=2.2.0,<2.3.0
flake8-import-order 0.18.1 Flake8 and pylama plugin that checks the ordering of import statements.
├── pycodestyle *
└── setuptools *
mypy 0.782 Optional static typing for Python
├── mypy-extensions >=0.4.3,<0.5.0
├── typed-ast >=1.4.0,<1.5.0
└── typing-extensions >=3.7.4
numpy 1.20.1 NumPy is the fundamental package for array computing with Python.
pytest 5.4.3 pytest: simple powerful testing with Python
├── atomicwrites >=1.0
├── attrs >=17.4.0
├── colorama *
├── importlib-metadata >=0.12
│   ├── typing-extensions >=3.6.4
│   └── zipp >=0.5
├── more-itertools >=4.0.0
├── packaging *
│   └── pyparsing >=2.0.2
├── pluggy >=0.12,<1.0
│   └── importlib-metadata >=0.12
│       ├── typing-extensions >=3.6.4
│       └── zipp >=0.5
├── py >=1.5.0
└── wcwidth *
pytest-cov 2.11.1 Pytest plugin for measuring coverage.
├── coverage >=5.2.1
│   └── toml *
└── pytest >=4.6
    ├── atomicwrites >=1.0
    ├── attrs >=17.4.0
    ├── colorama *
    ├── importlib-metadata >=0.12
    │   ├── typing-extensions >=3.6.4
    │   └── zipp >=0.5
    ├── more-itertools >=4.0.0
    ├── packaging *
    │   └── pyparsing >=2.0.2
    ├── pluggy >=0.12,<1.0
    │   └── importlib-metadata >=0.12 (circular dependency aborted here)
    ├── py >=1.5.0
    └── wcwidth *
pytype 2020.12.23 Python type inferencer
├── attrs *
├── importlab >=0.5.1
│   └── networkx >=2
│       └── decorator >=4.3.0
├── ninja >=1.10.0.post2
├── pyyaml >=3.11
├── six *
└── typed-ast *
safety 1.10.3 Checks installed dependencies for known vulnerabilities.
├── click >=6.0
├── dparse >=0.5.1
│   ├── packaging *
│   │   └── pyparsing >=2.0.2
│   ├── pyyaml *
│   └── toml *
├── packaging *
│   └── pyparsing >=2.0.2
├── requests *
│   ├── certifi >=2017.4.17
│   ├── chardet >=3.0.2,<5
│   ├── idna >=2.5,<3
│   └── urllib3 >=1.21.1,<1.27
└── setuptools *
scipy 1.6.0 SciPy: Scientific Library for Python
└── numpy >=1.16.5
```

## Install from PyPI

The `kallisto` program is [available on PyPI](https://pypi.org/project/kallisto/). The installation is straightforward using `pip`

```bash
> pip install kallisto
```

## Install from Source

Requirements to install`kallisto` from sources:

* [poetry](https://python-poetry.org/docs/#installation)
* [pyenv](https://github.com/pyenv/pyenv#installation) or [conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html)
* python &gt;=3.7

First check that `poetry` is running correctly \(v1.0.10 at the time of writing\)

```bash
> poetry --version
Poetry version 1.0.10
```

Create a virtual environment \(via `pyenv` or `conda`\) and activate it. Afterwards, clone the `kallisto` project from GitHub and install it using `poetry`

```bash
> git clone git@github.com:AstraZeneca/kallisto.git
> cd kallisto
> poetry install
```



