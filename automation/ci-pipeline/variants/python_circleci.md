## Python + CircleCI Specifics

### File Structure
- Create `.circleci/config.yml` file in repository root
- Define workflows with build and test jobs

### Environment Setup
- Detect Python version from `pyproject.toml`, `.python-version`, `runtime.txt`, or use current stable version if not specified
- Use Python Docker image: `cimg/python:${detected_version}`
- Install Python orb for convenience: `circleci/python@2.0.3`

### Change Detection
- Use `CIRCLE_COMPARE_URL` for commit range detection
- Parse commit range and run git diff for Python file changes
- Include Python extensions and dependency files
- Use workspace persistence to share results

### Job Configuration
- Use `circleci step halt` to skip jobs when no changes detected
- Configure workspace attachment for sharing data between jobs
- Set up proper job dependencies with `requires`

### Python Commands
- Install: Use Python orb `python/install-packages` or `pip install -r requirements.txt`
- Build: `python -m build`, package validation commands
- Format: `black --check .`, `isort --check-only .`
- Lint: `flake8 .`, `pylint **/*.py`
- Type check: `mypy .`
- Test: `pytest --cov=. --cov-report=xml`

### Artifacts & Reports
- Store test results: `store_test_results` 
- Store coverage artifacts: `store_artifacts` with coverage files
- Persist build outputs to workspace for deployment

### Analysis Update
- After creating `.circleci/config.yml`, update `.chorenzo/analysis.json`
- Set the workspace-level `ciCd` field to `"circleci"`
- If the file doesn't exist, create it with minimal structure including the `ciCd` field