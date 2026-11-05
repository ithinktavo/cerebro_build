This is the design the AI proposed for the sample persona Alex Example before building anything, printed in chat as the first reply to the build prompt.
Alex replied "yes", and the vault in `sample-vault/` is what the AI built from it.

## The profile Alex filled in

- Name or handle: Alex Example. Roles: developer, engineering manager.
- Teams: Team Alpha, reports through the Director of Platform. Team Beta, reports through the Director of Platform. Projects: Checkout Migration, goal: move checkout to the new service by the end of the quarter; Team Alpha; repos checkout-api and web-storefront. Observability Rollout, ongoing; Team Beta. Repositories: /Users/alex/code/checkout-api at https://github.com/example-org/checkout-api; /Users/alex/code/web-storefront at https://github.com/example-org/web-storefront.
- I report to the Director of Platform. Reporting to me: two tech leads.
- AI tools that read this folder: Claude Code, Codex, GitHub Copilot CLI, GitHub Copilot in VS Code. Chat tools I also use: ChatGPT, Microsoft 365 Copilot.
- Trackers: Team Alpha and Checkout Migration use GitHub Projects (owner example-org, project 7). Team Beta and Observability Rollout use Jira (example.atlassian.net; acli). Signed in from the terminal: gh and acli.
- Reports I owe: weekly status to the Director of Platform, Fridays, posted in Teams; leadership reads by team.
- My week: standup daily at 9:30, 1:1s on Tuesdays, staff meeting Mondays, planning every other Thursday.
- Note habits: I keep a daily note; to-dos in the vault; nothing else to preserve.
- 1:1 notes in the vault: no.
- The one thing I am tired of re-explaining: which repository serves which part of checkout, and the deploy order.
- Operating system: macOS. Mode: Design first.
- How I work with AI: as written in the prompt.

Every "Source: profile, 2026-11-05" line in the sample vault points at this block, and every marked blank is something it leaves open.

# Design for Alex Example's work vault

## 1. Modules

- Developer: on. You named two repositories and your roles include developer.
- Teams: on. You named Team Alpha and Team Beta, and two tech leads report to you. One-on-one logs stay off, as you said.
- Reports: on. You owe a weekly status across two teams and your roles include manager.

## 2. Mapping table

| Item | Module | Links |
| --- | --- | --- |
| Checkout Migration | Project | Team Alpha works it; repos checkout-api and web-storefront; record: GitHub Projects, owner example-org, project 7, shared with Team Alpha |
| Observability Rollout | Project, Goal says ongoing | Team Beta works it; record: Jira at example.atlassian.net through acli, shared with Team Beta |
| checkout-api | Repo | /Users/alex/code/checkout-api; serves Checkout Migration; which part and its place in the deploy order live in the project hub |
| web-storefront | Repo | /Users/alex/code/web-storefront; serves Checkout Migration; same |
| Team Alpha | Team | reports through the Director of Platform; works Checkout Migration; GitHub Projects project 7 |
| Team Beta | Team | reports through the Director of Platform; works Observability Rollout; Jira |
| Weekly status | Report | to the Director of Platform, Fridays, posted in Teams; one report per team, then one roll-up, because leadership reads by team |

## 3. Tree

- `AGENTS.md`, `CLAUDE.md`, `Me.md`, `Home.md`: the rulebook, the Claude Code pointer, your profile, the front door.
- `Daily/`: one note per work day, created by "Start my day". Empty until then.
- `Notes/`: ideas, learning notes, weekly reviews, one-off meeting notes. Empty at the start.
- `Library/`: How to Use This Vault, Vault Design, Tracker Commands, all dated today.
- `Projects/Checkout Migration/`: hub and running log. The checkout fact you are tired of re-explaining lives in this hub.
- `Projects/Observability Rollout/`: hub and running log, because a standing responsibility is a project whose Goal says ongoing.
- `Repos/checkout-api/` and `Repos/web-storefront/`: one hub each, a log on first need. Nothing is read from the repositories until you ask.
- `Teams/Team Alpha/` and `Teams/Team Beta/`: one hub and one check-in log each; status reports and decisions land here. No one-on-one logs.
- `Reports/`: the Reports hub with the recipes and an empty Open asks list; weekly roll-ups and monthly reviews land here.
- `System/Templates/`, `System/Attachments/`, `System/AI/`: 14 templates; files and exports; `AI-Memory.md` and `AI-Log.md`.

