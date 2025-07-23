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

For modern ESLint flat config (ESLint 9+), also install:

```bash
npm install --save-dev @eslint/js globals
```

## Configuration

Create an `eslint.config.mjs` file in the project root using the modern flat config format.

**Configuration guidelines:**

- **Extend recommended configurations**: Use `@eslint/js` recommended config as the base
- **For TypeScript projects**: Also extend `@typescript-eslint/recommended` configuration
- **File targeting**:
  - Apply TypeScript rules to `**/*.ts` and `**/*.tsx` files
  - Apply JavaScript rules to `**/*.js` and `**/*.cjs` files
- **Common ignore patterns**: Include `dist/**`, `build/**`, `node_modules/**`, and `**/*.generated.*` in the ignores array
- **Language options**: Set `ecmaVersion: 'latest'` and appropriate `sourceType` (module/commonjs)
- **Globals**: Include Node.js and ES2022 globals as needed

**Note**: ESLint automatically ignores `node_modules/` and `.git/` directories. Additional ignore patterns are specified in the `ignores` array within the configuration file. The `.eslintignore` file is deprecated in ESLint 9+ flat config.

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