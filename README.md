# Agent Skills for NeetTracker

Official AI Agent Skills for building complete NEET UG, JEE Main, and CET Test Paper Generator applications using the [NeetTracker Question Bank API](https://api.neettracker.com) and official MCP server (`https://api.neettracker.com/mcp`).

---

## ⚡ Quick Install

### Claude Code
```bash
npx skills add harshgp/skills -a claude-code
```
Or via plugin command in Claude Code:
```bash
/plugin add https://github.com/harshgp/skills
```
Or git clone:
```bash
git clone https://github.com/harshgp/skills.git ~/.claude/skills/neettracker
```

### Antigravity / Gemini CLI
```bash
npx skills add harshgp/skills -a antigravity
```
Or git clone:
```bash
git clone https://github.com/harshgp/skills.git ~/.gemini/config/skills/neettracker
```

### Cursor
```bash
npx skills add harshgp/skills -a cursor
```
Or git clone:
```bash
git clone https://github.com/harshgp/skills.git ~/.cursor/skills/neettracker
```

### Codex
```bash
npx skills add harshgp/skills -a codex
```

### OpenCode
```bash
npx skills add harshgp/skills -a opencode
```

---

## 🔌 Or Connect Via MCP (Zero GitHub Needed)

You can also connect directly to the official NeetTracker Model Context Protocol (MCP) server at:
```
https://api.neettracker.com/mcp
```

### Claude Desktop / Claude Code MCP
```bash
claude mcp add --header "Authorization: Bearer YOUR_NEETTRACKER_API_KEY" neettracker https://api.neettracker.com/mcp
```

### Config JSON (`claude_desktop_config.json` / Antigravity / Cursor / VS Code)
```json
{
  "mcpServers": {
    "neettracker": {
      "url": "https://api.neettracker.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_NEETTRACKER_API_KEY"
      }
    }
  }
}
```

---

## 📖 Autonomous 2-Command Flow

1. Ask your agent: `Visit api.neettracker.com`
2. Next command: `Build`

Your agent will autonomously scaffold, design, and validate the complete test paper generator using NeetTracker's verified 5 Lakh+ question bank.

Get your API key at [https://api.neettracker.com/get-started](https://api.neettracker.com/get-started).
