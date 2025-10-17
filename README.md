<p align="center">
  <img src="docs/logo.png" alt="Plugteca Logo" width="200"/>
</p>

<p align="center">
A curated marketplace of Claude Code plugins.
</p>

## What is Plugteca?

Plugteca is a Git repository-based marketplace for Claude Code plugins. It provides a simple, maintainable way to discover and install plugins that extend Claude Code's functionality with custom commands, agents, skills, and hooks.

## Installation

Add Plugteca as a marketplace in Claude Code:

```bash
/plugin marketplace add bandofai/plugteca
```

## Available Plugins

See the [plugins/](./plugins) directory for all available plugins, or browse the auto-generated catalog in [`.claude-plugin/marketplace.json`](./.claude-plugin/marketplace.json).

### Installing Plugins

Once you've added the marketplace, install any plugin with:

```bash
/plugin install <plugin-name>@plugteca
```

Example:
```bash
/plugin install essentials@plugteca
```

### List Available Plugins

```bash
/plugin list --marketplace plugteca
```

## Plugin Directory

<!-- This section will be populated as plugins are added -->

## Development

### Repository Structure

```
plugteca/
├── .claude-plugin/
│   └── marketplace.json          # Auto-generated catalog
├── plugins/                      # All plugins
│   └── example-plugin/
│       ├── .claude-plugin/
│       │   └── plugin.json       # Plugin manifest
│       ├── commands/             # Optional: slash commands
│       ├── agents/               # Optional: custom agents
│       ├── skills/               # Optional: agent skills
│       ├── hooks/                # Optional: event hooks
│       └── README.md
├── scripts/
│   ├── validate-plugin.js        # Validation script
│   └── generate-catalog.js       # Catalog generation
└── docs/                         # Documentation
```

### Adding Plugins

1. Create a new directory under `plugins/` with your plugin name
2. Add `.claude-plugin/plugin.json` with required metadata
3. Add plugin functionality (commands, agents, skills, hooks)
4. Add a README.md documenting the plugin
5. Run validation: `npm run validate <plugin-name>`
6. Generate catalog: `npm run generate-catalog`
7. Commit and push (GitHub Actions will auto-update the catalog)

### Plugin Structure

Each plugin must have a `plugin.json` manifest:

```json
{
  "name": "plugin-name",
  "version": "1.0.0",
  "description": "Brief description of the plugin",
  "author": {
    "name": "Your Name"
  }
}
```

See [docs/PLUGIN_GUIDELINES.md](./docs/PLUGIN_GUIDELINES.md) for detailed guidelines.

### Scripts

```bash
# Validate a plugin structure
npm run validate plugins/plugin-name

# Generate marketplace catalog
npm run generate-catalog

# Validate all plugins
npm run validate-all
```

## Documentation

- [Installation Guide](./docs/INSTALLATION.md) - Detailed setup instructions
- [Plugin Guidelines](./docs/PLUGIN_GUIDELINES.md) - Standards and best practices
- [Development Guide](./docs/DEVELOPMENT.md) - Local development workflow

## License

MIT License - See [LICENSE](./LICENSE) for details.
