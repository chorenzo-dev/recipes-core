# Setting up ESLint for JavaScript/TypeScript

## Installation

Check if ESLint is already installed:

```bash
npm list eslint
```

If not found, install ESLint as a development dependency:

```bash
npm install --save-dev eslint
```

For TypeScript projects, also install:

```bash
npm install --save-dev @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

## Configuration

Create an `.eslintrc.js` file in the project root:

```javascript
module.exports = {
  extends: ['eslint:recommended'],
  env: {
    node: true,
    es2022: true
  },
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module'
  }
};
```

For TypeScript projects, use:

```javascript
module.exports = {
  extends: [
    'eslint:recommended',
    '@typescript-eslint/recommended'
  ],
  parser: '@typescript-eslint/parser',
  plugins: ['@typescript-eslint'],
  env: {
    node: true,
    es2022: true
  },
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module'
  }
};
```

ESLint automatically ignores files in `.gitignore`, `node_modules`, and version control directories.

Only create a `.eslintignore` file if there are files that aren't already gitignored but shouldn't be linted:

```
# Examples of files to exclude that might not be in .gitignore:
# - Generated files not in gitignore
*.generated.*

# - Files with legacy code that cannot be linted
legacy/

# - Build output that might not be in gitignore
dist/
build/
```

## Scripts

Add linting scripts to `package.json`:

```json
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint --fix ."
  }
}
```

## Verification

Run the linter to check for issues:

```bash
npm run lint
```

Fix automatically fixable issues:

```bash
npm run lint:fix
```