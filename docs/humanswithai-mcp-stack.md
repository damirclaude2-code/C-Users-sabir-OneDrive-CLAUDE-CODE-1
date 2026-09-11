# HWAI Context Router

This project has been connected to Humanswith.ai MCP Stack as HWAI Context Router, the local technical core of a Token Efficiency Platform for Agentic IDEs.

- Installed profile: `core`
- Configured clients: claude
- Available MCP services: `router-lite-mcp`, `mcp-token-router`, `retrieval-mcp`, `context-prep-mcp`, `static-analysis-mcp`, `repo-history-mcp`, `repo-quality-gate-mcp`

## How Agents Should Use It

HWAI Context Router is not a set of slash commands for the user to memorize. It is a local prep layer for Claude Code, Codex, Cursor, and Windsurf. Agents should infer when to use it from natural language, prepare compact evidence, and keep frontier reasoning for final judgment.

| User wording, not commands | Agent should consider |
| --- | --- |
| "where is this implemented", "найди где живет", "что менять", "before editing find context" | `retrieval-mcp`, `language-graph-mcp`, `repo-history-mcp` |
| "huge log", "CI output", "stack trace", "summarize this long spec", "длинные логи" | `context-prep-mcp` |
| "compress this context", "сожми контекст", "preserve evidence", "too much tool output" | `context-prep-mcp` via context compression |
| "is this safe to merge", "quality gate", "static check", "перед PR проверь" | `static-analysis-mcp`, `repo-quality-gate-mcp` |
| "repo is growing", "find stale docs", "cleanup docs", "мусор в репо" | `repo-hygiene-mcp`, `docs-hygiene-mcp`, `docs-sync-mcp` |
| "release blocker", "missing LICENSE", "generated dist committed", "public repo hygiene" | `repo-hygiene-mcp`, `repo-quality-gate-mcp` |
| "API/schema changed", "contract drift", "dependency risk", "lockfile risk" | `contract-schema-mcp`, `dependency-risk-mcp` |
| "Playwright trace", "trace.zip", "HAR", "why did this browser test fail" | `playwright-trace-mcp`, `agent-trace-mcp` |
| "screenshot", "visual diff", "compare UI", "скриншот", "визуально проверь" | `visual-baseline-mcp` |

## Safety Rules

- Local repo/file evidence stays local by default.
- Agents still inspect exact files before edits.
- MCPs reduce noise and token waste; they do not replace frontier reasoning for hard judgment calls.
- Do not commit `~/.hwai/mcp-stack/env`, generated MCP configs with secrets, traces, logs, screenshots, or request artifacts.

## Maintenance

Re-run the installer from the project root after stack updates. Use `HWAI_MCP_AGENT_DOCS=skip` or `--agent-docs=skip` only if you intentionally do not want these local agent instructions updated.
