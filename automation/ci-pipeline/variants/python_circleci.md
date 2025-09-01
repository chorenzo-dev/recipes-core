## Python + CircleCI Specifics

### CircleCI Python Configuration
Use `.circleci/config.yml` with Python orb `circleci/python@2.0.3`. Configure Docker image `cimg/python:${version}` based on `pyproject.toml`, `.python-version`, or `runtime.txt`.

### Python Change Detection
Utilize `CIRCLE_COMPARE_URL` to detect Python file changes:
- Source: `**/*.py`
- Dependencies: `requirements*.txt`, `pyproject.toml`, `setup.py`, `Pipfile`
- Tests: `tests/**`, `**/test_*.py`

### CircleCI Python Commands
- Dependency installation: `python/install-packages` (orb) or `pip install -r requirements.txt`
- Package building: `python -m build`
- Formatting: `black --check .` and `isort --check-only .`
- Linting: `flake8 .` or `ruff check`
- Type checking: `mypy .`
- Testing: `pytest --cov=. --cov-report=xml`

### Python Artifacts
- Test results: Store JUnit XML from pytest
- Coverage: Store `coverage.xml` and HTML reports
- Build artifacts: Persist `dist/` directory for wheel/sdist files