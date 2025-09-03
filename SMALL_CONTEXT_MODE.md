# Small-Context Mode for HexStrike AI MCP

## Overview

Small-context mode significantly reduces the initial token load for resource-constrained local LLMs by compressing tool descriptions while **maintaining access to ALL 161 security tools**.

### Key Benefits

- ✅ **ALL 161 tools remain available** (no tool limitation)
- ✅ **~80% token reduction** through description compression
- ✅ **Full functionality preserved** while reducing context size
- ✅ **Intelligent docstring compression** maintains essential information
- ✅ **Backward compatible** with existing configurations

### How It Works

Instead of limiting the number of available tools, small-context mode uses intelligent docstring compression:

1. **Full Mode**: Tools have detailed descriptions (~20,000 tokens)
2. **Small-Context Mode**: Same tools with compressed descriptions (<4,000 tokens)
3. **Compression Strategy**: Extracts main description, removes verbose Args/Returns sections
4. **Preservation**: Core functionality and tool parameters remain unchanged

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
| **Full Mode** (default) | 161 tools (full descriptions) | ~20,000 tokens | High-capacity models (GPT-4, Claude-3, etc.) |
| **Small-Context Mode** | 161 tools (compressed descriptions) | <4,000 tokens | Local LLMs, resource-constrained models |

## All Tools Available in Small-Context Mode

**NEW APPROACH**: Small-context mode now provides access to **ALL 161 security tools** with compressed descriptions instead of limiting to a subset.

### Tool Categories (All Available):

**🔍 Network & Reconnaissance (25+ tools):**
- `nmap_scan`, `masscan_scan`, `rustscan_scan`, `autorecon_scan`, `amass_scan`, `subfinder_scan`, `fierce_scan`, `dnsenum_scan`, etc.

**🌐 Web Application Security (40+ tools):**
- `gobuster_scan`, `feroxbuster_scan`, `ffuf_scan`, `dirb_scan`, `nuclei_scan`, `nikto_scan`, `sqlmap_scan`, `wpscan_scan`, etc.

**🔐 Authentication & Password (12+ tools):**
- `hydra_scan`, `john_crack`, `hashcat_crack`, `medusa_scan`, `patator_scan`, `evil_winrm_scan`, etc.

**🔬 Binary Analysis & Reverse Engineering (25+ tools):**
- `ghidra_analyze`, `radare2_analyze`, `gdb_debug`, `binwalk_extract`, `ropgadget_find`, etc.

**☁️ Cloud & Container Security (20+ tools):**
- `prowler_scan`, `scout_suite_scan`, `trivy_scan`, `kube_hunter_scan`, etc.

**🏆 CTF & Forensics (20+ tools):**
- `volatility_analyze`, `autopsy_analyze`, `steghide_extract`, etc.

**🕵️ OSINT & Intelligence (20+ tools):**
- `sherlock_scan`, `social_analyzer_scan`, `recon_ng_scan`, etc.

## Benefits

- **✅ Full Tool Access**: ALL 161 tools available regardless of context mode
- **✅ Dramatic Token Reduction**: ~80% reduction through description compression
- **✅ Preserved Functionality**: Tool parameters and capabilities unchanged
- **✅ Local LLM Compatibility**: Works with models that have smaller context windows  
- **✅ Intelligent Compression**: Main descriptions preserved, verbose sections removed
- **✅ Zero Functionality Loss**: No tool limitation or capability reduction

## Technical Details

- **Compression Strategy**: Intelligent docstring compression preserves essential information
- **Token Estimation**: Uses ~4 characters per token approximation
- **Dynamic Compression**: Descriptions compressed based on context mode setting
- **Backward Compatibility**: Full mode maintains all existing functionality
- **All Tools Available**: Both modes now register identical tool sets

## Example Usage

```bash
# For local models with limited context
python3 hexstrike_mcp.py --small-context-mode --max-initial-prompt-tokens 2000

# Standard small-context mode
python3 hexstrike_mcp.py --small-context-mode

# Full feature mode (default)
python3 hexstrike_mcp.py
```