# Dekreto Test Marketplace

A local ChatGPT/Codex marketplace containing exactly one sample plugin, one skill, and one public HTTP MCP server reference. No app code, API key, or local MCP process is needed.

## Layout

```text
.agents/plugins/marketplace.json
plugins/marketplace-smoke-test/
  .codex-plugin/plugin.json
  .mcp.json
  skills/marketplace-check/SKILL.md
```

The marketplace uses OpenAI's supported Codex compatibility format. Its plugin path resolves from this repository root, not from `.agents/plugins/`.

## Try it in ChatGPT

1. Open this folder as the project in a ChatGPT desktop surface that supports local plugin marketplaces.
2. Restart ChatGPT, open the Plugins Directory, and select **Dekreto Test Marketplace**.
3. Install **Marketplace Smoke Test** and start a new chat in the project.
4. Ask: **Use the marketplace-check skill to greet me.** Expect `Hello from Dekreto! The marketplace-check skill is loaded.`
5. Ask: **Use the marketplace-check skill to check the MCP connection.** Expect a successful documentation search and fetch, a short description, and a source link.
6. Disable the plugin and start another chat to check that its skill and tools are no longer available; re-enable it to repeat the checks.

Local marketplace availability varies by client. For supported Codex clients, register this directory explicitly if needed:

```sh
codex plugin marketplace add /Users/admin/Development/dekreto-plugins
codex plugin marketplace list
codex plugin list
codex plugin add marketplace-smoke-test@dekreto-test
```

Use your checkout's absolute path if you moved the folder. Registering the marketplace and installing a plugin are separate steps.

## Scaffold verification

Verified with an isolated Codex configuration: marketplace registration, discovery of exactly one plugin, installation, and enabled status. The skill passed the skill validator, and the public MCP endpoint passed initialization, tool discovery, search, and fetch checks. ChatGPT UI installation and skill execution still need the manual checks above.

## Public MCP server

The plugin references `https://developers.openai.com/mcp`, OpenAI's public documentation server. It requires no credentials and provides read-only tools suitable for this smoke test. It is a real documentation service, rather than a dedicated test sandbox.

The skill uses `search_openai_docs` and `fetch_openai_doc` to verify that the connection works. Installation and the greeting check alone do not prove that MCP tools loaded.

## Refresh and troubleshoot

- After editing the plugin, refresh/reinstall it from the marketplace and restart ChatGPT so the installed cache picks up the changes.
- If the marketplace is missing, check that the project root is this folder and that the client supports local marketplaces.
- If the greeting works but MCP fails, check network access to the configured endpoint and whether the client permits remote MCP connections.

References: [OpenAI plugin packaging and local marketplaces](https://developers.openai.com/plugins/build/plugins), [plugin MCP configuration](https://developers.openai.com/api/docs/guides/agents-api/tools/plugins), and [public Docs MCP](https://developers.openai.com/learn/docs-mcp).
