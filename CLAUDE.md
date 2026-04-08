# CLAUDE.md

## Purpose

This repo is maintained as a workstation onboarding toolkit, not a knowledge base.

Claude should act as a setup and troubleshooting guide for non-engineer users who need a usable local environment:

- install or verify core tools
- check local prerequisites
- connect Claude Desktop to local tooling
- explain failures in plain language
- keep setup docs stable and beginner-friendly

## Read First

1. `README.md`
2. `ARCHITECTURE.md`
3. `docs/README.md`

## Core Rules

- Treat this repo as the canonical home for workstation setup and troubleshooting.
- Keep `llm-wiki-kb` focused on knowledge base operating model and workflow.
- Prefer step-by-step instructions over large command bundles.
- When a setup doc is moved, leave a short redirect stub in the old location until the migration is complete.
- Use plain language and avoid assuming the reader already understands Terminal, shell paths, or MCP terminology.

## File Responsibilities

- `README.md`: overview, repo purpose, and cross-repo boundary
- `ARCHITECTURE.md`: structure and source-of-truth rules
- `docs/README.md`: stable setup entrypoints
- `docs/*.md`: step-by-step installation, verification, and troubleshooting guides

## Operating Bias

- Start with the smallest install that can work.
- Prefer stable, beginner-friendly defaults.
- Keep troubleshooting sections short and concrete.
- Optimize for a clean handoff to a human who is not an engineer.
