# Setting up Husky and lint-staged for JavaScript/TypeScript

## Prerequisites Check

Before setting up pre-commit hooks, verify that type checking, code formatting, or code linting scripts exist in `package.json`. Do not proceed if no relevant scripts are found.

Required scripts (at least one must exist):
- Type checking: `typecheck`, `type-check`, `tsc`, `check-types`
- Formatting: `format`, `format:fix`, `prettier`, `fmt`
- Linting: `lint`, `lint:fix`, `eslint`, `eslint:fix`

## Installation

Check if Husky and lint-staged are already installed:

```bash
npm list husky lint-staged
```

If not found, install as development dependencies:

```bash
npm install --save-dev husky lint-staged
```

## Husky Setup

Initialize Husky:

```bash
npx husky init
```

This creates `.husky/` directory and adds a prepare script to `package.json`.

## lint-staged Configuration

Add lint-staged configuration to `package.json` based on available scripts. Only include commands that exist in the project's scripts.

Example configuration structure:
```json
{
  "lint-staged": {
    "*.{js,jsx,ts,tsx}": [
      // Add commands based on available scripts
    ],
    "*.{json,md,yml,yaml}": [
      // Add formatting commands if available
    ]
  }
}
```

Configure based on which scripts are available:
- For type checking: Add `"npm run typecheck"` if `typecheck`, `type-check`, `tsc`, or `check-types` script exists
- For linting: Add `"npm run lint:fix"` if available, otherwise `"npm run lint"` or `"npm run eslint"`
- For formatting: Add `"npm run format"` if available, otherwise `"npm run prettier"` if available
- Only include file patterns that have corresponding available commands

## Pre-commit Hook

Create the pre-commit hook file:

```bash
echo 'npx lint-staged' > .husky/pre-commit
chmod +x .husky/pre-commit
```

## Verification

Test the setup by staging some files and attempting a commit:

```bash
git add .
git commit -m "test pre-commit hooks"
```

The hooks should run automatically and either pass or prevent the commit if issues are found.

## Troubleshooting

If hooks don't run:
- Ensure the `.husky/pre-commit` file is executable
- Verify that all referenced npm scripts exist in `package.json`
- Check that Husky is properly initialized with `npx husky init`