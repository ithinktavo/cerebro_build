# Playbook: managers, PMs, and directors

For team leads, managers, PMs, directors, and program or governance leads. The job has three parts: track teams, run initiatives that span them, and report upward. The vault gives every team a hub and a check-in log, reads your tracker through three named queries, and turns both into status reports, a leadership roll-up, and a monthly review that you edit instead of write. Every line the AI writes ends with its source.

The daily work needs no terminal. The one-time sign-in to a tracker's command-line tool does, and [Connect your work trackers](../docs/03-connect-work-trackers.md) shows how; until then every ritual still works vault-only. The first section says which tool to open.

## Which tool

Any AI tool that can open the vault folder does everything on this page. The routes without a terminal come first.

- The Code tab of the Claude desktop app. Open the vault folder and keep Manual mode, so Claude shows each edit before it is made. Nothing else to install. It needs a paid plan.
- GitHub Copilot in VS Code, with the vault folder open as the workspace. An agent session reads `AGENTS.md` at the workspace root on its own and, under its default permissions, asks before running a command it has not been allowed to run. Check your version.
- Codex in the ChatGPT desktop app, pointed at the vault folder, if your admin has turned local work on. Check your version.
- In a terminal: `claude`, `codex`, or the GitHub Copilot CLI, started in the vault folder.

Claude chat, ChatGPT, and Microsoft 365 Copilot cannot open the folder. For a quick question away from the vault, say "Context pack for Team Alpha" to a tool that can, paste the block it prints as the first message, and paste the answer back with "from [tool], [date]" as its source. A pack never includes one-on-one logs unless you ask for them. You can also keep copies of `Me.md`, `Home.md`, and the hub in a Claude Project or a ChatGPT Project. Setup, sign-in, and what each tool accepts: [Connect your AI tools](../docs/02-connect-ai-tools.md) and [prompts/context-pack.md](../prompts/context-pack.md).

## What the vault holds for you

**A hub per team**, `Teams/Team Alpha/Team Alpha.md`, created together with its check-in log. Its sections, in order:

- Current state, as of a date, one line per fact with its source.
- Team: reports through, and members by name and role only.
- Works on: one line per project with a link.
- Cadence: standup, sync, one-on-one days, reporting day. "Start my day" reads it for today's commitments.
- Tracker and queries: the system, the command-line tool, the board URL, and the three named queries.
- Priorities, as of a date, each with its source.
- Milestones, from its projects.
- Next steps, each with an owner.
- Waiting on: who, what, since when.
- Risks: risk, owner, raised date, status, mitigation.
- Open questions.
- Decisions, one line each, linking the decision note.
- Reports: the recipe line (audience, day, destination), then the team's status reports, newest first.
- Notes in this folder, including the check-in log and the one-on-one logs if you opted in.

The check-in log is a running note, for example `Teams/Team Alpha/2026-11-05 Team Alpha Log.md`, with the newest entry at the bottom. Every entry has the same shape: `## 2026-11-05`, then What happened, Decided, Next, Waiting on, Links, Source.

**A project per initiative**, `Projects/Checkout Migration/Checkout Migration.md`, for anything with a finish line that is bigger than one ticket, whether one team or five work on it. The hub carries the goal, a dated current state, the people by name and role, links to the tracker and the documents, one line per team with what it owns, milestones with date and status, next steps with owners, waiting on, open questions, risks, and decisions. It has its own running log. A standing responsibility, such as a governance program, is a project whose Goal says ongoing. Ticket-sized work is a log entry, not a project.

Teams and projects point at each other, one line each:

```
Teams/Team Alpha/Team Alpha.md, under Projects this team works on:
- [[Checkout Migration]]: owns the API work; next milestone M2 on 2026-12-15 (as of 2026-11-05)

Projects/Checkout Migration/Checkout Migration.md, under Teams:
- [[Team Alpha]]: API and data migration
- [[Team Beta]]: web checkout
```

The roll-up walks teams and then their projects, or initiatives first. Your profile says which way leadership reads.

