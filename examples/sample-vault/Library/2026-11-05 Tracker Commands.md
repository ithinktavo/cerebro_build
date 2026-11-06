---
type: howto
summary: "The exact read and write commands for GitHub Projects through gh and for Jira through acli, with the sign-in step and scope each needs, plus the gh commands for the repositories."
up:
  - "[[Home]]"
created: 2026-11-05
created_by: ai
tags:
  - howto
  - trackers
---

The rules are in `AGENTS.md`: read freely, ask first before any write and show the command, link items by URL, copy only key, title, state, owner, and dates. This note holds the commands. None of them ran during the build, so the first run of each is its check. Where a flag depends on the installed version, the line says so.

## GitHub Projects, owner example-org, project 7

The record for [[Team Alpha]] and [[Checkout Migration]]. Source: profile, 2026-11-05.

Sign-in and scope. The `gh project` commands need the `project` scope on top of the normal sign-in.

```sh
gh auth status                 # who is signed in, and which scopes the token has
gh auth refresh -s project     # adds the project scope once; opens the browser
```

Read freely.

```sh
gh project view 7 --owner example-org                                   # title, fields, item count
gh project field-list 7 --owner example-org                             # field names and ids, used by the filters below
gh project item-list 7 --owner example-org --limit 200 --format json    # every item as JSON
```

The three named queries, until the saved views are recorded in [[Team Alpha]]. The Status values depend on the board; check them with `field-list` first. The `--jq` flag and the JSON shape depend on your version of gh.

```sh
# changed in the last 7 days: issues and pull requests updated this week, per repo
gh issue list -R example-org/checkout-api --state all --limit 100 --search "updated:>=$(date -v-7d +%F)"
gh pr list -R example-org/checkout-api --state all --limit 100 --search "updated:>=$(date -v-7d +%F)"
# open and blocked: items whose Status field is Blocked
gh project item-list 7 --owner example-org --limit 200 --format json --jq '.items[] | select(.status == "Blocked") | "\(.title)\t\(.status)\t\(.content.url // "")"'
# no change in 14 days: open issues not touched for two weeks, per repo
gh issue list -R example-org/checkout-api --state open --limit 100 --search "updated:<$(date -v-14d +%F)"
```

Write only after a yes, with the command shown first.

```sh
gh issue create -R example-org/checkout-api --title "<title>" --body "<body>"     # a new item, then add it to the board
gh project item-add 7 --owner example-org --url <issue or pull request URL>
gh project item-edit --id <item id> --project-id <project id> --field-id <field id> --single-select-option-id <option id>   # ids from field-list and item-list
gh issue comment <number> -R example-org/checkout-api --body "<text>"
gh issue close <number> -R example-org/checkout-api
```

## Jira at example.atlassian.net, through acli

The record for [[Team Beta]] and [[Observability Rollout]]. Project key: _left blank, Alex to fill in_. Source: profile, 2026-11-05.

Sign-in. The flags of `acli jira auth login` depend on your version; check `acli jira auth login --help`.

```sh
acli jira auth status                                      # which site and account are signed in
acli jira auth login --site example.atlassian.net --web    # browser sign-in; never paste a token into the vault or the chat
```

Read freely. Replace `<KEY>` with the project key once it is recorded.

```sh
acli jira project list                                                                                  # find the project key
acli jira workitem search --jql "project = <KEY> AND updated >= -7d ORDER BY updated DESC"              # changed in the last 7 days
acli jira workitem search --jql "project = <KEY> AND statusCategory != Done AND (status = Blocked OR Flagged = Impediment)"   # open and blocked
acli jira workitem search --jql "project = <KEY> AND statusCategory != Done AND updated <= -14d"        # no change in 14 days
acli jira workitem search --jql "assignee = currentUser() AND statusCategory != Done"                   # assigned to me
acli jira workitem view <KEY>-123                                                                       # one item
```

Once the three filters are saved in Jira, "Record these queries in the Team Beta hub" writes their names and ids into [[Team Beta]], and each runs as `--jql "filter = <id>"`. An item's URL is `https://example.atlassian.net/browse/<KEY>-123`.

Write only after a yes, with the command shown first. The flags depend on your version; check `acli jira workitem <command> --help`.

```sh
acli jira workitem create --project <KEY> --type Task --summary "<title>" --description "<text>"
acli jira workitem transition --key <KEY>-123 --status "<status>"
acli jira workitem assign --key <KEY>-123 --assignee "<account>"
acli jira workitem comment create --key <KEY>-123 --body "<text>"   # the docs' usage line says create and its examples omit it; check your version
```

## Repositories, through gh and git

Read freely, in the repository folder for git and with `-R` for gh, because the vault is not a repository.

```sh
git status --short && git branch --show-current && git log --oneline -10
gh pr status -R example-org/checkout-api
gh pr checks -R example-org/checkout-api
gh pr list -R example-org/web-storefront --author @me --state open
gh search prs --review-requested=@me --state=open      # across repos: waiting for my review
gh search prs --author=@me --state=open                # across repos: my open pull requests
gh search issues --assignee=@me --state=open           # across repos: assigned to me
```

Write only after a yes: `git switch -c <branch>`, `git commit`, `git push`, `gh pr create`, `gh pr comment`, `gh pr merge`, each shown in full first.
