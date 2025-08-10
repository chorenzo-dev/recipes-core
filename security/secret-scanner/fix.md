# Add Secret Scanner GitHub Action

## GitHub Actions Workflow

Create `.github/workflows/security.yml` with a workflow that uses the official gitleaks-action on push and pull requests to main/master branches. The workflow should checkout with full history (`fetch-depth: 0`) and run gitleaks/gitleaks-action@v2 with the GITHUB_TOKEN environment variable.

## Update .gitignore

Add patterns to prevent accidental commits of common secret files: `.env*` files, `*.pem`, `*.key`, and configuration files that may contain secrets like `config/secrets.yml`.

## Verification

Push code to trigger the workflow. The secret scanner will run automatically on all pushes and pull requests to protected branches. If secrets are detected, the workflow will fail and prevent the merge, protecting the codebase from exposed credentials.