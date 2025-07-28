# @chorenzo/recipes-core

Core recipes for the Chorenzo engine - atomic, composable automation recipes.

## Recipe Documentation

For complete documentation on recipe structure, file formats, design principles, and contributing guidelines, see:

**[Recipe Documentation](https://github.com/chorenzo-dev/engine/blob/main/docs/recipes.md)**

## Example Recipe

See `code-quality/code-formatting/` for a complete example implementing code formatter detection and setup.

## Contributing

1. Create a folder matching your recipe ID (kebab-case)
2. Add `metadata.yaml` with at least: id, summary, ecosystems, provides
3. Write `prompt.md` with Goal, Investigation, and Expected Output sections
4. Add variant-specific fix prompts under `fixes/`
5. Ensure all paths in metadata.yaml match actual file locations

## Open Issues

- Recipe validation CLI (`chorenzo recipes lint`) to be implemented in the main CLI repository