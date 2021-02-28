# Testing suite

The `kallisto` project uses [nox](https://nox.thea.codes/en/stable/tutorial.html#installation) as an automated unit test suite, which is therefore an **additional dependency**.

### Default nox session

The default `nox` session includes: linting \(lint\), type checks \(mypy, pytype\), and unit tests \(tests\). When everything runs smoothly through, you are ready to go!

```bash
> nox
```

After one successful run of `nox` we can reuse the virtual environment \(faster\)

```bash
> nox -r
```

Different unit test sessions are implemented, which can be called separately via the run session \(`-rs`\) flag. I the following we describe list all sessions.

### Tests

Run all unit tests that are defined in the `/tests` directory.

```bash
> nox -rs tests
```

### Lint

`kallisto` uses the [flake8](https://flake8.pycqa.org/en/latest/) linter behind the scenes

```bash
> nox -rs lint
```

### Black

`kallisto` uses the [black](https://github.com/psf/black) code formatter

```bash
> nox -rs black
```

### Safety

`kallisto` checks the security of dependencies via [safety](https://pyup.io/safety/)

```bash
> nox -rs safety
```

### Mypy

`kallisto` checks for static types via [mypy](https://github.com/python/mypy)

```bash
> nox -rs mypy
```

### Pytype

`kallisto` furthermore uses [pytype](https://github.com/google/pytype)

```bash
> nox -rs pytype
```

### Coverage

Unit test [coverage](https://coverage.readthedocs.io/en/coverage-5.4/) is checked as well

```bash
> nox -rs coverage
```

{% hint style="info" %}
Sometimes `conda` and `nox` are getting in their ways, which could lead to a failure while running unit tests. When facing such a case, deactivate the virtual environment and try again.
{% endhint %}



