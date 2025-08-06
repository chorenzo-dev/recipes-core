# Setting up Husky and lint-staged for JavaScript/TypeScript

## Prerequisites Check

Verify that type checking, code formatting, or code linting scripts exist in package.json. Look for scripts named: typecheck, type-check, tsc, check-types, format, format:fix, prettier, fmt, lint, lint:fix, eslint, or eslint:fix.

Do not proceed if no relevant scripts are found.

## Installation

Check if Husky and lint-staged are already installed: `npm list husky lint-staged`

If not found, install as development dependencies: `npm install --save-dev husky lint-staged`

## Husky Setup

Initialize Husky: `npx husky init`

This creates .husky/ directory and adds a prepare script to package.json.

## lint-staged Configuration

Create a lint-staged configuration file: `touch .lintstagedrc.json`

Edit .lintstagedrc.json to define which commands run on which files. Structure the configuration to run available scripts in order: type checking first, linting second, formatting last. Only include commands that exist in your package.json scripts.

## Pre-commit Hook

Create the pre-commit hook file: `echo 'npx lint-staged' > .husky/pre-commit`

Make the hook executable: `chmod +x .husky/pre-commit`

## Verification

The setup is complete. Test by staging files and committing. The hooks will run automatically and either pass or prevent the commit if issues are found.

## Troubleshooting

If hooks don't run, ensure .husky/pre-commit file is executable. Verify that all referenced npm scripts exist in package.json. Check that Husky is properly initialized.