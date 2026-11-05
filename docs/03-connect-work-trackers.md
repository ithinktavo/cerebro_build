# 3. Connect your work trackers

GitHub and the work trackers stay the systems of record. The vault links to their items and never copies them. Connect a tracker and the AI can read its live state through the tracker's command-line tool, with your own permissions and nothing more.

This serves both jobs the guide is written for:

- A manager, PM, or director asks for a status report or a check-in agenda and gets it from the tracker, not from memory, with a source on every line. See [Managers, PMs, and directors](../roles/pm-director.md).
- A developer asks what is assigned to them across several repositories, which of their pull requests wait on review, and what changed in a repository since the last session. See [Developers](../roles/developer.md).

Many people are both. One vault handles it, because each team or project hub names its own tracker. Team Alpha can sit in Jira, Team Beta in GitHub Projects, and a third team in Azure DevOps at the same time.

## The pattern, whatever the tracker

The commands run in the AI tool that opens the vault folder: Claude Code, Codex, or GitHub Copilot, as set up in [Connect your AI tools](02-connect-ai-tools.md). Chat tools cannot run them.

1. Install the command-line tool.
2. Sign in once. Prefer your company sign-in, through the browser, where the tool supports it. Where it needs a personal access token, let the tool keep it in its own secure store or read it from an environment variable. A token never goes in the vault or in a note.
3. Run one read command in a plain terminal, in the form the AI will use: a `gh` command always names its repository with `-R`, so that it never depends on the folder it runs in. If it does not work there, it will not work for the AI.
4. Create the three named queries for each team in the tracker itself: changed in the last 7 days; open and blocked; no change in 14 days. Add one more per tracker, assigned to me and open, which "Start my day" runs; it is recorded under Trackers and tools in `Home.md`. Then say: "Record these queries in the Team Alpha hub". The AI writes their names or ids into the hub's Tracker section and quotes them on `Home.md` under Trackers and tools. Until they are recorded, a status report carries marked blanks instead of invented queries.

If you cannot install anything on your machine, run the saved queries in the tracker's browser view instead, copy or export the key, title, state, owner, and dates, and paste them to the AI with "from Jira export, [date]" as the source. "Start my day, vault only" and every vault-side ritual still work; what you lose is the live read.

What the AI knows about your trackers lives in two places. Each team or project hub records its tracker, the tool, and the three queries by name or id. The exact read and write commands live in `Library/YYYY-MM-DD Tracker Commands.md`, which the build writes for every tracker you named in the Trackers line of your profile, dated the day the vault was built. `AGENTS.md` holds only the rules. If you connect a tracker after the build, say "Add a team" for a new team. For an existing one, tell the AI the facts: "Team Beta tracks in Azure DevOps, organization YOURORG, project Platform, through az. Update the Team Beta hub and the Tracker Commands note." It shows the before and after, and you say yes.

The rules the vault gives the AI, written into `AGENTS.md` by the build:

- Read freely: list, view, search, query, and anything else that only reads.
- Ask first, showing the exact command: create, update, assign, transition, comment, and anything else that writes.
- Link items by URL. Copy only the key, the title, the state, the owner, and the dates. Never descriptions or attachments.
- When you ask for status, read the tracker first and the vault second, and say which is newer when they disagree.
- A tool that is not signed in or that fails is named in one line, and the AI continues from the vault.
- Never log in, store, or print tokens. Never run a tracker tool during the build.

The tools return keys and numbers, not links. The URL shapes the AI uses to link an item:

- GitHub issue: `https://github.com/<owner>/<repo>/issues/123`. A pull request uses `/pull/123`.
- GitHub Project: `https://github.com/orgs/<org>/projects/<number>`.
- Jira: `https://<site>.atlassian.net/browse/KEY-123`.
- Azure DevOps: `https://dev.azure.com/<org>/<project>/_workitems/edit/123`.

The data and token rules are in [Keep it safe](05-keep-it-safe.md).

## GitHub Projects

