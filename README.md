# flh-claude-toolkit

`flh-claude-toolkit` is a private FLH onboarding toolkit for setting up a Mac so non-engineer colleagues can work with Claude and related local tools without having to learn the full terminal stack first.

Use this repo when the problem is setup, not knowledge modeling:

- Terminal basics
- Homebrew
- Node.js
- GitHub `gh` CLI
- Claude Desktop App
- Claude Code CLI
- MCP setup
- Google Workspace `gws` CLI / MCP

## What this repo is for

This repo is the starting point when you need help with:

- a tool that is not installed yet
- a `command not found` error
- Claude Desktop not seeing local tools
- MCP setup and verification
- beginner-friendly troubleshooting

If you are trying to design or maintain a knowledge base, use [`llm-wiki-kb`](../llm-wiki-kb/README.md) instead.

## Start here

1. `docs/mac-terminal-basics.md`
2. `docs/setup-homebrew.md`
3. `docs/setup-nodejs.md`
4. `docs/setup-github-gh-cli.md`
5. `docs/setup-claude-code-cli.md`
6. `docs/setup-terminal-mcp.md`
7. `docs/setup-google-workspace-gws.md`

## What lives here

The docs in this repo are organized around stable workstation setup and troubleshooting:

- basic terminal use
- installation prerequisites
- step-by-step setup
- verification steps
- plain-language troubleshooting

## Repo boundary

- `flh-claude-toolkit`
  Owns workstation onboarding and local tooling setup
- `llm-wiki-kb`
  Owns knowledge base structure, ingestion, querying, and maintenance workflows

The two repos are related, but they should stay separate.