**Decision records**, dated `type: decision` notes in the project or team folder: Context, Decision, Alternatives, Consequences, Decided by and when, Status. They are the most valuable notes in the vault. Six months later someone asks why, and the answer is there. Say "Write a decision note: we decided X because Y; the alternatives were Z". Or paste raw notes with "Turn these notes into a meeting note for Checkout Migration: [paste]" and get a meeting note plus one decision note per decision, with the actions landing under Next steps or Waiting on in the hub. The prompt is in [prompts/meeting-notes.md](../prompts/meeting-notes.md).

**A standards library**, `Library/`, for definitions, a glossary, checklists, and the standards your teams follow. Link to the source of record; never copy it. When the official document lives in SharePoint or Teams, ask Microsoft 365 Copilot to summarize it, then paste the summary into the Library note with the document's link and the date as its source. The Tracker Commands note lives here too.

**The Reports module**, `Reports/`, switches on when you owe a recurring report across more than one team or project, or when your roles include manager, PM, or director and you named a report in your profile. It holds three things. The Reports hub, `Reports/Reports.md`, with one recipe per recurring report (audience by role, cadence and day, headings, sources, destination, link to the last one) and the list Open asks of leadership (what, who decides, since when), refreshed on every roll-up. The weekly roll-ups, `Reports/YYYY-MM-DD Weekly Roll-Up.md`. The monthly reviews, `Reports/YYYY-MM-DD Monthly Review.md`. Without the module, a one-off roll-up goes to `Notes/` with the tag `rollup`.

## Getting status without adding a process

Three sources, in this order. Nobody writes a status email for you.

**1. The tracker**, through three named queries per team:

| Query | What it feeds |
| --- | --- |
| Changed in the last 7 days | Done and In progress |
| Open and blocked | Blocked or at risk |
| No change in 14 days | What has stalled |

The hub records each query by saved filter name (Jira), shared query id (Azure DevOps), or project number and field (GitHub Projects). The AI runs it by that name with the sign-in you already have, so it never invents a query. If your tracker makes only two easy, start with changed in the last 7 days and everything open, and add the third when you can. Create them in the tracker, then say "Record these queries in the Team Alpha hub". Sign-in and the commands for each tracker are in [Connect your work trackers](../docs/03-connect-work-trackers.md). A fourth query, assigned to me and open, is recorded once per tracker under Trackers and tools in `Home.md` and feeds "Start my day".

For a GitHub Projects board, the hub records the owner, the project number, and each query's filter text, because that is what `gh project item-list` takes. The filter syntax is the same as the board's own filter box, so build each query there and copy its text. The `gh project` commands need one extra token scope:

```
gh auth status                    # which account is signed in
gh auth refresh -s project        # add the project scope to that login, once
gh project list --owner YOURORG   # find the project number
gh project item-list 7 --owner YOURORG --format json --limit 100 --query "-status:Done"     # everything open; --query needs gh 2.87.0 or newer, check your version
gh project item-list 7 --owner YOURORG --format json --limit 100 --query "status:Blocked"   # or label:blocked, however your board marks it
```

The teams' code is on GitHub, so the rulebook also lets the AI read the repositories a hub names, through `gh`: pull requests still open, issues closed this week, failing checks. Read-only commands run freely. Anything that writes is shown as the exact command first and waits for your yes.

**2. Your check-ins.** After a standup, a sync, or a one-on-one, say "Log this check-in for Team Alpha: cutover moved to Thursday; waiting on the security review since Monday; Alex Example out next week." The AI adds a dated entry to the check-in log in your words, with "said in chat" and the date as its source. It shows the hub edits the lines imply (priorities, Waiting on, Risks) as a before and after, for one yes. It offers a tracker item where a line deserves one, with the command shown. It lists what you promised. Or type the lines into today's Log and let "Close my day" file them. The prompt is in [prompts/team-check-in.md](../prompts/team-check-in.md).

**3. The team's own words.** Where a team already posts a weekly update in Teams or sends one in Outlook, paste it, or ask Microsoft 365 Copilot for a summary of the channel or thread and paste that. The AI logs it with "from the team's update, [date]" or "from Microsoft 365 Copilot, [date]" as its source. Three to five lines, never a transcript, and never calendar or email text; the AI never reads your inbox. Microsoft 365 Copilot does not read the vault folder on your computer. A director tracks each team the same way, with the managers' pasted updates logged as "from [role]'s update" with the date.

