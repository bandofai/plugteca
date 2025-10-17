# Installation Guide

This guide explains how to add Plugteca as a marketplace and install plugins.

## Prerequisites

- Claude Code installed and configured
- Git access to this repository

## Adding Plugteca Marketplace

### From GitHub

If this repository is hosted on GitHub:

```bash
/plugin marketplace add bandofai/plugteca
```

### From Local Path

For local development or testing:

```bash
/plugin marketplace add /path/to/plugteca
```

## Installing Plugins

Once the marketplace is added, you can install any plugin:

```bash
/plugin install <plugin-name>@plugteca
```

### Examples

```bash
# Install the example formatter plugin
/plugin install example-formatter@plugteca

# List all available plugins in Plugteca
/plugin list --marketplace plugteca

# Check installed plugins
/plugin list
```

## Uninstalling Plugins

To remove a plugin:

```bash
/plugin uninstall <plugin-name>
```

## Updating Plugins

To update a plugin to the latest version:

```bash
/plugin update <plugin-name>@plugteca
```

Or update all plugins:

```bash
/plugin update --all
```

## Removing the Marketplace

To remove Plugteca from your marketplaces:

```bash
/plugin marketplace remove plugteca
```

## Troubleshooting

### Marketplace Not Found

If you get an error that the marketplace cannot be found:

1. Check that the repository URL is correct
2. Ensure you have access to the repository
3. Verify `.claude-plugin/marketplace.json` exists in the repository

### Plugin Installation Fails

If a plugin fails to install:

1. Check that the plugin exists in the marketplace
2. Verify the plugin structure is correct using `npm run validate`
3. Check the plugin's README for specific requirements

### Cannot Access Private Repository

For private repositories:

1. Ensure you have proper Git credentials configured
2. Use SSH URL format if using SSH keys
3. Or use a personal access token with appropriate permissions

## Configuration

### Repository-Level Auto-Install

You can configure specific plugins to auto-install for a repository by adding to `.claude/settings.json`:

```json
{
  "plugins": {
    "autoInstall": [
      "plugin-name@plugteca"
    ]
  }
}
```

This ensures team members automatically get the required plugins when working on the project.

## Support

For issues with:
- **Plugteca marketplace**: Open an issue in this repository
- **Claude Code**: Visit [Claude Code documentation](https://docs.claude.com/en/docs/claude-code)
- **Specific plugins**: Check the plugin's README and documentation
