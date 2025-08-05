## Python + CircleCI Specifics

### File Structure
- Create `.circleci/config.yml` file in repository root
- Define workflows with build and test jobs

### Environment Setup
- Use Python Docker image: `cimg/python:3.11` or similar
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