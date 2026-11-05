---
type: hub
summary: ""
up:
  - "[[Home]]"
created: "{{date:YYYY-MM-DD}}"
tags:
  - repo
---

## Current state ({{date:YYYY-MM-DD}})

- 

## Repository

- Local path: 
- GitHub: 
- Default branch: 
- Read at commit: 

## Serves

- Which project or team, and which part of the system.

## Architecture (read at commit )

- Ten lines at most, written from the repository.

## Documents to read

- Paths in the repository: README, docs, PR template, AGENTS.md or CLAUDE.md if present.

## Run and test

- 

## Conventions

- 

## Gotchas

- 

## Live views

Results are never stored. Run and read.

```sh
gh pr list -R <owner>/<repo> --author @me --state open
gh pr list -R <owner>/<repo> --search "review-requested:@me" --state open
gh run list -R <owner>/<repo> --status failure --limit 10
```

## Notes in this folder

- Log: created on first need, as `YYYY-MM-DD <repo> Log.md`.
