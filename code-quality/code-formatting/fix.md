# Code Formatting Setup

## Installation

Check if the formatter is already installed using the tool's version command or by checking project dependencies.

If not found, install the formatter as a development dependency using the project's package manager, ensuring installation occurs in the project's virtual environment if one exists.

## Configuration

Create or update the appropriate configuration file in the project root with minimal, sensible defaults.

The formatter should automatically respect `.gitignore` for file exclusions. Only create additional ignore files or exclusion rules for files that aren't already gitignored but shouldn't be formatted (such as lock files, generated files, or legacy code that must preserve its formatting).

## Scripts

Add formatting commands to the project's script system (package.json, Makefile, etc.) that provide:
- A format command to apply formatting to all files
- A format:check command to verify all files are properly formatted

## Verification

Apply formatting to all files using the format command, then verify all files are properly formatted using the format:check command.