# Calibrate MCP

[MCP server](https://modelcontextprotocol.io) for [Calibrate](https://calibrate.artpark.ai) — expose Calibrate API tools to coding agents like Cursor, Claude Code, or Codex so they can list agents, run tests, and poll results without leaving your editor.

## Install

```bash
npx -y @dalmia/calibrate-mcp start --api-key-auth sk_your_key_here
```

## Usage

Get your API key from the [UI](https://calibrate.artpark.ai/workspace-settings?tab=api-keys), then connect the server in your editor.

**Cursor** — add to MCP settings (`stdio` transport):

```json
{
  "mcpServers": {
    "calibrate": {
      "command": "npx",
      "args": ["-y", "@dalmia/calibrate-mcp", "start"],
      "env": {
        "CALIBRATE_API_KEY_AUTH": "sk_your_key_here"
      }
    }
  }
}
```

**Claude Code:**

```bash
claude mcp add CalibrateMcp -- npx -y @dalmia/calibrate-mcp start --api-key-auth sk_your_key_here
```

Once connected, ask your agent to list agents, resolve names to UUIDs, run tests, or poll run status.

## Self-hosting

For self-hosted Calibrate deployments, pass `--server-url` to point the MCP server at your API instance:

```bash
npx -y @dalmia/calibrate-mcp start \
  --api-key-auth "$CALIBRATE_API_KEY_AUTH" \
  --server-url https://calibrate.my-company.internal
```

## Local development

To test changes from a local clone:

```bash
npm install
npm run build
node bin/mcp-server.js start --api-key-auth sk_your_key_here
```

Point Cursor at the local build by using `node` with the path to `bin/mcp-server.js` instead of `npx @dalmia/calibrate-mcp`.

## Resources

- `npx @dalmia/calibrate-mcp start --help` — all flags and transports
- [Calibrate docs](https://calibrate.artpark.ai/docs) — API reference
