# MinerU MCP Plugin README

This plugin enables Claude to extract high-precision structured data (Markdown, HTML, LaTeX, DOCX) from PDFs, images, and web pages using the MinerU API via the Model Context Protocol (MCP).

## 🚀 Features

- **Document Extraction:** Convert PDFs, images, and Word/PPTx files to structured Markdown.
- **Web Extraction:** Fetch and convert remote web pages via URL.
- **Precision Mode:** High-precision table recognition, formula recognition, and OCR.
- **Flash Mode (Default):** Free, no authentication required, limited to 20 pages / 10 MB. **Used automatically if no API Token is set.**

## 🛠️ Setup

### Important Notice

> **未设置 API Token，将使用 Flash 模式（免费，无需认证，限 20 页 / 10 MB）。如需完整功能，请设置 MINERU_API_TOKEN 环境变量。**

This plugin supports automatic fallback to Flash Mode. If you do not provide a `MINERU_API_TOKEN`, it will default to the free tier.

### Required Environment Variables

To unlock full functionality (Precision Mode), set your API token:

```bash
export MINERU_API_TOKEN="your-token-here"
```

### Obtaining Tokens

1. Visit [https://mineru.net/api-keys](https://mineru.net/api-keys) (official MinerU API Token page).
2. Create a new API token.
3. Set the `MINERU_API_TOKEN` environment variable.

## ⚙️ MCP Configuration

Your MCP config (e.g., `claude_desktop_config.json` or `mcp.json`) should remain as follows. The `env` field will pass the environment variable you set to the MinerU MCP server:

```json
{
  "mcpServers": {
    "mineru": {
      "type": "streamableHttp",
      "url": "https://mcp.mineru.net/mcp",
      "env": {
        "MINERU_API_TOKEN": "your token"
      }
    }
  }
}
```

## 📂 Directory Structure

```text
mineru-claude-plugin/
├── .claude-plugin/
│   └── plugin.json      # Plugin metadata
├── .mcp.json            # MCP server configuration
├── skills/              # Skill definitions
│   └── mineru-extract/
│       ├── skill.json   # Skill metadata
│       └── SKILL.md     # Skill instructions
└── README.md            # Documentation
```

## 📖 Usage

Once configured, Claude can use the following capabilities through the Mineru MCP server:

### 1. Document Extraction
- **Flash Extract:** Fast conversion for files up to 10 MB and 20 pages.
- **Precision Extract:** High-precision mode requiring an API token, supporting tables and formulas.

### 2. Web Extraction
- **Crawl:** Convert content from a URL to Markdown or HTML.

## ❓ Troubleshooting

- **Authentication Errors:** If you see 401 Unauthorized, verify your token.
- **Flash Mode Fallback:** If you are not using a token, ensure your file is within the 20 pages / 10 MB limit.
- **Feature Limits:** Flash Mode does not support complex table/formula recognition. Use Precision Mode for these features.

## 🔗 Resources

- [MinerU Website](https://mineru.net/)
- [MinerU Extract Skill](https://clawhub.ai/mineru-extract/mineru-document-extractor)
- [Claude Plugins Documentation](https://github.com/anthropics/claude-plugins-official)
