## Python + GitHub Actions Specifics

### File Structure
- Create `.github/workflows/` directory for workflow files
- Use separate `build.yml` and `test.yml` workflow files

### Environment Setup
- Configure Python with `actions/setup-python@v4` action
- Use pip cache for faster dependency installation: `cache: 'pip'`
- Detect Python version from `pyproject.toml`, `.python-version`, `runtime.txt`, or use current stable version if not specified

### Change Detection
- Use `dorny/paths-filter@v2` action for efficient change detection
- Include Python extensions: `**/*.py`
- Include dependency files: `requirements*.txt`, `pyproject.toml`, `setup.py`, `Pipfile`

### Python Commands
- Install: `pip install -r requirements.txt` or `pip install -e .`
- Build: `python -m build` for packages, or validation commands
- Format: `black --check .`, `isort --check-only .`
- Lint: `flake8 .`, `pylint **/*.py`
- Type check: `mypy .`
- Test: `pytest`, `python -m pytest --cov=. --cov-report=xml`

### Monorepo Integration
- For Poetry monorepos: Use workspace dependencies and `poetry run` commands
- For setuptools monorepos: Use `pip install -e packages/*/` pattern
- Change detection per package with path filters

### Analysis Update
- After creating GitHub Actions workflows, update `.chorenzo/analysis.json`
- Set the workspace-level `ciCd` field to `"github_actions"`
- If the file doesn't exist, create it with minimal structure including the `ciCd` field