# Unit tests

The `kallisto` project uses [nox](https://nox.thea.codes/en/stable/tutorial.html#installation) as an automated unit test suite, which is therefore an additional dependency. Different unit test sessions are implemented:

### Complete testing suite

```bash
> nox
```

After one successful run of `nox` we can reuse the virtual environment \(faster\)

```bash
> nox -r
```

### Tests

```bash
> nox -rs tests
```

### Lint

```bash
> nox -rs lint
```

### Black

```bash
> nox -rs black
```

### Safety

```bash
> nox -rs safety
```

### Mypy

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





