## Goal

Configure workspace-level CI/CD pipelines with separate build and test workflows that optimize for monorepos by detecting changed files and running commands only for affected projects.

## Investigation

1. **Detect existing CI/CD configuration**
   - Check for .github/workflows/ directory and YAML files
   - Check for .gitlab-ci.yml file in workspace root
   - Check for .circleci/config.yml file
   - Check for any other CI/CD configuration files

2. **Analyze workspace structure**
   - Identify if workspace is a monorepo with multiple projects
   - List all package.json, setup.py, pyproject.toml, go.mod files to identify projects
   - Determine primary ecosystem and any mixed ecosystems

3. **Identify build and test commands**
   - Check package.json scripts for build, test, lint, typecheck commands
   - Check pyproject.toml, setup.py, tox.ini for Python build/test commands
   - Check Makefile, go.mod for Go build/test commands
   - Identify format checking, linting, and type checking tools in use

4. **Assess current CI/CD platform**
   - Check git remotes to determine if using GitHub, GitLab, or other platforms
   - Look for existing workflow files to understand current CI/CD setup
   - Identify any existing optimization strategies for monorepos

## Expected Output

- ci-pipeline.platform: The CI/CD platform being configured (github-actions, gitlab-ci, circleci)