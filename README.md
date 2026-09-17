# Osboon MCP Server

Connect your AI assistant to your [Osboon](https://osboon.com) account and ask questions about your own digital business cards in plain language — "How many visits did my card get this week?", "Who viewed it, and from where?", "Which of my cards performs best?". Read-only, free, and you can disconnect at any time.

**Server address:**

```
https://osboon.com/mcp/
```

- **Transport:** Streamable HTTP (remote server — nothing to install or run)
- **Auth:** OAuth 2.1 — authorization code + PKCE, with dynamic client registration and automatic discovery. You sign in on osboon.com; your password never touches the assistant.
- **Access:** read-only, 7 tools, free with any Osboon account

## Connect

Full step-by-step guides for every supported client, with screenshots: **[osboon.com/mcp/connect](https://osboon.com/mcp/connect/)**

**Chat apps** (Claude, Mistral Le Chat, and other MCP-capable assistants): add a custom connector and paste the server address above — the guide covers each one.

**CLI / dev tools:**

```bash
# Claude Code
claude mcp add --transport http osboon https://osboon.com/mcp/

# Codex CLI
codex mcp add osboon --url https://osboon.com/mcp/
```

**Generic MCP client config** (VS Code with GitHub Copilot, Cursor, Zed, Goose, LM Studio, Warp, Gemini CLI, Qwen Code CLI, …):

```json
{
  "mcpServers": {
    "osboon": {
      "type": "http",
      "url": "https://osboon.com/mcp/"
    }
  }
}
```

Your client opens a browser window to osboon.com, you sign in and approve, and the tools appear. About two minutes, once.

## Tools (7, all read-only)

| Tool | What it answers |
|---|---|
| `get_card_analytics` | Visitor counts for your cards over today / 7 days / 30 days |
| `compare_card_analytics` | Ranks your cards by visits over a range and names the best performer |
| `list_card_viewers` | Who viewed your cards — country, city, device type, time (privacy-floored) |
| `get_card_link` | The public URL and slug for one of your cards |
| `get_my_connections` | Your active network connections (people and companies) |
| `get_my_contact_channels` | The contact channels on your own profile (email, phone, website, …) |
| `get_languages` | Reference list of the languages Osboon supports |

## Security & privacy

- **Read-only.** No tool can create, change, or delete anything on your account.
- **Your password never reaches the assistant.** Sign-in and consent happen on osboon.com (OAuth 2.1); the assistant only ever holds a scoped token.
- **Scoped tokens.** Access is split into `analytics:read`, `contact:read`, `profile:read`, and `card:read` — a token carries only what it needs.
- **Viewer data is dashboard-grade only.** `list_card_viewers` returns the same fields your own dashboard shows — country, city, device type, visit time — never IP addresses or user agents. Ranges with fewer visits than the privacy floor return only a count, no rows.
- **Disconnect any time.** On osboon.com: Settings → Security → Agents. Or remove the connector in your AI client — either side kills the access.

## Links

- Setup guides & FAQ: [osboon.com/mcp/connect](https://osboon.com/mcp/connect/)
- Osboon: [osboon.com](https://osboon.com)
- Terms: [osboon.com/eula](https://osboon.com/eula/)

---

This repository is documentation for the hosted Osboon MCP server; the server itself is not open source.