The vault never claims more than its sources say.

## The weekly status report

Say "Weekly status for all my teams", or name one team. For each team the AI:

1. Runs the three named queries and copies only the key, title, state, owner, and dates.
2. Reads the check-in log entries of the last seven days.
3. Reads the hub's Current priorities, Waiting on, Risks, Open questions, and the Milestones of its initiatives.
4. Reads last week's report, so that Next becomes Done or In progress and what did not happen is named.

The draft has the same five headings every time: Done, In progress, Blocked or at risk, Decisions needed, Next. One line per item, under a page, no adjectives. Every line ends with its source: a tracker item by URL, a note by link, or "said in chat" with the date. The draft states the delta since last week and says where the tracker and the vault disagree and which is newer. After your yes it is saved as `Teams/Team Alpha/2026-11-06 Team Alpha Status Report.md`, `type: report`, and listed in the hub.

```
## Blocked or at risk
- Security review of the cutover plan not started, requested 2026-10-29. Source: https://github.com/example-org/checkout-api/issues/412
- Alex Example out next week; API work pauses. Source: said in chat, 2026-11-05
```

With the draft you get a paste-ready copy: links turned into plain titles, tracker URLs kept, sources moved to a short list at the end. You edit it in ten minutes instead of writing it in an hour. The prompt is in [prompts/weekly-status-report.md](../prompts/weekly-status-report.md).

## The roll-up and the monthly review

"Roll up this week for leadership" writes `Reports/2026-11-06 Weekly Roll-Up.md` from this week's team and project reports, every hub's Risks and Open questions, the recipe in the Reports hub, and last week's roll-up. In short: one block per team, then the things you need decided. In full: a three-line headline; one block per team or initiative, grouped the way the recipe says leadership reads, with the delta since last week and a traffic state the AI proposes and marks as a proposal until you set it; Risks new or changed, with owner and age; Decisions needed, with the ask, who decides, and by when; Milestones in the next 30 days; a link to each team report. It declines when a team status is missing and offers to draft it first. Each run refreshes Open asks of leadership in the Reports hub.

"Monthly review for October" writes `Reports/2026-11-02 Monthly Review.md`: outcomes against plan from the hubs' Milestones, decisions made with their status, risks opened and closed, priorities that changed, next month, asks.

Two requests run the whole sequence:

- "Close the week", on your reporting day: the team statuses; "What did I ship this week?" if you have repositories; the roll-up; then "Write this week's review" (see Your own notes below).
- "Close the month": the monthly review; "What is stale or contradictory?"; then proposals for your yes: projects to archive, a rollover for any running log past a few hundred lines, a new Current focus for `Home.md`.

The flow is in [prompts/close-the-week.md](../prompts/close-the-week.md).

## Where reports go

Delivery is yours. Paste the paste-ready copy into Outlook, Teams, Word, or Loop, where Microsoft 365 Copilot can fit it to the house format. The AI never emails or posts to people. Microsoft 365 Copilot is where reports go, not a reader of the vault. For a deck, ask for a slide outline: a `type: plan` note that Obsidian's core Slides plugin presents.

## Keeping yourself honest

- "What is waiting on me?" Waiting on in every hub where you are the one who owes, plus review requests if you have repositories.
- "What am I waiting on, and since when?" Waiting on in every hub, oldest first.
- "Which open items across the queries have had no change in 14 days?" The third query, run for every team.
- "What did I promise this week?" Daily notes and check-in logs.
- "What is stale or contradictory?" Hubs past 30 days, Waiting on and open asks older than 30 days, outdated plans without a successor, notes that disagree.

"Start my day" does part of this every morning: Waiting on older than seven days, teams with no check-in this week, hubs past 30 days, the inputs a report due this week still lacks, and each team's blocked query. It appends at most ten `AI:` lines under Plan, each with its source.

## 1:1s

One-on-one logs are off by default. Turn them on with "1:1 notes in the vault: yes" in your profile. Each direct report then gets one running log in the team folder, named like every other log, for example `Teams/Team Alpha/2026-11-05 Alex Example One-on-One Log.md`. Write "One-on-One", not "1:1": a file name cannot contain a colon. Each entry has Their topics, Mine, Decisions, Actions with owners, Waiting on me, Waiting on them. The template prints the boundary line: nothing about performance, pay, health, or personal matters.

