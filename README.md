# Calculator — Python testing practice

A small calculator module used to practise structuring a real test suite and wiring up quality tooling around it. The arithmetic is trivial on purpose; the point of the repo is everything around it.

## Layout

```
src/calculator.py          arithmetic with input validation and error handling
tests/unit/                unit tests
tests/integration/         integration tests
pytest.ini                 markers, test paths, coverage-friendly config
requirements.txt           pytest, pytest-cov, pylint, bandit, black
.github/workflows/ci.yml   pipeline scaffold (see note below)
```

## Test configuration

`pytest.ini` registers severity markers rather than relying on naming conventions, so tests can be selected by level of the pyramid:

```
markers =
    unit: Unit tests
    integration: Integration tests
    system: System tests
    acceptance: Acceptance tests
    slow: Slow running tests
```

Run by marker:

```bash
pytest -m unit
pytest -m integration
pytest -m "not slow" --cov=src
```

## Quality tooling

`requirements.txt` pulls in the full set used across the course:

| Tool | Purpose |
|---|---|
| `pytest` + `pytest-cov` | test runner and coverage |
| `pylint` | style and static analysis |
| `bandit` | security-oriented static analysis |
| `black` | formatting |

## Note on the CI workflow

`.github/workflows/ci.yml` is deliberately a **stub**. It is set to `workflow_dispatch` only and its single step echoes that nothing runs on push or PR. It's a scaffold for wiring up a real pipeline, not a working one — worth being explicit rather than letting the green badge imply otherwise.

Wiring it up would mean adding a `push`/`pull_request` trigger, a Python setup step, `pip install -r requirements.txt`, then `pytest --cov`, `pylint src` and `bandit -r src`.

## Run it

```bash
pip install -r requirements.txt
pytest
```
