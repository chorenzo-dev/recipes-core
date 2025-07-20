# Setting up Prettier for JavaScript/TypeScript

## Installation

Install Prettier as a development dependency:

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

Run the formatter to verify it's working:

```bash
npm run format
```

Check if all files are formatted correctly:

```bash
npm run format:check
```