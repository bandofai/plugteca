<div style="text-align: center">
  <img src="docs/logo.png" alt="Plugteca Logo" width="200"/>
</div>
<p style="text-align: center">
  A curated marketplace of Claude Code plugins.
</p>

## What is Claude Code Plugin?

Claude Code plugins extend Claude's capabilities with custom commands, agents, skills, hooks, and MCP servers. They allow you to add specialized functionality to your Claude Code environment, from semantic code navigation to external tool integrations, making your development workflow more powerful and tailored to your needs. Learn more in the [official documentation](https://docs.claude.com/en/docs/claude-code/plugins).

## Installation

Plugteca supports two installation modes: **global** (available in all projects) and **local** (project-specific).

### Global Installation

Add Plugteca marketplace globally:

```bash
/plugin marketplace add bandofai/plugteca
```

Install a plugin globally:

```bash
/plugin install essentials@plugteca
```

This makes the plugin available across all your projects.

### Local Installation (Project-Specific)

For team projects or to limit plugins to specific repositories, use local configuration:

1. Create `.claude/settings.json` in your project root:

```json
{
  "marketplaces": [
    {
      "name": "plugteca",
      "url": "https://github.com/bandofai/plugteca"
    }
  ],
  "plugins": [
    {
      "name": "essentials",
      "marketplace": "plugteca"
    }
  ]
}
```

2. Team members who "trust" this folder will automatically have these plugins installed **only for this project**.

**Benefits:**
- Project-specific plugin configuration
- Automatic installation for team members
- No global plugin pollution
- Version control friendly

Learn more in the [official plugin documentation](https://docs.claude.com/en/docs/claude-code/plugins).

## Available Plugins

### Essentials

Essential MCP servers and requirements management commands for enhanced Claude Code development workflow.

#### MCP Servers

- **Serena** - Semantic code navigation with LSP-powered symbol search and editing
- **Context7** - Up-to-date documentation and code examples from current sources
- **Sequential Thinking** - Structured step-by-step problem-solving and reasoning

#### Commands

**Core Workflow:**
- `/brainstorm <name>` - Create requirement through interactive Q&A
- `/implement <name>` - Implement a requirement systematically
- `/continue [name]` - Resume interrupted implementation

**Management:**
- `/req-list` - Show all requirements with status
- `/req-update <name>` - Modify existing requirement
- `/req-tests <name>` - Generate test scenarios
- `/req-status [name]` - Check implementation progress

**Installation:**
```bash
/plugin install essentials@plugteca
```

**Prerequisites:**
- `uv` package manager ([install guide](https://docs.astral.sh/uv/getting-started/installation/))
- Node.js >= v18.0.0

After installing, restart Claude Code to activate the MCP servers.

---

### Chrome DevTools

Control and inspect Chrome browsers with full DevTools automation, debugging, and performance analysis.

#### MCP Servers

- **Chrome DevTools MCP** - 26+ tools for browser automation, input control, navigation, performance analysis, network monitoring, and debugging

**Installation:**
```bash
/plugin install chrome-devtools@plugteca
```

**Prerequisites:**
- Node.js >= v20.19
- Chrome browser (stable or newer)

After installing, restart Claude Code to activate the MCP server.

---

### Figma

Generate code from Figma designs, extract components, variables, and maintain design-code consistency.

#### MCP Servers

- **Figma MCP** - Remote HTTP server for design-to-code generation, component extraction, and design context retrieval

**Installation:**
```bash
/plugin install figma@plugteca
```

**Prerequisites:**
- Dev or Full seat on Professional, Organization, or Enterprise Figma plan
- OAuth authentication (setup via `/mcp` command after installation)

**Authentication:** After installation, type `/mcp`, select **figma**, and choose **Authenticate**.

After installing, restart Claude Code to activate the MCP server.

## License

MIT License
