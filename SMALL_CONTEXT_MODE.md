# Small-Context Mode for HexStrike AI MCP

## Overview

Small-context mode significantly reduces the initial token load for resource-constrained local LLMs by providing a streamlined tool registration that omits non-essential details.

## Usage

### CLI Options

```bash
# Enable small-context mode with default 4,000 token limit
python3 hexstrike_mcp.py --small-context-mode

# Enable small-context mode with custom token limit
python3 hexstrike_mcp.py --small-context-mode --max-initial-prompt-tokens 2000

# Normal full mode (default)
python3 hexstrike_mcp.py
```

### Configuration File Integration

Update your AI client configuration to use small-context mode:

#### Claude Desktop (`~/.config/Claude/claude_desktop_config.json`)

```json
{
  "mcpServers": {
    "hexstrike-ai": {
      "command": "python3",
      "args": [
        "/path/to/hexstrike-ai/hexstrike_mcp.py",
        "--server",
        "http://localhost:8888",
        "--small-context-mode"
      ],
      "description": "HexStrike AI v6.0 - Small Context Mode",
      "timeout": 300,
      "disabled": false
    }
  }
}
```

#### VS Code Copilot (`.vscode/settings.json`)

```json
{
  "servers": {
    "hexstrike": {
      "type": "stdio",
      "command": "python3",
      "args": [
        "/path/to/hexstrike-ai/hexstrike_mcp.py",
        "--server",
        "http://localhost:8888",
        "--small-context-mode",
        "--max-initial-prompt-tokens",
        "3000"
      ]
    }
  }
}
```

## Token Usage Comparison

| Mode | Tools Registered | Estimated Token Usage | Target Audience |
|------|------------------|----------------------|-----------------|
| **Full Mode** (default) | 150+ tools | ~20,000 tokens | High-capacity models (GPT-4, Claude-3, etc.) |
| **Small-Context Mode** | 10 essential tools | <4,000 tokens | Local LLMs, resource-constrained models |

## Essential Tools in Small-Context Mode

The following 10 essential tools are included in small-context mode:

1. **`nmap_scan`** - Network scanning with Nmap
2. **`execute_command`** - Execute command on HexStrike server
3. **`intelligent_smart_scan`** - AI-driven intelligent scanning
4. **`select_optimal_tools_ai`** - AI tool selection for target
5. **`optimize_tool_parameters_ai`** - AI parameter optimization
6. **`gobuster_scan`** - Directory/DNS brute-forcing with Gobuster
7. **`nuclei_scan`** - Vulnerability scanning with Nuclei
8. **`sqlmap_scan`** - SQL injection testing with SQLMap
9. **`get_process_dashboard`** - Get system process dashboard
10. **`format_tool_output_visual`** - Format tool output with visual styling

## Benefits

- **Reduced Memory Usage**: Significantly lower initial token consumption
- **Faster Initialization**: Quicker tool registration and startup
- **Local LLM Compatibility**: Works with models that have smaller context windows
- **Essential Functionality**: Covers core security testing needs
- **Fallback Access**: Full tool access still available through AI intelligence tools

## Technical Details

- **Token Estimation**: Uses ~4 characters per token approximation
- **Minimal Docstrings**: Essential tools use condensed descriptions
- **Conditional Registration**: Tools are registered based on context mode and token budget
- **Backward Compatibility**: Full mode maintains all existing functionality

## Example Usage

```bash
# For local models with limited context
python3 hexstrike_mcp.py --small-context-mode --max-initial-prompt-tokens 2000

# Standard small-context mode
python3 hexstrike_mcp.py --small-context-mode

# Full feature mode (default)
python3 hexstrike_mcp.py
```