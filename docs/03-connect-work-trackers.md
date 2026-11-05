# 3. Connect your work tracker

The vault links to tracker items and never copies them. Connecting the tracker means the AI can read the live state when you ask for a status report or a check-in agenda, through the tracker's command-line tool, with your own permissions and nothing more.

## The pattern, whatever the tracker

1. Install the command-line tool.
2. Sign in once. Prefer your company sign-in where the tool supports it. Where it needs a personal access token, let the tool keep it in its own secure store or read it from an environment variable. A token never goes in the vault or in a note.
3. Run one read command in a plain terminal to check that it works. If it does not work there, it will not work for the AI.
4. Tell the AI. If you named the tracker in the build prompt, the rules and the tool's name are already in `AGENTS.md` and `Me.md`. If you connected it later, say: "My tracker is [Jira or Azure DevOps] at [URL], through [the tool]. Update AGENTS.md and Me.md." The tool shows the before and after, and you say yes. Record the shared queries or saved filters it may run by name in the team or project hub, under the tracker links.

The rules the vault gives the AI:

- Read freely: list, view, search, query.
- Ask first, showing the exact command: create, update, assign, transition, comment.
- Link items by URL. Copy only the key, the title, the state, and the dates.
- Never log in, store, or print tokens.

## Jira

Two command-line tools work with Jira Cloud. Both can use an API token, which you create in your Atlassian account settings under Security, then API tokens. Atlassian's own tool can also sign in through the browser.

### Atlassian CLI, Atlassian's own tool

Install on macOS with `brew tap atlassian/homebrew-acli` and then `brew install acli`. On Windows, download `acli.exe` from the install page. On Linux, use the apt or yum repository on the same page. Docs: [developer.atlassian.com/cloud/acli](https://developer.atlassian.com/cloud/acli/guides/install-acli/). It documents Jira Cloud; for Jira Data Center use jira-cli below.

Sign in through the browser:

```bash
acli jira auth login --web
```

Or with a token kept in a file outside the vault:

```bash
acli jira auth login --site "yourcompany.atlassian.net" --email "you@yourcompany.com" --token < token.txt
```

Read:

```bash
acli jira workitem view KEY-123
acli jira workitem search --jql "assignee = currentUser() AND statusCategory != Done" --limit 50
acli jira workitem search --jql "project = TEAM AND updated >= -7d" --json
```

Write, always shown first:

```bash
acli jira workitem create --summary "New task" --project "TEAM" --type "Task"
acli jira workitem transition --key "KEY-123" --status "Done"
acli jira workitem comment create --key "KEY-123" --body "Comment text"
```

If a command errors, add `--help` to it to see the syntax of your version.

### jira-cli, open source

Install on macOS with `brew tap ankitpokhrel/jira-cli` and then `brew install jira-cli`. On Windows, the project's wiki lists Scoop (`scoop bucket add extras`, then `scoop install jira-cli`) and release binaries. Anywhere with Go: `go install github.com/ankitpokhrel/jira-cli/cmd/jira@latest`. Docs: [github.com/ankitpokhrel/jira-cli](https://github.com/ankitpokhrel/jira-cli).

Set the token in your shell profile, not in the vault, then run the setup once:

```bash
export JIRA_API_TOKEN="the token, set in your shell profile"
jira init
```

Choose Cloud, then enter the site, your login, and the default project and board. For Jira Data Center, use a personal access token with `JIRA_AUTH_TYPE=bearer` and choose Local. The token can also sit in the macOS Keychain or in `.netrc` instead of the environment.

Read:

```bash
jira me
jira issue list -a$(jira me) -s~Done
jira issue list -q "project = TEAM AND updated >= -7d" --plain
jira issue view KEY-123
jira sprint list --current
jira epic list
```

Write, always shown first:

```bash
jira issue create -tTask -s"Title" -b"Description" --no-input
jira issue move KEY-123 "In Progress"
jira issue comment add KEY-123 "Comment text"
```

### Saved filters

Create one saved filter per team or project in Jira, such as "Team Alpha, updated in the last 7 days". The AI then searches with `filter = "Team Alpha, updated in the last 7 days"` instead of inventing a query each time, and you can read the same filter in the browser.

## Azure DevOps

The Azure CLI with the Azure DevOps extension. It works with Azure DevOps Services, the cloud service, and not with Azure DevOps Server on premises. Docs: [learn.microsoft.com/azure/devops/cli](https://learn.microsoft.com/en-us/azure/devops/cli/).

Install the Azure CLI if it is not there yet, with `brew install azure-cli` on macOS, `winget install Microsoft.AzureCLI` on Windows, or the installer at [learn.microsoft.com/cli/azure/install-azure-cli](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli). Then add the extension:

```bash
az extension add --name azure-devops
```

Sign in with your company account and set the defaults, so no command needs the organization and project again:

```bash
az login
az devops configure --defaults organization=https://dev.azure.com/YOURORG project="Your Project"
```

If your organization requires a personal access token instead, `az devops login --organization https://dev.azure.com/YOURORG` prompts for it, or the tool reads it from the `AZURE_DEVOPS_EXT_PAT` environment variable. Never from a note.

Read:

```bash
az boards work-item show --id 123 -o table
az boards query --id <saved-query-id> -o table
az boards query --wiql "SELECT [System.Id], [System.Title], [System.State], [System.AssignedTo] FROM WorkItems WHERE [System.TeamProject] = @project AND [System.ChangedDate] >= @Today - 7 ORDER BY [System.ChangedDate] DESC" -o table
az repos pr list --status active -o table
az pipelines runs list --top 10 -o table
```

Write, always shown first:

```bash
az boards work-item create --title "Title" --type Task --assigned-to "you@yourcompany.com"
az boards work-item update --id 123 --state Active
```

Shared queries do the heavy lifting. Create one per team or initiative under Boards, Queries, Shared Queries, copy its id from the URL, and record the id in the team hub. The AI runs `az boards query --id` with it and never has to write a query. `-o table` gives a readable table; `--query` with a JMESPath expression picks fields.

## GitHub

Install the GitHub CLI with `brew install gh` on macOS or `winget install GitHub.cli` on Windows; other options are at [cli.github.com](https://cli.github.com/).

```bash
gh auth login
gh pr list --state open
gh pr view 123
gh issue list --assignee "@me"
gh run list --limit 10
```

Docs: [cli.github.com/manual](https://cli.github.com/manual/). Creating issues, commenting, and merging are shown first.

## What to ask once it works

- "Status report for Team Alpha for this week from the tracker."
- "Which items in project TEAM changed state in the last 7 days? Group them by owner."
- "Open pull requests older than three days in [repository]."
- "Log a check-in for Alpha from the items that moved today."

## Troubleshooting

- Not signed in, or a 401 error: run the sign-in command again. Tokens expire.
- The AI says the command is not found: open a new terminal and check that the tool runs there. It must be on the path of the shell the AI uses.
- Huge output: narrow by date, add `--limit` or `--top`, and use `-o table` or `--plain`.
- The AI invents a query that fails: give it a saved query or filter by name instead.

Next: [Working day to day](04-working-day-to-day.md).
