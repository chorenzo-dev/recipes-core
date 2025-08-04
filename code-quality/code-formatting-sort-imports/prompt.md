## Goal

Configure automatic import sorting as part of the code formatting workflow.

## Investigation

1. **Check existing formatter configuration**
   - Look for formatter configuration files (e.g., .prettierrc, pyproject.toml, setup.cfg)
   - Verify if import sorting is already enabled in the formatter configuration
   - Check if dedicated import sorting tools are configured separately

2. **Detect current import sorting setup**
   - Search for import sorting tool configuration files (e.g., .isort.cfg, import-sort configuration)
   - Check package.json or requirements files for import sorting dependencies
   - Look for import sorting rules in linter configurations

3. **Identify integration opportunities**
   - Check if the formatter supports built-in import sorting features
   - Verify compatibility between existing formatter and import sorting tools
   - Assess if import sorting can be integrated into the current formatting workflow

## Expected Output

This recipe does not provide any state variables as import sorting configuration is too specific for cross-recipe dependencies.
