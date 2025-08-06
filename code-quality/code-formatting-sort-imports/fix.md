# Setting up Import Sorting

## Overview

Configure automatic import sorting to organize imports in a consistent order as part of the code formatting workflow. Import sorting ensures imports follow a predictable pattern: external libraries first, then internal modules, and finally relative imports.

## Configuration Approach

1. **Integrate with existing formatter**: Add import sorting to your current code formatter configuration rather than using a separate tool when possible.

2. **Define import groups**: Configure the tool to recognize and separate different types of imports:
   - External library imports (third-party packages)
   - Internal/aliased imports (project-specific modules)
   - Relative imports (local file references)

3. **Enable group separation**: Configure blank lines between import groups for better readability.

## Integration Steps

1. Install the appropriate import sorting tool or plugin for your ecosystem.

2. Add import sorting configuration to your formatter's configuration file.

3. Update your format command to include import sorting if needed.

4. Verify the integration by running your standard format command.

## Verification

After configuration, run your project's format command and confirm that:
- Imports are grouped by type (external, internal, relative)
- Each group is alphabetically sorted
- Groups are separated by blank lines
- The formatting integrates seamlessly with your existing workflow