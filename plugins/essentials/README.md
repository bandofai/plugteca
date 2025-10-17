# Essentials Plugin

A collection of essential MCP servers that enhance Claude Code with powerful semantic code navigation, up-to-date documentation, and structured reasoning capabilities.

## Installation

```bash
/plugin install essentials@plugteca
```

## What's Included

This plugin bundles three powerful MCP servers:

### 1. Serena - Semantic Code Navigation

Provides IDE-like semantic code analysis and navigation using Language Server Protocol (LSP).

**Key Features:**
- Symbol-level code understanding (`find_symbol`, `find_referencing_symbols`)
- Precise code editing with `insert_after_symbol`
- Multi-language support: Python, TypeScript/JavaScript, PHP, Go, Rust, C/C++, Java, Ruby, and 15+ others
- Eliminates the need to read entire files or perform error-prone string replacements

**What it enables:**
- "Find all references to the `UserAuth` class"
- "Insert this code after the `validateUser` function"
- "Navigate to the definition of `processPayment`"

### 2. Context7 - Current Documentation

Fetches up-to-date, version-specific code documentation and examples directly from source repositories.

**Key Features:**
- Current API documentation (eliminates outdated training data)
- Real code examples from actual repositories
- Works without API key (basic rate limits apply)
- Optional API key for higher limits and private repositories

**What it enables:**
- "Show me the latest Next.js 15 app router examples"
- "Get current React 19 hook documentation"
- "Find up-to-date FastAPI security patterns"

### 3. Sequential Thinking - Structured Reasoning

Enables step-by-step problem decomposition and dynamic reasoning.

**Key Features:**
- Break down complex problems into manageable steps
- Revise and refine thinking as understanding deepens
- Explore alternative reasoning paths
- Adjust analysis scope dynamically

**What it enables:**
- "Think through this architecture decision step by step"
- "Analyze this bug systematically"
- "Plan the implementation with careful reasoning"

## Prerequisites

### Required Dependencies

**For Serena:**
- `uv` package manager ([installation guide](https://docs.astral.sh/uv/getting-started/installation/))
- Python 3.8+
- Language servers auto-install for most languages
- Some languages require manual setup:
  - Go: `go install golang.org/x/tools/gopls@latest`
  - Rust: `rustup component add rust-analyzer`

**For Context7:**
- Node.js >= v18.0.0
- No API key required (optional for higher limits)

**For Sequential Thinking:**
- Node.js >= v18.0.0

### Quick Setup

1. Install uv:
```bash
# macOS/Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"

# Or via pip
pip install uv
```

2. Ensure Node.js is installed:
```bash
node --version  # Should be >= v18.0.0
```

## Usage

Once installed, all three MCP servers are automatically available in Claude Code.

### Serena Examples

```
"Find all references to the authenticate function"
"Show me the definition of UserController"
"Insert this logging code after the handleRequest method"
```

### Context7 Examples

```
"Get the latest documentation for Prisma 5.x migrations"
"Show me current examples of using shadcn/ui components"
"Find up-to-date examples of Next.js Server Actions"
```

### Sequential Thinking Examples

```
"Think through this refactoring step by step"
"Analyze why this test is failing using systematic reasoning"
"Plan the database migration carefully with all considerations"
```

## Configuration

### Basic Configuration (Default)

The plugin works out of the box with sensible defaults. No additional configuration needed.

### Optional: Context7 API Key

For higher rate limits and private repository access:

1. Get an API key from [Context7](https://context7.com)
2. Set environment variable:
```bash
export CONTEXT7_API_KEY=your_api_key_here
```

3. Restart Claude Code

### Optional: Serena Custom Configuration

Create `~/.serena/serena_config.yml` for global settings:

```yaml
contexts:
  ide-assistant:
    enabled_tools:
      - find_symbol
      - find_referencing_symbols
      - insert_after_symbol
      - read_file_range
```

Project-specific settings are auto-generated in `.serena/project.yml`.

## Troubleshooting

### Serena Not Working

**Issue**: "uv: command not found"
- Install uv following the prerequisites above
- Restart your terminal/Claude Code

**Issue**: Language server not working for specific language
- Check if language server is installed
- See [Serena documentation](https://github.com/oraios/serena) for language-specific setup

### Context7 Rate Limits

**Issue**: "Rate limit exceeded"
- Add a Context7 API key (see Configuration section)
- Or wait a few minutes for the rate limit to reset

### Sequential Thinking Not Available

**Issue**: Tool not showing up
- Verify Node.js >= v18.0.0: `node --version`
- Reinstall the plugin: `/plugin uninstall essentials && /plugin install essentials@plugteca`

## What This Plugin Does Behind the Scenes

When you install this plugin, it:
1. Configures three MCP servers in your Claude Code environment
2. Makes their tools automatically available to Claude
3. Enables semantic code navigation, current documentation, and structured reasoning

The MCP servers run on-demand when Claude needs them - no background processes.

## Performance Notes

- **Serena**: First run may take a moment while language servers initialize
- **Context7**: Fetches documentation on-demand (network required)
- **Sequential Thinking**: Lightweight, no performance impact

## Links

- [Serena Repository](https://github.com/oraios/serena)
- [Context7 Repository](https://github.com/upstash/context7)
- [Sequential Thinking Repository](https://github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking)

## License

MIT License

Individual MCP servers retain their original licenses:
- Serena: MIT
- Context7: MIT
- Sequential Thinking: MIT
