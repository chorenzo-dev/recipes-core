## Python + GitLab CI Specifics

### File Structure
- Create `.gitlab-ci.yml` file in repository root
- Define stages: changes, build, test

### Environment Setup
- Detect Python version from `pyproject.toml`, `.python-version`, `runtime.txt`, or use current stable version if not specified
- Use Python Docker image: `python:${detected_version}`
- Set PYTHON_VERSION variable for consistency
- Configure pip cache for efficient builds

### Change Detection Setup
- Create separate job to check for Python changes
- Use git diff with GitLab CI variables for change detection
- Include extensions: `.py`, dependency files like `requirements*.txt`, `pyproject.toml`

### Job Configuration
- Use `rules` with change detection variables to skip unnecessary jobs
- Configure cache for pip and virtual environments
- Set up proper job dependencies with `needs`

### Python Commands
- Install: `pip install -r requirements.txt` or `pip install -e .`
- Build: `python -m build`, `python setup.py build`
- Format: `black --check .`, `isort --check-only .`
- Lint: `flake8 .`, `pylint **/*.py`
- Type check: `mypy .`
- Test: `pytest --cov=. --cov-report=xml`

### Artifacts & Reports
- Store coverage reports with cobertura format
- Configure test artifacts for GitLab integration
- Set reasonable expire times for build artifacts

### Analysis Update
- After creating `.gitlab-ci.yml`, update `.chorenzo/analysis.json`
- Set the workspace-level `ciCd` field to `"gitlab_ci"`
- If the file doesn't exist, create it with minimal structure including the `ciCd` field