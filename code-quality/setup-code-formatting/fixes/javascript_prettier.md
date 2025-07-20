# Setting up Prettier for JavaScript/TypeScript

## Installation

Check if Prettier is already installed:

```bash
npm list prettier
```

If not found, install Prettier as a development dependency:

```bash
npm install --save-dev prettier
```

## Configuration

Create a `.prettierrc` file in the project root:

```json
{
  "singleQuote": true
}
```

Prettier automatically ignores files in `.gitignore`, `node_modules`, and version control directories.

Only create a `.prettierignore` file if there are files that aren't already gitignored but shouldn't be formatted:

```
# Examples of files to exclude that might not be in .gitignore:
# - Lock files (to preserve their formatting)
package-lock.json
yarn.lock
pnpm-lock.yaml

# - Generated files not in gitignore
*.generated.*

# - Files with legacy formatting that must be preserved
legacy/
```

## Scripts

Add formatting scripts to `package.json`:

```json
{
  "scripts": {
    "format": "prettier --write .",
    "format:check": "prettier --check ."
  }
}
```

## Verification

Check if all files are formatted correctly (without modifying them):

```bash
npm run format:check
```

This command will:
- Exit with code 0 if all files are properly formatted
- Exit with code 1 and list unformatted files if formatting is needed