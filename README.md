# Qorlie remote MCP

Qorlie makes editable QR codes and short links that never expire. This repository is docs and connection info for the hosted remote MCP server. It does not contain product source code.

**Endpoint:** `https://api.qorlie.com/mcp` (Streamable HTTP)

**Auth:** Sign in with your Qorlie account over OAuth 2.1 (PKCE). Every signed-in plan gets MCP access, with the same limits as the web app. Tool discovery works without signing in. Creating a stored link or reading your stats requires a sign-in.

Official MCP Registry: [`com.qorlie/qorlie`](https://registry.modelcontextprotocol.io/v0/servers/com.qorlie%2Fqorlie/versions/latest) 0.3.0. Docs: [qorlie.com/en/docs/api](https://qorlie.com/en/docs/api).

## Setup

Copy-paste configs below. Longer steps for each client are in [docs/clients.md](docs/clients.md).

### Claude

In Claude, open **Customize → Connectors**, add a custom connector named Qorlie, and use this server URL:

```
https://api.qorlie.com/mcp
```

Sign in with your Qorlie account when prompted. See [Claude's custom connector guide](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp).

### ChatGPT

A Qorlie app in the ChatGPT directory is not live yet. If your ChatGPT plan lets you add a custom MCP connector or app, use `https://api.qorlie.com/mcp` and sign in with OAuth. This page will be updated when the official app is available.

### Cursor

[Add to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=qorlie&config=eyJ1cmwiOiJodHRwczovL2FwaS5xb3JsaWUuY29tL21jcCJ9), or put this in `.cursor/mcp.json` (an example is in this repo) or `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "qorlie": {
      "url": "https://api.qorlie.com/mcp"
    }
  }
}
```

Sign in when Cursor prompts you. See [Cursor's MCP docs](https://cursor.com/docs/mcp).

### VS Code

Put this in `.vscode/mcp.json`, or in your user MCP config via **MCP: Open User Configuration**:

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

See [VS Code MCP configuration](https://code.visualstudio.com/docs/agents/reference/mcp-configuration).

### Windsurf

Open the MCP config from Windsurf settings and add:

```json
{
  "mcpServers": {
    "qorlie": {
      "serverUrl": "https://api.qorlie.com/mcp"
    }
  }
}
```

`url` is also accepted in place of `serverUrl`. See [Windsurf MCP docs](https://docs.devin.ai/windsurf/plugins/cascade/mcp).

### Other clients (`mcp-remote`)

If a client only supports local stdio servers, use [mcp-remote](https://github.com/punkpeye/mcp-remote):

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

## Tools

Live list from `tools/list` (public, no sign-in required). Write tools need a signed-in account. Bulk create and Bitly import also need Scan Pass or Business.

| Tool | What it does | Access |
| --- | --- | --- |
| `create_static_qr` | Encode a URL or text into a QR image. Nothing is stored. Works without signing in. | Read-only |
| `create_fixed_link` | Create a fixed (non-editable) short link and QR on your account. | Write |
| `create_dynamic_qr` | Create an editable short link and QR you can change later. | Write |
| `update_dynamic_qr` | Change the destination URL or title of an editable code. | Write |
| `list_dynamic_qrs` | List your codes and links (fixed and editable). | Read-only |
| `get_qr_analytics` | Pull scan stats for one of your codes. Detail depends on your plan. | Read-only |
| `get_account_analytics` | Pull account-wide scan rollups. | Read-only |
| `get_plan` | Show your plan, limits, and remaining credits. | Read-only |
| `import_bitly_csv` | Preview a Bitly CSV import. Needs Scan Pass or Business. | Write |
| `bulk_create_dynamic_qrs` | Create multiple editable codes at once. Needs Scan Pass or Business. | Write |

## Example prompts

- Make a QR code for https://example.com/menu.
- Point my spring-menu code to the new PDF.
- How many scans did my flyer get last week?

## Pricing

An editable code is $12 once and includes 10k scans/mo. Scan Pass is $9/mo. Every signed-in plan, including free, gets MCP access with the same limits as the web app. Full plan details are on the [pricing page](https://qorlie.com/en/pricing).

## Links

- [qorlie.com](https://qorlie.com)
- [API & MCP docs](https://qorlie.com/en/docs/api)
- [Pricing](https://qorlie.com/en/pricing)
- [Privacy](https://qorlie.com/en/privacy)
- [Terms](https://qorlie.com/en/terms)
- [Security](https://qorlie.com/en/docs/security)
- Support: [support@qorlie.com](mailto:support@qorlie.com)
- [Glama listing](https://glama.ai/mcp/connectors/com.qorlie/qorlie) (already claimed via DNS)
