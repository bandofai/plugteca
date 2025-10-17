# Plugin Guidelines

Standards and best practices for creating high-quality Plugteca plugins.

## Plugin Structure

Every plugin must follow this structure:

```
plugin-name/
├── .claude-plugin/
│   └── plugin.json          # REQUIRED: Plugin manifest
├── commands/                # OPTIONAL: Slash commands
│   └── command-name.md
├── agents/                  # OPTIONAL: Custom agents
│   └── agent-name.md
├── skills/                  # OPTIONAL: Agent skills
│   └── skill-name/
│       └── SKILL.md
├── hooks/                   # OPTIONAL: Event hooks
│   └── hooks.json
└── README.md                # REQUIRED: Documentation
```

## Plugin Manifest (plugin.json)

The manifest must include these required fields:

```json
{
  "name": "plugin-name",
  "version": "1.0.0",
  "description": "Brief, clear description of what the plugin does",
  "author": "Your Name or Organization"
}
```

### Naming Conventions

- **name**: Lowercase, alphanumeric, hyphens only (e.g., `code-formatter`, `git-utils`)
- **version**: Semantic versioning (MAJOR.MINOR.PATCH)
- Keep names concise but descriptive

### Optional Fields

```json
{
  "name": "plugin-name",
  "version": "1.0.0",
  "description": "Plugin description",
  "author": "Your Name",
  "repository": "https://github.com/username/plugin-repo",
  "license": "MIT",
  "keywords": ["formatting", "code-quality"],
  "dependencies": {
    "other-plugin": "^1.0.0"
  }
}
```

## README Documentation

Every plugin must include a comprehensive README.md with:

1. **Title and Description**: Clear explanation of what the plugin does
2. **Installation**: How to install the plugin
3. **Usage**: Examples of how to use commands, agents, or skills
4. **Configuration**: Any required setup or settings
5. **Examples**: Real-world usage examples
6. **Troubleshooting**: Common issues and solutions
7. **License**: License information

### README Template

```markdown
# Plugin Name

Brief description of what the plugin does.

## Installation

\`\`\`bash
/plugin install plugin-name@plugteca
\`\`\`

## Features

- Feature 1
- Feature 2
- Feature 3

## Usage

### Commands

\`\`\`bash
/command-name [arguments]
\`\`\`

### Agents

Description of custom agents and how they work.

### Skills

Description of skills and when they're invoked.

## Configuration

Any configuration steps needed.

## Examples

Practical examples showing the plugin in action.

## Troubleshooting

Common issues and how to resolve them.

## License

MIT License - see LICENSE file
```

## Components

### Commands

Slash commands are defined as Markdown files in `commands/`:

```markdown
# Description (shown in /plugin list)

Brief description of what this command does

# Instructions

Detailed instructions for Claude on how to execute this command.
Include parameters, expected behavior, and output format.
```

**Best Practices:**
- Use clear, descriptive command names
- Document all parameters
- Provide usage examples
- Keep commands focused on a single task

### Agents

Custom agents in `agents/` extend Claude's capabilities:

```markdown
# Agent Name

## Description
What this agent does and when to use it

## Capabilities
- Capability 1
- Capability 2

## Instructions
Detailed instructions for the agent's behavior
```

### Skills

Skills in `skills/*/SKILL.md` allow autonomous invocation:

```
skills/
└── skill-name/
    └── SKILL.md
```

**SKILL.md Structure:**
- Clear description of when to use the skill
- What the skill can do
- Instructions for execution

### Hooks

Event handlers in `hooks/hooks.json`:

```json
{
  "pre-commit": "echo 'Running pre-commit validation'",
  "post-tool": "echo 'Tool execution complete'"
}
```

## Quality Standards

### Code Quality

- Validate all JSON files are properly formatted
- Test commands and agents before publishing
- Ensure hooks don't break workflows
- Handle errors gracefully

### Documentation

- Write clear, concise descriptions
- Include practical examples
- Document all parameters and options
- Keep documentation up-to-date with code

### Versioning

Follow semantic versioning:
- **MAJOR**: Breaking changes
- **MINOR**: New features (backward compatible)
- **PATCH**: Bug fixes

### Testing

Before adding a plugin:

1. Validate structure: `npm run validate plugins/plugin-name`
2. Test installation locally
3. Test all commands and features
4. Verify documentation accuracy
5. Check for conflicts with common plugins

## Security

- Never include sensitive data (API keys, credentials)
- Avoid executing arbitrary code without user consent
- Validate all inputs in commands
- Document any external dependencies
- Be transparent about data usage

## Performance

- Keep plugins lightweight
- Avoid unnecessary dependencies
- Optimize command execution
- Don't abuse hooks (they run on every event)

## Maintenance

- Respond to issues and questions
- Keep dependencies updated
- Fix bugs promptly
- Maintain backward compatibility when possible

## Examples

See [`plugins/example-formatter/`](../plugins/example-formatter/) for a complete, well-structured example plugin.

## Validation

Run validation before committing:

```bash
npm run validate plugins/your-plugin-name
```

This checks:
- Directory structure
- Required files exist
- plugin.json format and required fields
- Naming conventions
- JSON syntax

## License

Plugins should include clear license information. MIT is recommended for maximum compatibility.
