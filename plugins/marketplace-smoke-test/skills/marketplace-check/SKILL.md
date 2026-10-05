---
name: marketplace-check
description: Run the sample marketplace plugin's greeting or public MCP connection check when the user asks to test this plugin.
---

# Marketplace check

For a greeting or skill-only check, respond with:

> Hello from Dekreto! The marketplace-check skill is loaded.

For an MCP connection check, use the bundled `openai_docs` server:

1. Call `search_openai_docs` with query `plugin marketplace` and limit `1`.
2. Call `fetch_openai_doc` on a URL returned by the search.
3. Report that the skill loaded and the MCP search and fetch succeeded, followed by one sentence about the fetched page and a link to it.

Only report MCP success after both calls succeed. If the tools are unavailable or a call fails, report that the skill loaded but the MCP check did not complete, with the actual failure. A greeting alone does not verify the MCP connection.
