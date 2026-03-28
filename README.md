# teague-tools — Claude Code Plugins

Developer workflow plugins for Claude Code.

## Plugins

| Plugin | Description |
|--------|-------------|
| [jetsam](plugins/jetsam) | Git workflow accelerator — MCP server, agent routing, safety hooks |
| [blq](plugins/blq) | Build Log Query — capture, query, and analyze build/test output |

## Installation

```bash
# Add this marketplace
/plugin marketplace add teaguesterling/claude-plugins

# Install a plugin
/plugin install jetsam@teague-tools
```

## Requirements

Each plugin lists its own requirements. Generally:
- **jetsam**: `pip install jetsam-mcp` + `gh` CLI
- **blq**: `pip install blq-cli`
