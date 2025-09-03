## Goal

Add a GitHub Actions workflow to automatically scan for exposed API keys, passwords, tokens, and other sensitive information in the repository on every push and pull request.

## Investigation

1. **Check for existing secret scanning in GitHub Actions**
   - Look in `.github/workflows/` for existing security or gitleaks workflows
   - Check if secret scanning is already configured in other workflow files
   - Verify GitHub Actions is already set up (required dependency)

2. **Assess current .gitignore coverage**
   - Check if common secret file patterns are already ignored (.env, *.key, *.pem)
   - Identify any obvious secret files that should be excluded

3. **Check for existing gitleaks configuration**
   - Look for `.gitleaks.toml` custom configuration file
   - Check if any custom secret patterns are needed for this specific project

## Expected Output

This recipe relies on the automatic `secret-scanner.applied` field to indicate successful configuration.