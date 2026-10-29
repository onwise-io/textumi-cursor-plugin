# Textumi for Cursor

Check text for AI-writing signals and rewrite English drafts in a natural human voice, right from the Cursor agent. Facts, numbers and links of the original are kept.

The plugin adds:

- **MCP server** `textumi` → `https://textumi.com/mcp` (Streamable HTTP, sign-in with OAuth).
- **Skill** `textumi` → tells the agent when and how to use the tools.

## Tools

| Tool | What it does |
|---|---|
| `detect_ai_text` | Scores how strongly a text shows patterns typical of AI writing (0–100, an uncalibrated signal, not proof of authorship). |
| `humanize_text` | Starts a rewrite of an English text of 50–2,000 words. Textumi writes the drafts and checks numbers, links and length; the agent reviews the meaning. |
| `humanize_continue` | Sends the agent's reviews and returns the next state. |
| `humanize_status` | Shows the state of a rewrite in progress. |
| `humanize_cancel` | Stops a rewrite that is no longer needed. |
| `get_account` | Shows the plan and what is left of its allowances. |

## Install

1. Install **Textumi** from the Cursor Marketplace (**Customize** → search "Textumi" → **Install**).
2. When Cursor asks, sign in to your Textumi account in the browser and allow access.
3. Ask the agent, for example: "Check this README with Textumi" or "Humanize this release note with Textumi".

Checks and rewrites need a Textumi plan that includes work through an assistant. See [plans](https://textumi.com/pricing).

### Test from this repository

Copy this folder to `~/.cursor/plugins/local/textumi`, then run **Developer: Reload Window** and open **Customize**.

### Access token instead of sign-in

If your setup cannot open a browser sign-in, create an access token at [textumi.com/account/agents](https://textumi.com/account/agents), put it in the `TEXTUMI_TOKEN` environment variable and add this to your own `~/.cursor/mcp.json` instead of installing the plugin:

```json
{
  "mcpServers": {
    "textumi": {
      "url": "https://textumi.com/mcp",
      "headers": { "Authorization": "Bearer ${env:TEXTUMI_TOKEN}" }
    }
  }
}
```

Never commit a token to a repository.

## Privacy and security

- Texts are sent to Textumi only when you or the agent call a tool, and are processed for that request. What is kept and for how long depends on your plan and is described in the [privacy policy](https://textumi.com/privacy).
- The plugin contains no code, scripts or binaries: only a manifest, an MCP server address, a skill and a logo.
- Sign-in uses OAuth 2.1 with PKCE. You can see and disconnect every connected app at [textumi.com/account/agents](https://textumi.com/account/agents).

## Support

[support@textumi.com](mailto:support@textumi.com) · [Setup guide](https://textumi.com/connect-cursor)

## License

MIT
