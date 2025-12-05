---
name: use-context7-mcp
description: Use the Context7 MCP tools to look up library APIs before answering. Use when needing official API docs, methods, or usage examples for a library or package.
---

# Use Context7 MCP for library APIs

## Instructions
1) When asked about a library/package API, first resolve it: call `resolve-library-id` with the package name.
2) If a valid ID is returned, fetch docs with `get-library-docs` (mode `code` for API/reference; `info` for conceptual) and a topic if relevant (e.g., hooks, routing).
3) Cite snippets from retrieved docs; avoid guessing. Prefer latest page unless user specifies version.
4) If multiple matches, pick the closest and mention ambiguity briefly before proceeding.
5) If no match, ask for clarification or alternate names instead of inventing APIs.
6) Do not rely on memory for API shapes when Context7 docs are available; re-fetch as needed for accuracy.

## Example prompts
- "查下某个 npm 包的 hook 签名，用 context7 搜"
- "给我 next.js app router 的官方用法，先用 context7 mcp"
- "mongodb driver 的插入示例，走 context7 的文档"
