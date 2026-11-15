# Twinpost MCP server

Crosspost from chat. Ask your AI app to show the accounts and X mirrors in your Twinpost workspace, check what was mirrored or failed, preview a post on each network, draft a crosspost for Bluesky, Threads, Telegram, LinkedIn and more, and publish or retry only when you confirm.

This is a hosted remote MCP server. There is nothing to install.

- Endpoint: `https://twinpo.st/mcp` (Streamable HTTP)
- Sign-in: OAuth 2.1 with dynamic client registration. You sign in to your Twinpost account in the browser. There is no API key.
- Docs: https://go.twinpo.st/mkt-github-docs
- Website: https://go.twinpo.st/mkt-github
- Server card: https://twinpo.st/.well-known/mcp/server-card.json
- License: MIT (this repository's metadata and docs)

## Connect

Claude Code:

```bash
claude mcp add --transport http twinpost https://twinpo.st/mcp
```

Claude (claude.ai and desktop), ChatGPT and other apps with custom connectors: add a custom connector (remote MCP server), paste https://twinpo.st/mcp and sign in with Twinpost when asked.

Cursor (`~/.cursor/mcp.json` or `.cursor/mcp.json`) and any client that reads `mcpServers`:

```json
{
  "mcpServers": {
    "twinpost": {
      "url": "https://twinpo.st/mcp"
    }
  }
}
```

VS Code: run MCP: Add Server, choose HTTP and paste the server URL.

## Tools

| Tool | Access | What it does |
| --- | --- | --- |
| `whoami` | read | Shows which Twinpost account and workspace the app is using. |
| `list_accounts` | read | Lists your connected accounts: X and the networks you mirror to. |
| `list_mirrors` | read | Lists your mirrors, whether each is on, and its targets. |
| `list_mirror_activity` | read | Shows recent mirrored posts and where each one landed or failed. |
| `preview_crosspost` | read | Shows how a post would look on each network, with nothing sent. |
| `draft_crosspost` | draft | Saves a crosspost as a draft. Never publishes. |
| `list_drafts` | read | Lists your saved drafts. |
| `list_scheduled_posts` | read | Lists posts that are scheduled to go out. |
| `publish_draft` | publish | Publishes or schedules a draft. Asks for your confirm first. |
| `pause_mirror` | pause or resume | Pauses a mirror, or resumes it. Resuming asks for your confirm. |
| `retry_mirror_post` | publish | Publishes again a mirrored post that failed. Asks for your confirm first. |

Full input schemas and annotations are in the server card above.

## Safety

- Drafts never publish on their own.
- Anything that reaches an audience needs `confirm: true`, which the AI only sends after you say yes in the chat.
- Reading, previews and drafts work on any Twinpost plan. Publishing a draft directly needs a plan that includes direct posts; otherwise the tool returns a clear plan message.
- Disconnect an app any time at https://twinpo.st/app/apps. It loses access straight away.

## Privacy

The app never sees your password. See the [Privacy Policy](https://twinpo.st/privacy).

## Support

Documentation: https://go.twinpo.st/mkt-github-docs

## Repository contents

- `server.json`: MCP registry manifest for the remote server.
- `.mcp.json`, `.cursor-plugin/plugin.json`, `.claude-plugin/marketplace.json`, `plugins/twinpost/`: plugin metadata for clients and directories that scan a repository.
- The server itself runs at twinpo.st; this repository holds its metadata and docs.
