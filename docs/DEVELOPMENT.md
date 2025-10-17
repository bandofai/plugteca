# Development Guide

Guide for developing and testing plugins locally for Plugteca.

## Setup

### Clone the Repository

```bash
git clone https://github.com/username/plugteca.git
cd plugteca
```

### Install Dependencies

```bash
npm install
```

## Creating a New Plugin

### 1. Create Plugin Directory

```bash
mkdir -p plugins/your-plugin-name/.claude-plugin
```

### 2. Create Plugin Manifest

Create `plugins/your-plugin-name/.claude-plugin/plugin.json`:

```json
{
  "name": "your-plugin-name",
  "version": "1.0.0",
  "description": "What your plugin does",
  "author": "Your Name"
}
```

### 3. Add Plugin Components

Add any combination of:

**Commands** (`commands/*.md`):
```bash
mkdir plugins/your-plugin-name/commands
```

**Agents** (`agents/*.md`):
```bash
mkdir plugins/your-plugin-name/agents
```

**Skills** (`skills/*/SKILL.md`):
```bash
mkdir -p plugins/your-plugin-name/skills/skill-name
```

**Hooks** (`hooks/hooks.json`):
```bash
mkdir plugins/your-plugin-name/hooks
```

### 4. Create README

Create `plugins/your-plugin-name/README.md` documenting your plugin.

## Development Workflow

### 1. Validate Plugin Structure

```bash
npm run validate plugins/your-plugin-name
```

This checks:
- Directory structure is correct
- Required files exist (`.claude-plugin/plugin.json`)
- JSON is valid
- Naming conventions are followed
- Recommended files present (README.md)

### 2. Generate Catalog

After adding or modifying plugins:

```bash
npm run generate-catalog
```

This scans `plugins/` and updates `.claude-plugin/marketplace.json`.

### 3. Test Locally

Add your local Plugteca as a marketplace:

```bash
/plugin marketplace add /path/to/plugteca
```

Install your plugin:

```bash
/plugin install your-plugin-name@plugteca
```

Test all functionality:
- Try all commands
- Test agents with various inputs
- Verify skills are invoked correctly
- Check hooks trigger as expected

### 4. Iterate

To test changes:

```bash
# Uninstall the plugin
/plugin uninstall your-plugin-name

# Regenerate catalog if manifest changed
npm run generate-catalog

# Reinstall
/plugin install your-plugin-name@plugteca
```

## Testing Best Practices

### Command Testing

Create test scenarios for each command:

```bash
# Test basic usage
/your-command

# Test with parameters
/your-command --option value

# Test edge cases
/your-command --edge-case

# Test error handling
/your-command --invalid
```

### Agent Testing

Test agents with:
- Simple tasks
- Complex multi-step tasks
- Edge cases
- Error conditions

### Skills Testing

Verify skills:
- Are invoked automatically when appropriate
- Don't interfere with normal operations
- Handle errors gracefully

### Hooks Testing

Test hooks in real workflows:
- Pre/post commit
- Tool execution
- Session events

## Debugging

### Plugin Not Found

1. Check `.claude-plugin/marketplace.json` includes your plugin
2. Verify marketplace path is correct
3. Regenerate catalog: `npm run generate-catalog`

### Plugin Installation Fails

1. Run validation: `npm run validate plugins/your-plugin-name`
2. Check `plugin.json` syntax
3. Verify all referenced files exist

### Commands Not Working

1. Check command file syntax (valid Markdown)
2. Verify file is in `commands/` directory
3. Check command name matches filename

### Agents Not Behaving Correctly

1. Review agent instructions for clarity
2. Test with simpler inputs first
3. Check for conflicts with built-in agents

## Scripts Reference

### validate

Validates a single plugin:

```bash
npm run validate plugins/plugin-name
```

Checks:
- Directory structure
- Required files
- JSON validity
- Naming conventions

### generate-catalog

Generates marketplace catalog:

```bash
npm run generate-catalog
```

Scans `plugins/` and creates/updates `.claude-plugin/marketplace.json`.

### validate-all

Validates all plugins:

```bash
npm run validate-all
```

Useful before committing to ensure all plugins are valid.

## Git Workflow

### 1. Create Branch

```bash
git checkout -b add-plugin-name
```

### 2. Add Plugin

Create plugin following the structure above.

### 3. Validate

```bash
npm run validate plugins/your-plugin-name
npm run generate-catalog
```

### 4. Commit

```bash
git add plugins/your-plugin-name
git add .claude-plugin/marketplace.json
git commit -m "feat: add your-plugin-name plugin"
```

### 5. Push

```bash
git push origin add-plugin-name
```

### 6. Test in Production

After merge, the GitHub Action will automatically update the catalog.

## Automated Catalog Updates

The repository includes a GitHub Action that:
1. Triggers on pushes to `main` that modify `plugins/`
2. Runs `generate-catalog.js`
3. Commits updated `marketplace.json` if changed

See `.github/workflows/update-catalog.yml` for details.

## Directory Structure Reference

```
plugteca/
├── .claude-plugin/
│   └── marketplace.json              # Auto-generated, don't edit manually
│
├── plugins/                          # Your plugins here
│   └── your-plugin/
│       ├── .claude-plugin/
│       │   └── plugin.json          # Required
│       ├── commands/                 # Optional
│       ├── agents/                   # Optional
│       ├── skills/                   # Optional
│       ├── hooks/                    # Optional
│       └── README.md                 # Required
│
├── scripts/
│   ├── validate-plugin.js           # Validation logic
│   └── generate-catalog.js          # Catalog generation
│
├── docs/
│   ├── INSTALLATION.md              # User installation guide
│   ├── PLUGIN_GUIDELINES.md         # Plugin standards
│   └── DEVELOPMENT.md               # This file
│
├── .github/
│   └── workflows/
│       └── update-catalog.yml       # Auto-catalog update
│
├── package.json                      # Scripts and dependencies
└── README.md                         # Main documentation
```

## Tips

- Keep plugins focused on a single purpose
- Write clear documentation
- Test thoroughly before committing
- Use semantic versioning
- Follow the guidelines in [PLUGIN_GUIDELINES.md](./PLUGIN_GUIDELINES.md)

## Getting Help

- Check [PLUGIN_GUIDELINES.md](./PLUGIN_GUIDELINES.md) for standards
- Review the example plugin in `plugins/example-formatter/`
- Read [Claude Code plugin documentation](https://docs.claude.com/en/docs/claude-code/plugins)
