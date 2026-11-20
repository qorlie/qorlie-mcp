# Glama

Qorlie's Glama connector listing is already claimed via DNS, not via a GitHub `glama.json`:

https://glama.ai/mcp/connectors/com.qorlie/qorlie

Ownership metadata is published at:

- https://qorlie.com/.well-known/glama.json
- https://api.qorlie.com/.well-known/glama.json

That file follows [Glama's connector schema](https://glama.ai/mcp/schemas/connector.json) (`maintainers` email / claim token). The listing is verified against a record on qorlie.com.

Glama also has a **repo-root** schema at [https://glama.ai/mcp/schemas/server.json](https://glama.ai/mcp/schemas/server.json). That file is for GitHub-crawled local/stdio servers, and its only field is `maintainers`: an array of GitHub usernames. It is not included here because:

- This repository is docs for a hosted remote server, not a local server Glama would build from source.
- The official connector is already claimed via DNS.
- A repo-root `glama.json` would have to list a personal GitHub username.