"Prepare my 1:1 with Alex Example" reads their log, the team hub's Waiting on and Risks, and their tracker items this week. Work topics only. Only what concerns the team's work goes from a one-on-one into the check-in log.

There is no People folder. A person appears as a name and a role in a team hub, and nowhere else. Performance, compensation, health, and personal matters live in the HR system, never in the vault. The rulebook tells the AI to say so and leave them out when something like that is pasted. The same goes for what you govern: no samples of the data, no customer records, nothing a classification rule keeps out of general systems. A link to the source of record is enough. A one-on-one with your own manager, a peer, or a skip-level has no team folder: it becomes a meeting note in `Notes/`, under the same work-only rule. See [Keep it safe](../docs/05-keep-it-safe.md).

## Your own notes

The vault is your notebook before it is a reporting machine.

- Today's note, `Daily/2026-11-05.md`, has Plan and Log. Promises, follow-ups, and what a standup said go into Log in your words, one line each. "Close my day" shows where each line belongs, and one yes files the batch. Away from Obsidian, "Add to today: [line]" appends your words as they are. If you missed a day, "Catch me up" files every unclosed day in one pass.
- "Write this week's review" saves `Notes/2026-11-06 Weekly Review.md`, tag `review`: What moved, What stalled, Promises kept and not kept, What to drop, Next week's three, and a paragraph for your own team's update. It proposes new Current focus lines for `Home.md`, for your yes.
- `Library/` holds your own checklists: a release checklist, a review checklist, the questions you ask in every planning meeting.
- `Notes/` holds ideas with a title, one-off meeting notes, and prep for your own manager: "From this week's roll-up and the Open asks of leadership, give me the three things to raise with my manager." Nothing is saved unless you ask.

The daily and weekly rhythm is in [Working day to day](../docs/04-working-day-to-day.md).

## What to tell the AI in your profile

The build prompt, [prompts/build-work-vault.md](../prompts/build-work-vault.md), designs the vault from a short profile. Fill in:

- Your roles: manager, PM, director, program lead, in any mix. Add developer if you also write code.
- Teams, one line each: the name and what it reports through. Projects or initiatives: name, goal, which teams.
- Who you report to, and who reports to you.
- The tracker per team or project: GitHub Projects with owner and project number, Jira with its site and whether you use acli or jira-cli, or Azure DevOps with organization and project. Which tools you are signed in to from the terminal, or none yet.
- The reports you owe: audience by role, cadence and day, where it goes, and whether leadership reads by team or by initiative.
- Your week: standups, one-on-one days, staff or planning meetings, review days.
- Note habits: whether you keep a daily note, and whether your to-dos live in the vault or only in the tracker.
- One-on-one notes in the vault, yes or no. The default is no.
- The one thing you are tired of re-explaining to AI tools.

Leave blank what you do not know. A blank becomes a marked blank and a question, never a guess. In Design first mode the AI may ask up to five questions before writing anything: whether X is a team, a project, or a repository; which tracker is the record when two are named; whether to group teams by manager when you name more than about twelve; whether leadership reads by team or by initiative. A team that arrives later is added with "Add a team" and the same facts.

## Requests to try

1. "Add a team: Team Beta, reports through the head of platform. Members: Alex Example, tech lead; Sam Example, PM. Tracker: GitHub Projects, owner YOURORG, project 12."
2. "Log this check-in for Team Alpha: cutover moved to Thursday; waiting on the security review since Monday; Alex Example out next week."
3. "Weekly status for all my teams."
4. "Roll up this week for leadership."
5. "What is waiting on me, and what has not moved in two weeks?"

If you also write code, read the [developer playbook](developer.md). One vault holds the Developer module, the `Repos/` folder, next to Teams and Reports, with one daily note and one set of rituals, and "Close the week" adds "What did I ship this week?" between the team statuses and the roll-up.

If you also write the stories your teams build and want a spec per story that the developers' tools read first, read [roles/product-owner.md](product-owner.md). The Specs switch joins the same vault next to Teams and Reports, and a developer's spec question on a story shows up in your morning.

Next: [Set up Obsidian](../docs/01-set-up-obsidian.md).