## 4. Hubs, templates, and the daily note

- Every hub opens with Current state (dated) and ends with Notes in this folder. Project and team hubs keep Next steps, Waiting on, Risks, Open questions, Decisions; project hubs add Goal, Teams and repos, Tracker, Priorities, Milestones; team hubs add Team (names and roles only), Works on, Cadence, Tracker and queries, Reports. Repo hubs keep Repository, Serves, Architecture stamped with the commit, Documents to read, Run and test, Conventions, Gotchas, Live views. The Reports hub keeps Recipes and Open asks of leadership.
- Templates, 14: Daily Note, Note, Meeting, Decision, Design, Status Report, Weekly Review, Log, Project Hub, Slide Outline, Repo Hub, Team Hub, Roll-Up, Monthly Review. No One-on-One Log template, because 1:1 logs are off; it is added if you turn them on.
- Daily note: `## Plan` with checkboxes and `## Log` with one line per thing in your words, no properties. The morning pulls, for your two roles: carried-over Plan items; Next steps you own and Waiting on older than seven days in every hub; today's cadence (standup 9:30, Tuesday 1:1s, Monday staff meeting, planning every other Thursday); what the Friday status still lacks; teams with no check-in this week; stale hubs; open questions. Then, through gh and acli: your open pull requests, the ones waiting for your review, failing checks, your items in GitHub Projects and Jira through the named queries, and each team's blocked query.

## 5. Report recipes

- Weekly status, Fridays: one `YYYY-MM-DD <Team> Status Report.md` per team with Done, In progress, Blocked or at risk, Decisions needed, Next, every line ending with its source; then `Reports/YYYY-MM-DD Weekly Roll-Up.md` grouped by team, with a paste-ready copy for Teams. Microsoft 365 Copilot fits the house format there; nothing is sent by the AI.
- Monthly review, on request: `Reports/YYYY-MM-DD Monthly Review.md`.

## 6. Rituals, in your names

- Daily: "Start my day", "Start my day, vault only", "Add to today: [line]", "Close my day", "Catch me up".
- Work: "Start on Checkout Migration", "Start on Observability Rollout", "Where did we leave off on checkout-api?", "Where did we leave off on web-storefront?", "Close the session", "Draft the PR for this branch".
- Teams: "Log this check-in for Team Alpha: [lines]", "Log this check-in for Team Beta: [lines]", "Record these queries in the Team Alpha hub", "Record these queries in the Team Beta hub", "Add a team".
- Reports: "Status report for Team Alpha for this week", "Weekly status for all my teams", "Roll up this week for leadership", "What did I ship this week?", "Write this week's review", "Close the week", "Monthly review for [month]", "Close the month", "What is stale or contradictory?".
- Setup and context: "Read my repos and fill in their hubs", "Add the repo at [path]", "Context pack for [hub]" for ChatGPT. Not available: "Prepare my 1:1 with [name]", since 1:1 logs are off.

## 7. Repository paths, first requests, assumptions

- Read only when you later ask: /Users/alex/code/checkout-api and /Users/alex/code/web-storefront.
- First five requests: "Start my day"; "Read my repos and fill in their hubs"; "Record these queries in the Team Alpha hub", after you create the three views and the three Jira filters; "Log this check-in for Team Alpha: [lines]"; "Close my day". On Friday: "Close the week".
- Assumptions: one tech lead per team, names left blank. The project 7 board and the Jira project each hold all of their team's work, so the project hubs reuse the team queries with a filter left blank. The Jira project key, the default branch and current commit of each repository, the planning Thursdays, and the last day of the quarter are marked blanks. No tracker, git, or gh command runs during the build.

## 8. Questions, each with the default a bare yes takes

1. The fact you are tired of re-explaining, which repository serves which part of checkout and the deploy order, lives in the Checkout Migration hub, and each repo hub points to it. Default: yes, as a marked blank for you to fill in.
2. Do Team Beta and Observability Rollout share one Jira project? Default: yes, one project, key left blank.
3. Does GitHub project 7 hold all of Team Alpha's work, or only Checkout Migration? Default: all of it; the project hub filters it by a field left blank.
4. On Fridays, do you post the roll-up or the two team reports in Teams? Default: the roll-up, built from the two team reports, since leadership reads by team.

Reply yes to build with these defaults, or tell me what to change.