One tool, the GitHub CLI, serves both GitHub Projects and the repositories. Install it with `brew install gh` on macOS or `winget install --id GitHub.cli --source winget` on Windows; other options are at [cli.github.com](https://cli.github.com/). Docs: [cli.github.com/manual](https://cli.github.com/manual/).

The `gh project` commands work with the current GitHub Projects and need one extra token scope, `project`, granted once:

```bash
gh auth login                      # sign in through the browser, once
gh auth status                     # which host and account are active
gh auth refresh -s project         # add the project scope to an existing login
gh auth login --scopes "project"   # or sign in fresh with the scope
```

Read:

```bash
gh project list --owner YOURORG                                   # projects and their numbers
gh project view 7 --owner YOURORG                                 # one project
gh project field-list 7 --owner YOURORG --format json             # its fields, with the Status options
gh project item-list 7 --owner YOURORG --format json --limit 200  # every item; the default limit is 30
gh project item-list 7 --owner YOURORG --query "assignee:@me -status:Done"   # filter on the server; gh 2.87 or newer
gh project item-list 7 --owner YOURORG --field "Status" --field "Priority"   # named fields as columns; gh 2.97 or newer
```

`--query` takes the same syntax as the filter box of the project in the browser: `status:"In progress"`, `-status:Done`, `assignee:@me`, `label:bug`, `is:issue is:open`. Build a filter in the browser, confirm it shows what you want, and copy the text. It needs gh 2.87 or newer and a host that supports it. `--jq` trims the JSON on your side without installing jq. Use `--owner "@me"` for a project under your own account.

Write, always shown first:

```bash
gh project item-add 7 --owner YOURORG --url https://github.com/example-org/checkout-api/issues/123   # add an existing issue or pull request
gh project item-create 7 --owner YOURORG --title "New item" --body "What it is"                        # add a draft issue
gh project item-edit 7 --owner YOURORG --url https://github.com/example-org/checkout-api/issues/123 --field "Status" --value "In progress"   # set a field by name; gh 2.97 or newer
```

Name-based editing and the `--field` columns arrived in gh 2.97.0, and `--query` in 2.87.0. `gh --version` tells you what you have. Older versions address items and fields by node id instead, with `--id`, `--field-id`, and `--project-id` taken from the JSON output. Assignees, labels, and milestones belong to the issue, not to the project, so `item-edit` cannot change them.

Record in the team hub: the owner, the project number, and the name of the Status field with its options, because the Status values feed the five headings of the status report. The three queries for a project are below.

## GitHub repositories

Code lives in several repositories, and the AI runs `gh` from the vault folder, so every `gh` command names the repository with `-R owner/repo` and never depends on the folder it runs in. The repo hub in `Repos/<repo-name>/` records the owner and name; "Read my repos and fill in their hubs" or "Add the repo at [path]" puts it there.

Read, in one repository:

```bash
gh pr list -R example-org/checkout-api --state open
gh pr view 123 -R example-org/checkout-api
gh pr checks 123 -R example-org/checkout-api
gh issue list -R example-org/checkout-api --assignee "@me"
gh issue view 45 -R example-org/checkout-api
gh run list -R example-org/checkout-api --limit 10
gh pr list -R example-org/checkout-api --search "updated:>=2026-10-29"   # what changed since a date
```

Read, across every repository you can see:

```bash
gh search prs --review-requested=@me --state=open   # waiting on my review
gh search prs --author=@me --state=open             # my open pull requests
gh search issues --assignee=@me --state=open        # assigned to me
```

These three are what "Start my day" runs each morning. On GitHub Enterprise Server, `gh search` may not be available; check your version. The AI then runs `gh pr list -R <owner>/<repo>` for each repository listed on `Home.md`.

Write, always shown first: creating a branch, committing (the diff and the message), pushing, `gh pr create` (the title and the body), commenting, closing, and merging. Work happens on a branch, never on the default branch.

## Jira

Two command-line tools work with Jira Cloud. Install one, not both. The Tracker Commands note names the one that is installed, because the two differ in syntax. The saved filters below work in either. Both can use an API token, which you create in your Atlassian account settings under Security, then API tokens. Atlassian's own tool can also sign in through the browser.

### Atlassian CLI, Atlassian's own tool

Install on macOS with `brew tap atlassian/homebrew-acli` and then `brew install acli`. On Windows, download `acli.exe` from the install page. On Linux, use the apt or yum repository on the same page. Docs: [developer.atlassian.com/cloud/acli](https://developer.atlassian.com/cloud/acli/guides/install-acli/). It documents Jira Cloud; for Jira Data Center use jira-cli below.

Sign in through the browser:

```bash
acli jira auth login --web
```

If your account only allows a token, pipe it in once from a file outside the vault and remove the file in the same step. The tool keeps the token in its own secure store.

```bash
acli jira auth login --site "yourcompany.atlassian.net" --email "you@yourcompany.com" --token < token.txt && rm token.txt
```

Read:

```bash
acli jira workitem view ALPHA-123
acli jira workitem search --jql 'filter = "Team Alpha changed 7d"' --limit 50
acli jira workitem search --jql 'filter = "Team Alpha open and blocked"' --json
acli jira workitem search --jql "assignee = currentUser() AND statusCategory != Done" --limit 50
```

Write, always shown first:

```bash
acli jira workitem create --summary "New task" --project "ALPHA" --type "Task"
acli jira workitem transition --key "ALPHA-123" --status "Done"
acli jira workitem comment create --key "ALPHA-123" --body "Comment text"
```

If a command errors, add `--help` to it to see the syntax of your version.

### jira-cli, open source

Install on macOS with `brew tap ankitpokhrel/jira-cli` and then `brew install jira-cli`. On Windows, the project's wiki lists Scoop (`scoop bucket add extras`, then `scoop install jira-cli`) and release binaries. Anywhere with Go: `go install github.com/ankitpokhrel/jira-cli/cmd/jira@latest`. Docs: [github.com/ankitpokhrel/jira-cli](https://github.com/ankitpokhrel/jira-cli).

Keep the token out of the vault. jira-cli can read it from the macOS Keychain or from `.netrc`; use one of those first. The `JIRA_API_TOKEN` variable in your shell profile is the last resort, and it is plain text there. Then run the setup once:

```bash
jira init
```

Choose Cloud, then enter the site, your login, and the default project and board. For Jira Data Center, use a personal access token with `JIRA_AUTH_TYPE=bearer` and choose Local.

Read:

```bash
jira me
jira issue list -q 'filter = "Team Alpha changed 7d"' --plain
jira issue list -a$(jira me) -s~Done
jira issue view ALPHA-123
jira sprint list --current
jira epic list
```

Write, always shown first:

```bash
jira issue create -tTask -s"Title" -b"Description" --no-input
jira issue move ALPHA-123 "In Progress"
jira issue comment add ALPHA-123 "Comment text"
```

### Saved filters

Create the three filters per team in Jira and give them names that say the team and the query: "Team Alpha changed 7d", "Team Alpha open and blocked", "Team Alpha no change 14d". The AI then searches with `filter = "Team Alpha changed 7d"` instead of inventing JQL each time, and you can open the same filter in the browser to see exactly what it sees. A director who wants one view across teams can add a filter that spans them, such as `project in (ALPHA, BETA) AND updated >= -7d`. The leadership roll-up itself is built from the team reports.

## Azure DevOps

The Azure CLI with the Azure DevOps extension. It works with Azure DevOps Services, the cloud service, and not with Azure DevOps Server on premises. A team on Server pastes its update into chat, and the AI logs it with that as its source. Docs: [learn.microsoft.com/azure/devops/cli](https://learn.microsoft.com/en-us/azure/devops/cli/).

Install the Azure CLI if it is not there yet, with `brew install azure-cli` on macOS, `winget install --exact --id Microsoft.AzureCLI` on Windows, or the installer at [learn.microsoft.com/cli/azure/install-azure-cli](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli). Then add the extension:

```bash
az extension add --name azure-devops
```

Sign in with your company account and set the defaults once, so the AI does not need the organization and project on every command:

```bash
az login
az devops configure --defaults organization=https://dev.azure.com/YOURORG project="Platform"
```

The defaults name one project. When a team lives in another Azure DevOps project, its hub says so and the AI passes `--project` on every command for that team.

If your organization requires a personal access token instead, `az devops login --organization https://dev.azure.com/YOURORG` prompts for it, or the tool reads it from the `AZURE_DEVOPS_EXT_PAT` environment variable. Never from a note.

Read:

```bash
az boards query --id <shared-query-id> -o table                        # one of the team's three shared queries
az boards query --id <shared-query-id> --project "Payments" -o table   # a team in another project
az boards work-item show --id 123 -o table
az boards query --wiql "SELECT [System.Id], [System.Title], [System.State], [System.AssignedTo] FROM WorkItems WHERE [System.TeamProject] = @project AND [System.ChangedDate] >= @Today - 7 ORDER BY [System.ChangedDate] DESC" -o table
az pipelines runs list --top 10 -o table                               # only if your pipelines run in Azure DevOps
```

Write, always shown first:

```bash
az boards work-item create --title "Title" --type Task --assigned-to "you@yourcompany.com"
az boards work-item update --id 123 --state Active
```

Shared queries do the heavy lifting. Create the three per team under Boards, Queries, Shared Queries, copy each id from the URL, and record the ids in the team hub. The AI runs `az boards query --id` with them and never has to write a query. When a team's items span projects, turn on Query across projects in the query editor. `-o table` gives a readable table; `--query` with a JMESPath expression picks fields.

## The three queries, tracker by tracker

Every team hub records the same three queries. Keep the names plain and consistent, so "Record these queries in the Team Alpha hub" has nothing to guess. Team Alpha is the example throughout.

GitHub Projects, recorded as the owner, the project number, the Status field name, and a filter string per query:

- Changed in the last 7 days: `item-list` has no changed-since filter, so this one runs on the team's repositories instead: `gh pr list -R example-org/checkout-api --search "updated:>=2026-10-29"`, with the date computed each time. `gh issue list` takes the same `--search`; check your version.
- Open and blocked: `--query "-status:Done status:Blocked"`, with whatever your Status option for blocked is called.
- No change in 14 days: build it in the project's filter box in the browser and copy the text; check your version for a qualifier on last update. If the filter box cannot express it, record a marked blank and the report says so.

Jira, recorded as three saved filter names:

- Changed in the last 7 days: `project = ALPHA AND updated >= -7d`
- Open and blocked: `project = ALPHA AND statusCategory != Done AND status = Blocked`, or a flag or a label if that is how your workflow marks blocked.
- No change in 14 days: `project = ALPHA AND statusCategory != Done AND updated <= -14d`

Azure DevOps, recorded as three shared query ids, built in the query editor. Several teams usually share one project and are told apart by Area Path, so every query also filters on the team's area, and the team hub records that path next to the query ids:

- Changed in the last 7 days: Team Project is the team's project, Area Path is under the team's area, and Changed Date >= @Today - 7.
- Open and blocked: Area Path under the team's area, State not in your closed states, and whatever marks blocked in your process, a Blocked field, a tag, or a state.
- No change in 14 days: Area Path under the team's area, State not in your closed states, and Changed Date <= @Today - 14.

The assigned-to-me query, one per tracker, recorded under Trackers and tools in `Home.md`: GitHub Projects `--query "assignee:@me -status:Done"`; Jira `assignee = currentUser() AND statusCategory != Done`, saved as a filter; Azure DevOps a shared query with Assigned To = @Me and State not in your closed states; GitHub repositories `gh search issues --assignee=@me --state=open`.

## What to ask once it works

For a manager, PM, or director:

- "Status report for Team Alpha for this week." The AI runs the three queries, reads the check-in log, and drafts the five headings with a source on every line. See [Weekly status report](../prompts/weekly-status-report.md).
- "Weekly status for all my teams."
- "Log this check-in for Team Alpha: [your lines]." See [Team check-in](../prompts/team-check-in.md).
- "Which items for Team Alpha changed state in the last 7 days? Group them by owner."

For a developer:

- "What is assigned to me and open, across my repositories?"
- "Which of my pull requests have waited on review for more than two days?"
- "Where did we leave off on checkout-api?"
- "What did I ship this week?"

"Start my day" runs the morning set for both: your open pull requests, the ones waiting on your review, the items assigned to you through the named queries, and each team's blocked query. See [Working day to day](04-working-day-to-day.md).

## Troubleshooting

- Not signed in, or a 401 error: run the sign-in command again. Tokens expire. For gh, `gh auth status` says which host and account are active.
- "not a git repository", or the wrong repository answered: a `gh` command ran without `-R`. Check that the repo hub records `owner/repo`, and ask the AI to fix the Tracker Commands note.
- `gh project` complains about the token or the scope: `gh auth refresh -s project`.
- `gh project item-list` rejects `--query` or `--field`: your gh is older than 2.87 or 2.97. Update it, or use `--format json` and let the AI filter with `--jq`.
- `gh search` is not available: GitHub Enterprise Server. The AI falls back to `gh pr list -R` per repository.
- The AI says the command is not found: open a new terminal and check that the tool runs there. It must be on the path of the shell the AI uses.
- Huge output: narrow by date, add `--limit`, `-L`, or `--top`, and use `-o table` or `--plain`.
- The AI invents a query that fails: give it a saved query or filter by name instead, and record it in the hub.
- The wrong Jira tool: the Tracker Commands note names one of the two. If it names the one you did not install, say so and the AI corrects the note.
- Azure DevOps returns nothing for a team: the team lives in another project. Record the project in the team hub so the AI passes `--project`.
- A command errors on a flag: add `--help` to it to see the syntax of your version.

Next: [Working day to day](04-working-day-to-day.md).
