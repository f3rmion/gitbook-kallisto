# Setup and Installation

This guide deal with the general setup and local installation of the `kallisto` program.

## Install from PyPI

The `kallisto` program is [available on PyPI](https://pypi.org/project/kallisto/). The installation is straightforward using `pip`

```bash
> pip install kallisto
```

## Install from Source

`kallisto` runs on `python3`

### Setup virtual environment

If you do not have it already installed, install the `pyenv` version manager

```text
> curl https://pyenv.run | bash
```

add the following to your `.bashrc` and source it

```text
> export PATH="~/.pyenv/bin:$PATH"
> eval "$(pyenv init -)"
> eval "$(pyenv virtualenv-init -)"
```

Install the latest `python` version

```text
> pyenv install 3.8.2
> pyenv install 3.7.7
> pyenv local 3.8.2 3.7.7
```

If you prefer to use the `conda` version manager then simply create a new virtual environment

```text
> conda create --name kallisto python=3.8
```

{% hint style="info" %}
Sometimes `conda` and `nox` are getting in their ways, which could lead to a failure while running unit tests. When facing such a case, deactivate the virtual environment and try again.
{% endhint %}

### Install the kallisto program

We start by cloning the repository

```text
> git clone git@github.com:f3rmion/kallisto.git
```

Install a python package manager, where we choose to go with [poetry](https://python-poetry.org/) via curl

```text
> curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python
> source ~/.poetry/env
```

or alternatively via `pip`

```text
> pip install --user poetry
```

Now, if you haven’t already done so, change into the cloned kallisto directory and download the dependencies via `poetry`

```text
> cd kallisto
> poetry install
```

Finally install the test automation environment [nox](https://nox.thea.codes/en/stable/) via `pip`

```text
> pip install --user --upgrade nox
```

Run `nox` to test the setup. When everything runs smoothly through, your are done!  


### Getting Help

Beside this manual you can check the in-program help by

```text
> kallisto --help
```

### The Verbose Mode

f you think some information is missing in your calculation you can switch to the verbose mode by using `--verbose` in the command line arguments.



