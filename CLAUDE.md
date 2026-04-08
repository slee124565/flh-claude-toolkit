# CLAUDE.md

## Purpose

This repo is maintained as a workstation setup and troubleshooting documentation repo.

Claude should treat this repository as the canonical home for:

- installation prerequisites
- CLI setup instructions
- MCP setup instructions
- verification steps
- concise troubleshooting notes

The target reader may be non-engineer colleagues, but that is a writing constraint, not the repo's core identity.

## Read First

1. `README.md`
2. `ARCHITECTURE.md`
3. `QUICKSTART.md`
4. `docs/README.md`

## Core Rules

- Keep this repo focused on workstation setup and tooling prerequisites.
- Keep `llm-wiki-kb` focused on knowledge base operating model and workflow.
- Prefer maintaining stable docs over embedding setup logic in chat responses.
- Prefer step-by-step instructions over large command bundles.
- Use plain language, but do not turn every document into a hand-holding tutorial.
- Update verification and troubleshooting sections when setup assumptions change.

## File Responsibilities

- `README.md`: human-facing repo overview and boundary
- `QUICKSTART.md`: linear onboarding path for first-time users
- `ARCHITECTURE.md`: source-of-truth and repo boundary rules
- `docs/README.md`: documentation index
- `docs/*.md`: stable setup, verification, and troubleshooting docs

## Operating Bias

- Keep docs short and durable.
- Optimize for reuse across multiple coworkers.
- Prefer explicit verification steps.
- Treat audience friendliness as a style rule, not a reason to blur repo boundaries.
