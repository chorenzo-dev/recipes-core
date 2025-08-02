# Setting up GitHub Actions Build Checks for JavaScript

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
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
        
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'
          
      - name: Install dependencies
        run: npm ci
        
      - name: Type check
        if: hashFiles('tsconfig.json') != ''
        run: npm run typecheck
        
      - name: Lint
        run: npm run lint
        
      - name: Build
        if: hashFiles('package.json') != '' && contains(fromJson('["build", "build:prod"]'), steps.check-scripts.outputs.build-script)
        run: npm run build
        
      - name: Test
        if: hashFiles('package.json') != '' && contains(fromJson('["test", "test:ci"]'), steps.check-scripts.outputs.test-script)
        run: npm test
        
      - name: Check scripts
        id: check-scripts
        run: |
          if jq -e '.scripts.build' package.json > /dev/null; then
            echo "build-script=build" >> $GITHUB_OUTPUT
          elif jq -e '.scripts["build:prod"]' package.json > /dev/null; then
            echo "build-script=build:prod" >> $GITHUB_OUTPUT
          fi
          
          if jq -e '.scripts.test' package.json > /dev/null; then
            echo "test-script=test" >> $GITHUB_OUTPUT
          elif jq -e '.scripts["test:ci"]' package.json > /dev/null; then
            echo "test-script=test:ci" >> $GITHUB_OUTPUT
          fi
```

## Configuration

For monorepo projects, add matrix strategy to run checks for each project:

```yaml
strategy:
  matrix:
    project: [frontend, backend, shared]
    
steps:
  - name: Install dependencies
    working-directory: ${{ matrix.project }}
    run: npm ci
```

## Verification

Push changes and verify the workflow runs successfully:
- Check Actions tab in GitHub repository
- Confirm all enabled checks pass
- Verify workflow triggers on pull requests