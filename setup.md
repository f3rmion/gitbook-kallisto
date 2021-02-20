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

```bash
> curl https://pyenv.run | bash
```

add the following to your `.bashrc` and source it

```bash
> export PATH="~/.pyenv/bin:$PATH"
> eval "$(pyenv init -)"
> eval "$(pyenv virtualenv-init -)"
```

Install the latest `python` version

```bash
> pyenv install 3.8.2
> pyenv install 3.7.7
> pyenv local 3.8.2 3.7.7
```

If you prefer to use the `conda` version manager than simply create a new virtual environment

```bash
> conda create --name kallisto python=3.8
```

{% hint style="info" %}
Sometimes `conda` and `nox` are getting in their ways, which could lead to a failure while running unit tests. When facing such a case, deactivate the virtual environment and try again.
{% endhint %}

### Clone and install the kallisto program

We start by cloning the repository

```bash
> git clone git@github.com:AstraZeneca/kallisto.git
```

Install a python package manager, where we choose to go with [poetry](https://python-poetry.org/) via curl

```bash
> curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python
> source ~/.poetry/env
```

or alternatively via `pip`

```bash
> pip install --user poetry
```

Check that `poetry` is running correctly

```bash
> poetry --version
Poetry version 1.0.10
```

Now, if you haven’t already done so, change into the cloned kallisto directory and download the dependencies via `poetry`

```bash
> cd kallisto
> poetry install
```

Finally, install the test automation environment [nox](https://nox.thea.codes/en/stable/) via `pip`

```bash
> pip install --user --upgrade nox
```

Run `nox` to test the setup. When everything runs smoothly through, you are done!  


### Getting Help

Besides this manual, you can check the in-program help by

```bash
> kallisto --help
```

### The Verbose Mode

If you think some information is missing in your calculation you can switch to the verbose mode by using `--verbose` in the command line arguments.



