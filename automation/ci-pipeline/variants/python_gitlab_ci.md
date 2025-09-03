## Python + GitLab CI Specifics

### GitLab CI Python Configuration
Use Python Docker image `python:${version}` based on `pyproject.toml`, `.python-version`, or `runtime.txt`. Define stages: `changes`, `build`, `test`.

### Python Cache Configuration
Configure cache with commit reference slug key and paths for pip cache and virtual environment directories.

### Python Change Detection
Detect Python changes using GitLab CI variables:
- Source: `**/*.py`
- Dependencies: `requirements*.txt`, `pyproject.toml`, `setup.py`, `Pipfile`
- Tests: `tests/**`, `**/test_*.py`

### GitLab Python Commands
- Virtual environment: `python -m venv venv && source venv/bin/activate`
- Dependency installation: `pip install -r requirements.txt`
- Package building: `python -m build`
- Formatting: `black --check .` and `isort --check-only .`
- Linting: `flake8 .` or `ruff check`
- Type checking: `mypy .`
- Testing: `pytest --cov=. --cov-report=xml --junitxml=report.xml`

### Python Coverage Integration
- Configure coverage regex: `/TOTAL.+?(\d+%)$/`
- Use cobertura format for GitLab coverage visualization
- Store test reports as JUnit XML