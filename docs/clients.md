# Client setup

Remote endpoint: `https://api.qorlie.com/mcp` (Streamable HTTP).

Sign in with your Qorlie account over OAuth 2.1 (PKCE, dynamic client registration). Every signed-in plan gets MCP access, with the same limits as the web app. `initialize` and `tools/list` work without a token. `create_static_qr` also works without signing in and stores nothing. Other tools need OAuth scopes `qorlie:read` or `qorlie:write`.

Discovery:

- Authorization server: https://api.qorlie.com/.well-known/oauth-authorization-server
- Protected resource: https://api.qorlie.com/.well-known/oauth-protected-resource

## Claude

Custom connectors are documented in [Claude's help center](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp).

1. Open **Customize → Connectors**.
2. Add a custom connector. On Team and Enterprise plans, an owner may need to add it under organization settings first.
3. Name it Qorlie.
4. Server URL: `https://api.qorlie.com/mcp`
5. Keep the detected authentication settings (OAuth sign-in).
6. Sign in with your Qorlie account.

## ChatGPT

A Qorlie app in the ChatGPT directory is not live yet. There is no official one-click ChatGPT install today.

If your ChatGPT plan lets you add a custom MCP connector or app:

1. Add a custom MCP server named Qorlie.
2. Server URL: `https://api.qorlie.com/mcp`
3. Sign in with OAuth when prompted.

This page will be updated when the official app is available.

## Cursor

Official docs: [cursor.com/docs/mcp](https://cursor.com/docs/mcp).

One-click (from Cursor, or from the [API & MCP docs](https://qorlie.com/en/docs/api)):

```
cursor://anysphere.cursor-deeplink/mcp/install?name=qorlie&config=eyJ1cmwiOiJodHRwczovL2FwaS5xb3JsaWUuY29tL21jcCJ9
```

Or add the server yourself:

- Project: `.cursor/mcp.json` (example in this repo; a copy is also at `docs/examples/cursor-mcp.json`)
- All projects: `~/.cursor/mcp.json`

```json
{
  "mcpServers": {
    "qorlie": {
      "url": "https://api.qorlie.com/mcp"
    }
  }
}
```

Cursor handles OAuth for remote URL servers. You do not need a pre-registered client ID. Qorlie supports dynamic client registration. Sign in when Cursor prompts you.

## VS Code

Official docs: [MCP configuration reference](https://code.visualstudio.com/docs/agents/reference/mcp-configuration).

- Workspace: `.vscode/mcp.json`
- User: Command Palette → **MCP: Open User Configuration**

```json
{
  "servers": {
    "qorlie": {
      "type": "http",
      "url": "https://api.qorlie.com/mcp"
    }
  }
}
```

`type` must be `http` (Streamable HTTP). On first connect, VS Code opens a browser for OAuth. Do not put a client secret in `mcp.json`.

## Windsurf

Official docs: [Windsurf MCP configuration](https://docs.devin.ai/windsurf/plugins/cascade/mcp).

Open the MCP config file from Windsurf or Cascade settings (do not rely on a hardcoded path; it has moved between editor versions) and add:

```json
{
  "mcpServers": {
    "qorlie": {
      "serverUrl": "https://api.qorlie.com/mcp"
    }
  }
}
```

`url` is also accepted in place of `serverUrl`. Save, enable the server if it is toggled off, and complete OAuth if prompted.

## Other clients (`mcp-remote`)

[mcp-remote](https://github.com/punkpeye/mcp-remote) bridges stdio-only clients to a remote Streamable HTTP server and runs the OAuth flow locally. Requires Node.js and `npx`.

```json
{
  "mcpServers": {
    "qorlie": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://api.qorlie.com/mcp",
        "--transport",
        "http-only"
      ]
    }
  }
}
```

`--transport http-only` matches Qorlie's Streamable HTTP endpoint (POST only). Tokens are stored locally by mcp-remote, not in this repository.
