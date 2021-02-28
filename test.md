# Unit tests

The `kallisto` project uses [nox](https://nox.thea.codes/en/stable/tutorial.html#installation) as an automated unit test suite, which is therefore an additional dependency.

### Testing suite

Run `nox` to test the setup. The default tests include: linting \(lint\), type checks \(mypy, pytype\), and unit tests \(tests\). When everything runs smoothly through, you are ready to go!

```bash
> nox
```

After one successful run of `nox` we can reuse the virtual environment \(faster\)

```bash
> nox -r
```

Different unit test sessions are implemented, which can be called separately.

### Tests

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

```bash
> nox -rs pytype
```

### Coverage

```bash
> nox -rs coverage
```

{% hint style="info" %}
Sometimes `conda` and `nox` are getting in their ways, which could lead to a failure while running unit tests. When facing such a case, deactivate the virtual environment and try again.
{% endhint %}



