# Setting up GitHub Actions Build Checks for Python

## Installation

Create or update the GitHub Actions workflow file at `.github/workflows/ci.yml`:

```yaml
name: CI

on:
  pull_request:
    branches: [main, master]
  push:
    branches: [main, master]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: ['3.8', '3.9', '3.10', '3.11']
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
        
      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python-version }}
          
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          if [ -f requirements.txt ]; then
            pip install -r requirements.txt
          elif [ -f pyproject.toml ]; then
            pip install -e .
          fi
          
      - name: Type check
        if: hashFiles('pyproject.toml') != '' || hashFiles('mypy.ini') != ''
        run: |
          if command -v mypy &> /dev/null; then
            mypy .
          else
            echo "mypy not found, skipping type check"
          fi
          
      - name: Lint
        run: |
          if command -v flake8 &> /dev/null; then
            flake8 .
          elif command -v pylint &> /dev/null; then
            pylint **/*.py
          elif command -v ruff &> /dev/null; then
            ruff check .
          fi
          
      - name: Format check
        run: |
          if command -v black &> /dev/null; then
            black --check .
          fi
          
      - name: Test
        run: |
          if command -v pytest &> /dev/null; then
            pytest
          elif command -v python &> /dev/null && find . -name "*test*.py" | head -1; then
            python -m unittest discover
          fi
          
      - name: Build
        if: hashFiles('setup.py') != '' || hashFiles('pyproject.toml') != ''
        run: |
          pip install build
          python -m build
```

## Configuration

For projects with specific requirements, add environment setup:

```yaml
- name: Install system dependencies
  run: |
    sudo apt-get update
    sudo apt-get install -y libpq-dev

- name: Set up environment variables
  run: |
    echo "DATABASE_URL=sqlite:///test.db" >> $GITHUB_ENV
    echo "SECRET_KEY=test-key" >> $GITHUB_ENV
```

## Verification

Push changes and verify the workflow runs successfully:
- Check Actions tab in GitHub repository
- Confirm all Python versions pass
- Verify all quality checks complete successfully