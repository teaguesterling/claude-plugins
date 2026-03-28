## claude-plugins — Developer Workflow Plugin Marketplace

This is a Claude Code plugin marketplace containing plugins for developer
workflow tools. Each plugin bundles MCP server config, skills (routing
instructions), and optional hooks.

### Structure

```
.claude-plugin/marketplace.json   — plugin catalog (update when adding plugins)
plugins/
  jetsam/                         — git workflow accelerator
  blq/                            — build log query
  fledgling/                      — DuckDB code analysis
```

### Plugin anatomy

Each plugin follows the same pattern:

```
plugins/<name>/
  .claude-plugin/plugin.json      — manifest (name, description, version)
  .mcp.json                       — MCP server config
  skills/<name>-workflow/SKILL.md  — routing table + tool reference
  hooks/                          — optional PreToolUse warning hooks
    hooks.json                    — hook registration
    <name>-warn.sh                — hook script
```

### Adding a new plugin

1. Create `plugins/<name>/` with the structure above
2. The `.mcp.json` should use the tool's standard serve command
3. The skill should have a routing table: "instead of X, use Y"
4. Hooks are optional — add them when the plugin's tools overlap with
   common Bash patterns (git, build, test commands)
5. Add the plugin entry to `.claude-plugin/marketplace.json`
6. Update `README.md`

### Existing tools and their repos

| Plugin | Package | Repo | MCP command |
|--------|---------|------|-------------|
| jetsam | `pip install jetsam-mcp` | teaguesterling/jetsam | `jetsam serve` |
| blq | `pip install blq-cli` | teaguesterling/blq | `blq mcp serve` |
| fledgling | `pip install fledgling` | teaguesterling/source-sextant | `duckdb -init .fledgling-init.sql` |

### Testing plugins

```bash
# Load a plugin locally for testing
claude --plugin-dir ./plugins/jetsam

# Or add the marketplace and install
/plugin marketplace add teaguesterling/claude-plugins
/plugin install jetsam@teague-tools
```

### Conventions

- Plugin names match the tool name (lowercase)
- Skill names use `<tool>-workflow` pattern
- Hook scripts use `<tool>-warn.sh` pattern
- MCP server names match existing conventions (`blq_mcp`, `jetsam`, `fledgling`)
- Version in plugin.json tracks the plugin config version, not the tool version
