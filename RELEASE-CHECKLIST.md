# Release Checklist

Use this before treating `flh-claude-toolkit` as a publishable repo.

## Repo Shape

- [ ] `README.md` clearly states repo purpose and boundary
- [ ] `ARCHITECTURE.md` matches the current file layout
- [ ] `CLAUDE.md` exists and gives Claude the correct operating rules
- [ ] `docs/README.md` lists the right setup entrypoints

## Setup Coverage

- [ ] `docs/mac-terminal-basics.md` is present
- [ ] `docs/setup-git-cli.md` is present
- [ ] `docs/setup-homebrew.md` is present
- [ ] `docs/setup-nodejs.md` is present
- [ ] `docs/setup-claude-desktop-app.md` is present
- [ ] `docs/setup-github-gh-cli.md` is present
- [ ] `docs/setup-claude-code-cli.md` is present
- [ ] `docs/setup-terminal-mcp.md` is present
- [ ] `docs/setup-google-workspace-gws.md` is present
- [ ] `docs/edit-claude-desktop-config.md` is present
- [ ] `docs/workstation-final-check.md` is present

## Boundary Checks

- [ ] `llm-wiki-kb` links to this repo for environment setup
- [ ] `llm-wiki-kb` no longer presents workstation setup as part of its core narrative
- [ ] Redirect stubs remain in old locations until migration is complete

## Publish Readiness

- [ ] Repo naming is final
- [ ] Canonical GitHub repo exists or the publish plan is explicitly recorded
- [ ] If this repo is synced as a subtree, the upstream remote is configured
- [ ] The first user-facing setup path can be followed end to end without engineer context
- [ ] `gh` is clearly presented as an advanced GitHub option rather than the default clone path

## Final Review

- [ ] A non-engineer can tell when to use this repo and when to use `llm-wiki-kb`
- [ ] The install order is beginner-friendly and consistent
- [ ] Troubleshooting steps point to the right file without circular redirects
- [ ] Required company-workstation tools and optional advanced tools are clearly separated
