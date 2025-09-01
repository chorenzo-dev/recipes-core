# CI/CD Pipeline Implementation

## Directory Structure

Create the CI/CD configuration directory based on your platform:
- GitHub Actions: `.github/workflows/`
- GitLab CI: Root directory (`.gitlab-ci.yml`)
- CircleCI: `.circleci/`

## Basic Pipeline Configuration

### 1. Create Build Pipeline File

Name your build pipeline file:
- `build.yml` or `build.yaml` for GitHub Actions
- Include `build:` stage in `.gitlab-ci.yml` for GitLab
- Include `build` job in `config.yml` for CircleCI

### 2. Define Build Steps

Configure these universal build steps:
```
1. Checkout code
2. Set up runtime environment (Node.js, Python, etc.)
3. Install dependencies
4. Run formatting check
5. Run linting
6. Run type checking (if applicable)  
7. Build/compile project
```

### 3. Create Test Pipeline File

Name your test pipeline file:
- `test.yml` or `test.yaml` for GitHub Actions
- Include `test:` stage in `.gitlab-ci.yml` for GitLab
- Include `test` job in `config.yml` for CircleCI

### 4. Define Test Steps

Configure these universal test steps:
```
1. Checkout code
2. Set up runtime environment
3. Install dependencies
4. Run unit tests
5. Run integration tests (if applicable)
6. Generate coverage report
7. Upload test artifacts
```

### 5. Configure Triggers

Set up pipeline triggers for:
- Push to main/master branch
- Pull request events
- Tag pushes (for releases)
- Manual triggers (workflow_dispatch or manual jobs)

### 6. Set Up Caching

Configure dependency caching:
- Cache package manager directories (node_modules, .pip, etc.)
- Use lock file checksums as cache keys
- Set appropriate cache expiration policies

### 7. Configure Change Detection

For monorepos, implement change detection:
- Define path filters for each package/module
- Use platform-specific change detection features
- Skip jobs when no relevant files changed

### 8. Update Project Analysis

After pipeline creation, update `analysis.json`:
```json
{
  "ci_cd": {
    "platform": "[github-actions|gitlab-ci|circleci]",
    "has_build_pipeline": true,
    "has_test_pipeline": true
  }
}