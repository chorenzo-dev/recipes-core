## Python + GitHub Actions Specifics

### Python Environment
Use `actions/setup-python@v4` with version detection from `pyproject.toml`, `.python-version`, or `runtime.txt`. Enable pip caching with `cache: 'pip'`.

### Change Detection for Python
Use `dorny/paths-filter@v2` with paths:
- Source files: `**/*.py`
- Dependency files: `requirements*.txt`, `pyproject.toml`, `setup.py`, `Pipfile`, `poetry.lock`
- Test files: `tests/**`, `**/test_*.py`, `**/*_test.py`

### Python-Specific Commands
- Dependency installation: `pip install -r requirements.txt` or `pip install -e .`
- Package building: `python -m build`
- Formatting check: `black --check .` and `isort --check-only .`
- Linting: `flake8 .` or `pylint **/*.py` or `ruff check`
- Type checking: `mypy .`
- Test with coverage: `pytest --cov=. --cov-report=xml`

### Python Monorepo Support
- Poetry workspaces: `poetry install` and `poetry run pytest`
- Multiple packages: `pip install -e packages/*/`
- Per-package testing: Use matrix strategy with package directories