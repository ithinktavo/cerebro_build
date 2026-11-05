# Playbook: developers

Your code stays in GitHub. The vault is two things. It is your own notebook, and it is the context every AI tool reads before it touches a repository: where the code is, how to run it, what was decided and why, and where you left off. It links to commits, pull requests, issues, and tracker items by URL and never copies them.

## What to tell the AI in your profile

The build prompt, [prompts/build-work-vault.md](../prompts/build-work-vault.md), starts with a profile. A developer fills in:

- Roles: developer, tech lead, or architect. Any of these, or one named repository, turns on the Developer module, the `Repos/` folder.
- Repositories, one line each: local path and GitHub URL.
- Projects, one line each: name, goal, and which repositories they touch.
- Trackers: GitHub Projects (owner and project number), Jira (site, and whether you use `acli` or `jira`), or Azure DevOps (organization and project), and which tools you are signed in to from the terminal.
- The tools that read the folder (Claude Code, Codex, GitHub Copilot CLI, GitHub Copilot in VS Code) and the chat tools you also use.
- Whether you lead a team or owe a report upward. Either one adds the Teams or Reports module to the same vault.
- The one thing you are tired of re-explaining to AI tools.

Leave blank what you do not know; a blank becomes a marked blank, never a guess. The build runs no git or gh command, so the repo hubs come out with blanks such as `_left blank, needs gh_`, filled in by your first request afterwards.

## What you get

- `Repos/<repo-name>/<repo-name>.md`: one hub per repository, named exactly like the repository on GitHub, so `example-org/checkout-api` becomes `Repos/checkout-api/checkout-api.md`. It is the one place in the vault where lowercase and hyphens are allowed. Its sections: Current state with a date; Repository (local path, GitHub URL, default branch, and the commit the hub was read at); Serves (the projects it serves, with a link to the project hub where the deploy order lives); Architecture, ten lines stamped with that commit; Documents to read, paths rather than copies; Run and test; Conventions; Gotchas; Live views, the exact `gh` commands for your open pull requests with their checks, the ones awaiting your review, and failing workflow runs, each with `-R <owner>/<repo>` so that no command depends on the folder it runs in; Notes in this folder. The results of the Live views are never stored. Nothing is mirrored from the repository by default; the hub points at documents instead of copying them.
- `Projects/<Name>/<Name>.md`: the goal, Current state with a date, the repositories it touches with the part each serves, the branch, the pull request, and the deploy order, the tracker and its named queries, Milestones, Next steps with owners, Waiting on, Risks, Open questions, and links to its decisions.
- One running log per project, `YYYY-MM-DD <Name> Log.md`, newest entry at the bottom, one entry per session, in the same shape every time: `## YYYY-MM-DD`, then What happened, Decided, Next, Waiting on, Links (commits, pull requests, issues, tracker items by URL), Source. A repository gets a log of its own on first need, for work that belongs to no project.
- Decision notes, dated, `type: decision`: Context, Decision, Alternatives, Consequences, Decided by and when, Status. The alternatives are kept so the reasons survive the people. A decision that belongs in a repository goes there through a pull request, and the hub links it by URL.
- Design notes, `type: plan`, before non-trivial code, and incident notes, tagged `incident`, in the repository's folder.

The AI keeps the parts of a repo hub that describe the repository as it is, without asking, and reports what it changed. Gotchas it proposes. Decisions, design notes, and anything you wrote it changes only after showing the before and after and getting your yes.

## How projects map to repositories

A project spans repositories. Its hub lists each one with the part it serves, the branch the work is on, the pull request, and the deploy order: infra first, then the service, then the web client, for example. That standing order lives in the project hub; a design note records the merge order for the one change it describes. A repository shared by several projects has one hub, linked from every project that uses it. Ticket-sized work is a log entry, not a project. A standing responsibility, such as owning a service, is a project whose Goal says ongoing. Session entries go in the project log. A repo log is created on first need and holds only work that has no project.

## Teach the AI your repositories

- "Read my repos and fill in their hubs": the first request after the build. For each repository in your profile, the AI reads the README, the structure, the build files, and the entry points, fills in the hub, and records the commit it read.
- "Add the repo at [path]": a new folder and hub under `Repos/`, which is created on first use if the module was off.
- "Refresh the hub for [repo]": when the commit moved or 30 days passed. Before relying on a hub, the AI checks the current commit; if it moved, or the hub is older than 30 days, it re-reads the repository first and says so. When the repository contradicts a note, it updates the AI-maintained part and leaves your words alone.
- "Scaffold a new service like checkout-api, at [path], for [purpose]": the payoff of a good hub. The AI proposes the layout from the hub's Architecture, Conventions, and Key files, and a design note comes first, before any file is written.

Infrastructure code, a shared library, or a module repository follows the same pattern: a repo hub for the repository the pieces come from, a design note before any code, pinned versions and no secrets in the project's repository, and a decision note and a log entry to close the loop.

## A coding session

1. Open the AI tool on the vault and say "Start on [project]" or "Where did we leave off on [repo]?". The AI reads the hub and the last three log entries. In each repository the hub names, it checks the working tree, the current branch, the last ten commits, and the open pull requests with their checks. It reads the linked tracker item, refreshes the hub's Current state, and answers in ten lines: where you left off and when, what moved since, what is next, what is waiting.
2. Work. Before non-trivial code the AI writes a design note: Problem, Constraints, Options considered, Chosen approach, Repos touched and merge order, Rollout and rollback, Open questions, Status. It waits for your yes before touching a repository. Then it works on a branch, never on the default branch, shows the diff and the message before a commit and the title and body before a pull request, checks for secrets before every commit, and never force-pushes, rewrites shared history, deletes branches, or changes repository settings.
3. "Draft the PR for this branch": the AI reads the diff against the default branch, the log entries, the ticket, and the repository's pull request template, shows the title and body, opens the pull request after your yes, and records the URL.
4. "Close the session": the AI drafts the log entry from the commits since the session started and your open pull requests in the repositories named in the session or in the project hub, appends it to the project log, or to the repo log for work with no project, updates Current state and Next steps, proposes new Gotchas for the repo hub, adds one `AI:` pointer line to today's Log, and reports what changed.

