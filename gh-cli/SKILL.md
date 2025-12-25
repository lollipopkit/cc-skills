---
name: gh-cli
description: Interact with GitHub repositories, PRs, and issues using the `gh` CLI. Use when the user asks to "list PRs", "check out PR", "view issue", or "create release".
allowed-tools: Bash
---

# Use GitHub CLI

## Instructions
1) Ensure gh is available and authenticated: run `gh auth status` (do not use --show-token); respect GH_HOST if set. Prefer GH_TOKEN/GITHUB_TOKEN env auth; never print tokens or add them to files.
2) Set repo context explicitly with `--repo owner/name` or by checking the current repo via `gh repo view`; avoid assuming defaults.
3) Prefer structured output with `--json` fields and `--limit` to keep responses concise (e.g., `gh pr list --state open --json number,title,author,headRefName,baseRefName,url --limit 20`).
4) Common reads: `gh pr view <number> --json number,title,state,author,mergedAt,commits,files,comments,url`, `gh issue list --state all --json number,title,state,author,url --limit 30`, `gh release list --limit 20`, `gh release view <tag> --json tagName,name,publishedAt,url`.
5) For write operations (create/update PRs, issues, comments, releases), confirm intent and required fields; use `--title`, `--body`, or `--body-file` without secrets. Avoid noisy outputs; capture URLs/results only.
6) When checking out PRs locally, use `gh pr checkout <number>` and handle branch existence gracefully; do not alter remotes or push unless explicitly requested.

## Example prompts
- "List open PRs with authors for repo owner/name using gh"
- "Show issue 42 details and comments via gh"
- "Checkout PR 17 locally with gh"
- "Draft release v1.2.0 on repo owner/name using gh"
