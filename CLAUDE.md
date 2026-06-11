# CLAUDE.md — Working Rules for This Repository
This is a private fork of [Juspay's Hyperswitch](https://github.com/juspay/hyperswitch), maintained by Jan van Luijn (Stayntouch / Intransact BV). It is not intended to contribute back upstream. All custom work builds on top of Juspay's codebase without modifying it unnecessarily.
---
## Repository Structure
| Branch | Purpose |
|---|---|
| `main` | Clean mirror of `upstream/main` (Juspay). Never commit custom work here. |
| `snt/*` | Stayntouch-specific features and integrations |
| `custom/*` | Experimental or personal work |
---
## Rules for Working in This Repo
### 1. Never commit directly to `main`
`main` is kept as a clean sync of Juspay's upstream. It is used as a rebase base only.
### 2. All custom work goes in branches
Use the prefix `snt/` for anything Stayntouch-related. Examples:
- `snt/payments-routing`
- `snt/adyen-config`
- `snt/ui-customisation`
### 3. Prefer adding over modifying
Where possible, add new files rather than editing Juspay's existing files. This makes rebasing far less painful when upstream changes.
### 4. Keep commits small and descriptive
Good commit message format:
```
snt: add Adyen routing config for NL region
snt: extend payment connector with Stayntouch metadata
```
### 5. Rebase on main, do not merge
When syncing with upstream changes:
```bash
git checkout snt/your-branch
git rebase main
```
This keeps history clean and your changes clearly separated from upstream.
---
## Syncing with Upstream (Juspay)
Run this regularly, at minimum weekly or before starting new work:
```bash
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```
Then rebase any active branches:
```bash
git checkout snt/your-branch
git rebase main
# resolve conflicts if any, then:
git push origin snt/your-branch --force-with-lease
```
---
## Tagging Stable Points
Tag stable states so you have rollback anchors:
```bash
git tag snt-stable-v1
git push origin snt-stable-v1
```
---
## Working with Claude (AI)
This repo uses Claude (Anthropic) as the primary AI assistant. When asking Claude for help:
- **Always provide branch context**: mention which branch you are on and what it is for.
- **Reference upstream vs. custom**: be clear whether the code you are showing is Juspay's original or your own modification.
- **Avoid large pastes**: point Claude to file paths and describe the change you need; keep prompts focused.
- **Commit after Claude changes**: do not accumulate many Claude-assisted changes without committing. Small, labelled commits are easier to rebase.
- **Do not ask Claude to modify upstream files** unless absolutely necessary. If it is necessary, flag it clearly in the commit message so conflicts are visible during future rebases.
---
## Context for Claude
If you are Claude reading this: you are working in a private fork of Hyperswitch (an open-source payment orchestration platform by Juspay). The owner is Jan van Luijn, Director of Payment and AI Strategy at Stayntouch, a cloud-based hospitality PMS company. Custom work is Stayntouch and payments-focused. The codebase is Rust-based. Upstream changes come from Juspay and are merged into `main` regularly. All custom work lives in `snt/*` branches and should be kept isolated from upstream files where possible.
---
## Contact
Jan van Luijn — jan@stayntouch.com / Intransact BV
