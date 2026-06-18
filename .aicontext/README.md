# AI Context

This repository is managed by [ai-frames](https://ai-frames.org) and contains the shared AI context for all repositories in your workspace.

Every folder here is synced to your local `.aicontext/` directory. When you run **Install**, ai-frames transforms these files into the native format expected by each AI assistant (Claude Code, GitHub Copilot, Cursor, Windsurf).

---

## Structure

### `rules/`
Mandatory instructions always injected into the AI context. Use this for coding conventions, API design standards, quality rules, security guidelines — anything the assistant must always follow.

- Files in `rules/` apply to **all assistants**.
- Files in `rules/.claude/` apply **only to Claude Code**.
- Files in `rules/.copilot/` apply **only to GitHub Copilot**.

### `agents/`
Specialized AI subagent definitions. Each file defines a subagent with a specific role, instructions and optionally restricted tool access.

- Files in `agents/` are available to **all assistants** that support subagents.
- Files in `agents/.claude/` are **Claude Code** specific agent definitions.

### `skills/`
Reusable slash commands that extend what the AI assistant can do. Each skill is a `.md` file with a prompt template invoked via a slash command.

- Files in `skills/` are shared across assistants.
- Files in `skills/.claude/` are only available in Claude Code.

### `prompts/`
Reusable prompt templates for common tasks — code review, refactoring, documentation, test generation, etc.

- Files in `prompts/` are shared.
- Files in `prompts/.claude/` become **Claude Code commands** (`.claude/commands/`).
- Files in `prompts/.copilot/` become **Copilot prompt files** (`.github/prompts/`).

### `mcps/`
MCP (Model Context Protocol) server configurations. Each file defines an MCP server that gives the AI assistant access to external tools, APIs or data sources.

### `contexts/`
Project-level context documentation, organized by organization and repository:

```
contexts/
  <org>/
    <repo>/
      CONTEXT.md   — shared context for all assistants
      CLAUDE.md    — Claude Code specific context (merged with CONTEXT.md on install)
      AGENTS.md    — Copilot/agents specific context (merged with CONTEXT.md on install)
```

Use this to document architecture decisions, project conventions, important patterns and anything the AI should know before working on a specific repository.

---

## How it works

1. Edit files in this repo.
2. Open ai-frames and press **Sync** — changes are pulled to your local `.aicontext/`.
3. Press **Install** — ai-frames distributes the right files to each AI assistant's native directory.