An incident gets its own dated note in the repository's folder, tagged `incident`, with the pull requests, workflow runs, and tracker items linked by URL. The hub links the note, and what the incident taught goes into Gotchas.

On your reporting day, "Close the week" runs "What did I ship this week?": merged pull requests by repository, closed tickets, and the week's log entries. When your lead wants a status in the five standard headings, ask for a status report on the project; the headings and the sourcing rules are in [prompts/weekly-status-report.md](../prompts/weekly-status-report.md).

## Your own notes

- Today's note, `Daily/YYYY-MM-DD.md`, has two sections, Plan and Log. "Start my day" creates it and adds up to ten `AI:` lines under Plan, each with its source: unchecked items from yesterday, Next steps and Waiting on from your hubs, your open pull requests and the ones waiting for your review, and the items assigned to you in your trackers. "Start my day, vault only" skips the tracker reads. Every line the AI writes starts with `AI:`. It never edits, reorders, or ticks a line of yours.
- "Add to today: [line]" appends your words to the Log as they are. Type into the Log all day: what you did, a gotcha, a decision, an idea, a to-do.
- "Close my day" shows a filing table for the day's Log lines, and one yes applies it: a gotcha goes to the repo hub, a decided line becomes a decision note, an idea with a title becomes a note in `Notes/`, a line that belongs in a tracker is shown as a command, and the rest stays. It also offers to close any session not closed today.
- `Notes/` holds ideas and learning notes, tagged `idea` or `learning`. `Library/` holds what others could reuse: how-tos, snippets, checklists, standards. A learning note moves to `Library/` once it is reusable.
- "Write this week's review" writes `Notes/YYYY-MM-DD Weekly Review.md` from the week's daily notes, logs, and shipped list: What moved, What stalled, Promises kept and not kept, What to drop, Next week's three.

The capture table, with where each kind of line goes, is in [docs/04-working-day-to-day.md](../docs/04-working-day-to-day.md).

## Which tool

- Claude Code (in the terminal, or the Code tab of the Claude desktop app), Codex, GitHub Copilot CLI, and GitHub Copilot in VS Code with the vault as the workspace can open the vault folder and read its rulebook. Setup and the check for each are in [docs/02-connect-ai-tools.md](../docs/02-connect-ai-tools.md).
- A session you start inside a repository does not read the vault's rulebook on its own. [Connect your AI tools](../docs/02-connect-ai-tools.md) has the two routes: start in the vault and add the repository with `--add-dir`, which Claude Code, Codex, and Copilot CLI all have; or start in the repository with the one-line pointer the build prints for `~/.claude/CLAUDE.md`, `~/.codex/AGENTS.md`, or `~/.copilot/copilot-instructions.md`, and add the vault with `--add-dir` when you need to write there. Copilot in VS Code reads the `AGENTS.md` at the workspace root, so open the vault as the workspace for vault work and attach the hub files for code work. Check once with "Read AGENTS.md and tell me the reading order".
- Claude chat, ChatGPT, and Microsoft 365 Copilot cannot open the folder. "Context pack for [hub]" prints one block to paste as the first message in Claude chat or ChatGPT: how you work with AI, Current focus, the hub, the last three log entries, each linked repo hub's Run and test, Conventions, Gotchas, and Architecture, and the Live views run now. Whatever comes back, you paste to the vault tool with "from [tool], [date]" as its source. Microsoft 365 Copilot is where a pasted status lands, in Outlook, Teams, Word, or Loop; it does not read the vault.
- When a repository carries its own `AGENTS.md` or `CLAUDE.md`, that file governs the code. The vault's rulebook governs anything written in the vault.

## Trackers

Each project hub records its tracker, the command-line tool, and its named queries. The exact commands live in `Library/YYYY-MM-DD Tracker Commands.md`; `AGENTS.md` holds only the rules. Read commands run freely. Write commands, such as creating, assigning, or transitioning an item, are shown first and run after your yes. Items are linked by URL, and the AI copies only the key, title, state, owner, and dates. When you ask for status, it reads the tracker first and the vault second, and says which is newer when they disagree. A tool that is not signed in gets one line saying so, and the AI continues from the vault.

- `gh` for GitHub repositories, pull requests, issues, and workflow runs, each command with `-R <owner>/<repo>` from the hub.
- `gh project` for a GitHub Projects board. It needs the `project` scope on your login, added once:

```
gh auth refresh -s project  # add the project scope to an existing gh login
gh project item-list <number> --owner <org> --query "assignee:@me -status:Done"  # your open items on a board; needs gh 2.87.0 or newer
```

- `acli` or `jira` for Jira. `az boards` for Azure DevOps work items. Code is on GitHub, so nothing from Azure Repos is needed.

Sign-in and the full command list per tracker are in [docs/03-connect-work-trackers.md](../docs/03-connect-work-trackers.md).

## Requests to try

1. "Read my repos and fill in their hubs."
2. "Where did we leave off on [repo]?"
3. "Draft the PR for this branch."
4. "Close the session."
5. "What did I ship this week?"

Next: build your vault with [prompts/build-work-vault.md](../prompts/build-work-vault.md), then follow [prompts/first-week.md](../prompts/first-week.md). If you also lead a team, read [roles/pm-director.md](pm-director.md); one vault holds both.
