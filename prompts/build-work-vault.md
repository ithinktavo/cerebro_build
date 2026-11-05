# Build prompt: a work vault the AI designs for you

This prompt turns an empty Obsidian vault into your work notebook and the context your AI tools read first. You fill in a short profile, the AI proposes a design for your roles and tools, you say yes, and it builds the whole vault in one pass: the rulebook, your home note, hubs for the real things you own, templates, and the two daily rituals.

## How to use this file

1. Create an empty vault in Obsidian and turn on the Daily notes and Templates core plugins. See [Set up Obsidian](../docs/01-set-up-obsidian.md).
2. Open a tool that can read and write the folder on that vault: Claude Code (in the terminal, or the Code tab of the Claude desktop app), Codex, or GitHub Copilot (the CLI, or VS Code with the vault as the workspace). See [Connect your AI tools](../docs/02-connect-ai-tools.md). Claude chat, ChatGPT, and Microsoft 365 Copilot cannot create files.
3. Fill in the profile between the square brackets. Leave blank what you do not know. A blank becomes a marked blank in the vault and a question for later, never a guess.
4. Keep `Design first`, the default, to read a short design and answer up to five questions before anything is written. Choose `Build now` to skip the design and build with the defaults.
5. Paste everything below the line as your first message. Expect a design to read, then about twenty-five files, then the settings to set in Obsidian. In a mode that asks before each write, expect one approval per file. If the build stops partway, say "Continue the build: compare the tree to the approved design and re-run the verification"; the stop on a non-empty folder is where a resumed build starts, not an error.

---

Build my work vault. This folder is a new, empty Obsidian vault. Read my profile, design the vault for it, and build it as described below. Make sensible choices, cite my profile for every fact you write, and list every assumption at the end.

Before anything else: if the folder holds anything besides the `.obsidian` folder, stop and show me what is in it, and offer to extend what is there by proposing additions only. Take today's date from the system clock (`date +%F` on Mac or Linux, `Get-Date -Format yyyy-MM-dd` on Windows). During the design and the build, run no tracker, git, or gh command and read nothing outside this folder.

## My profile

- Name or handle: [name]. Roles: [developer, tech lead, manager, PM, director, or others, in any mix].
- What I own, one line each. Teams: [team name, what it reports through]. Projects or initiatives: [name, goal, which teams or repos]. Repositories: [local path, GitHub URL].
- I report to [role]. Reporting to me: [roles, or none].
- AI tools that read this folder: [Claude Code, Codex, GitHub Copilot CLI, GitHub Copilot in VS Code]. Chat tools I also use: [Claude chat, ChatGPT, Microsoft 365 Copilot, or none].
- Trackers, one line per team or project: [team or project] uses [GitHub Projects (owner and project number), Jira (site; acli or jira-cli), or Azure DevOps (organization and project)]. Signed in from the terminal: [which tools, or none yet].
- Reports I owe: [audience by role, cadence and day, where it goes; whether leadership reads by team or by initiative; or none].
- My week: [standups, 1:1 days, staff or planning meetings, review days].
- Note habits: [I keep a daily note: yes or no. To-dos: in the vault, or only in the tracker. Anything I already do that must survive.]
- 1:1 notes in the vault: [yes or no; default no].
- The one thing I am tired of re-explaining to AI tools: [one line]. It becomes its own section of `Me.md`, goes into every context pack, and tells you which hub sections to fill hardest.
- Operating system: [macOS, Windows, or Linux].
- Mode: [Design first, or Build now].
- How I work with AI: I give short briefs and expect you to explore. Go by what I mean, not my exact wording. Give me your point of view, with the reason in a line. Lead with the answer. Say what you do not know instead of guessing. Once the vault exists, you ask before changing anything I wrote, you do your own bookkeeping without asking and report it, and you never delete or rename.

## What the vault is for

1. My notebook. One daily note is where everything lands during the day. Ideas, things I learn, and how-tos for myself have a home. Notes I write by hand are mine; you treat them as information and change them only with my yes.
2. The context every AI tool reads first: who I am, what is current, what each project, team, and repository is, what was decided and why, and where we left off.
3. Capture in one place, filing done for me: I type lines, you propose where each one goes, and one yes applies the batch.
4. Reports from sources, not memory: team status, roll-ups, and reviews, every line with its source.
5. GitHub and the work trackers stay the systems of record. The vault links to them and never copies them, and you read them through their command-line tools when I ask.

## The spine every vault has

```
AGENTS.md          the single rulebook, read by Codex and GitHub Copilot on their own; under 200 lines and 32 KiB
CLAUDE.md          pointer for Claude Code: one sentence and four @ lines; no rules
Me.md              who I am, what I own, my week, my note habits, how I work with AI; mine to edit
Home.md            front door: current focus, what to say, one line per hub, trackers and tools, library
Daily/             one note per work day, YYYY-MM-DD.md, from the core Daily notes plugin; no properties
Notes/             anything with a title and no hub: ideas, learning notes, weekly reviews, one-off meeting notes
Library/           reusable knowledge with no single owner: how-tos, checklists, standards, reusable prompts
Projects/          one folder per thing with a finish line, with a hub named like the folder and one running log
System/
  Templates/       one template per kind of note this vault uses
  Attachments/     images and exported deliverables, dated names, linked from a hub
  AI/              AI-Memory.md and AI-Log.md, your working notes
Archive/           created later, with my yes, when the first project finishes
```

## The modules and the rule for each

- **Developer**, when I name a repository or my roles include developer, tech lead, or architect: `Repos/<repo-name>/` with a hub named exactly like the repository on GitHub, the one place lowercase and hyphens are allowed; a running log on first need; incident notes.
- **Teams**, when I name a team or someone reports to me: `Teams/<Team>/` with a hub, a running check-in log created with it, status reports, decisions, and, only if I said yes above, one running one-on-one log per direct report. A direct report who covers several teams gets the log in the first of those team folders, linked from the others.
- **Reports**, when I owe a recurring report across more than one team or project, or my roles include manager, PM, or director and I named a report: `Reports/` with a hub of recipes and open asks, weekly roll-ups, and monthly reviews.

Nothing is built in case. A module I did not trigger is created on first use under the normal rules: "Add the repo at [path]" creates `Repos/`. No other folder kinds exist: no People, Areas, or custom folders. A folder for something new is proposed later, when three notes on one topic pile up in `Notes/`. Someone who is both a developer and a manager gets one vault with all three modules, one daily note, and one set of rituals.

## Design rules

- A hub is named exactly like its folder, states Current state with a date, and links every note in its folder. A project or team hub is created together with its running log; a repo hub gets its log on first need; the Reports hub has none.
- Real names from my profile, with marked blanks such as `_left blank, needs gh_` where you would need a tool. No example folders.
- A standing responsibility is a project whose Goal says ongoing. Ticket-sized work is a log entry, not a project.
- A fact lives in one note. Hubs and `Home.md` quote it with a date and a link.
- Names and roles only for other people. Nothing about performance, pay, health, or personal matters. No secrets, no customer data.

## Hubs

Sections, in this order. Every hub opens with Current state (as of a date, AI-maintained, one line per fact with its source) and ends with Notes in this folder.

- Project hub: Goal; People (owner and stakeholders, name and role only); Teams (one line per team with what it owns); Repos (one line per repo with the part it serves, the branch, the pull request, and the deploy order, which is where that standing fact lives); Tracker and queries; Priorities; Milestones (date, what, status, source); Next steps (checkboxes with owner); Waiting on (who, what, since when); Risks (risk, owner, raised, status, mitigation); Open questions; Decisions (one line each, linking the note); Log (link to the running log).
- Repo hub: Repository (local path, GitHub URL, default branch, read at commit); Serves (the projects, with a link to where the deploy order lives); Architecture (ten lines at most, stamped with the commit); Documents to read (paths, never copies); Run and test; Conventions; Gotchas (dated, each with a source); Live views (the exact `gh` commands; results never stored).
- Team hub: Team (reports through; members by name and role); Works on; Cadence; Tracker and queries; Priorities; Milestones; Next steps; Waiting on; Risks; Open questions; Decisions; Reports (the recipe line, then the reports, newest first). The check-in log and any one-on-one logs are listed under Notes in this folder.
- Reports hub: Recipes (one per recurring report: audience, cadence and day, headings, sources, destination, link to the last one); Open asks of leadership (what, who decides, since when; refreshed on every roll-up).
- `Home.md`: see Files to write.

## The design pass

In `Design first` mode, print the design in chat, under 80 lines, and write nothing until I say yes:

1. Modules on and off, one reason each.
2. A mapping table, one row per thing I own: item, module, links (which repos serve which project, which team works which initiative, which tracker holds what).
3. The tree with my real names and one line of reason per folder.
4. The hub sections you will keep, the templates, and the daily note's two sections, with what the morning will pull for my roles.
5. The report recipes with their cadence, if any.
6. The rituals, with the exact words, in my names.
7. The local repository paths you will read only when later asked, the first five requests, and your assumptions.
8. At most five questions, each with the default a bare yes takes. Ask only when the answer changes the structure and my profile left it open: is X a team, a project, or a repo; which tracker is the record when two are named; 1:1 logs or not; flat teams or grouped by manager when more than about twelve are named; whether leadership reads by team or by initiative. Never ask for URLs, ids, tokens, anything already in my profile, or permission for your own bookkeeping.

End with: "Reply yes to build with these defaults, or tell me what to change." Rounds continue until I say yes. In `Build now` mode, skip the pass, take every default, build, print the same summary afterwards, and put the unasked questions in `AI-Memory.md`.

## The daily note and the two daily rituals

The daily note is `Daily/YYYY-MM-DD.md`, with two sections: `## Plan`, checkboxes for today, and `## Log`, one line per thing as it happens, in my words. No properties. Starting a Log line with `[[Hub]]` is an optional hint about where it belongs; you use it when present and infer the home from the words when absent.

Ownership, written into `AGENTS.md`: you never edit, reorder, or tick a line I wrote; every line of yours starts with `AI:`; "Add to today: [line]" appends my words verbatim; the only change you ever make to my line is the filing marker ` → [[Hub]]` appended after my yes; you re-read the note right before every write.

**"Start my day"**: take the date from the clock, search the vault for today's note, and create it from the template if none exists. If any daily note since the last `AI: closed` marker has unfiled Log lines, run "Catch me up" first. Read yesterday's unchecked Plan items (carry them with the date first seen; on the third morning, flag it: give it a date in a hub or drop it), every hub's Next steps owned by me and Waiting on older than seven days, my week and each team's cadence for today's commitments and what inputs a report due this week still lacks, teams with no check-in this week, hubs whose Current state is past 30 days, and the open questions in `AI-Memory.md`. Then the trackers: my open pull requests and the ones waiting for my review, items assigned to me through each tracker's assigned-to-me query, and each team's blocked query. A tool that is not signed in or that fails gets one `AI:` line saying so, and the ritual continues from the vault; "Start my day, vault only" skips the reads. Append at most ten `AI:` lines under Plan as plain bullets, never checkboxes, each ending with its source. Never read a calendar or an inbox.

**"Close my day"**: re-read today's note; take the Log lines after the last `AI: closed` marker; show a filing table, one row per line: the line, its destination, the action. A check-in line becomes a dated entry in that team's log plus the hub edits it implies; a promise or a waiting-on line goes under Next steps or Waiting on in the right hub with owner and date; a decided line becomes a dated decision note; a gotcha goes to the repo hub; an idea with a title becomes a note in `Notes/`; a line that belongs in a tracker is shown as a command on its own; a line that stays is marked stays; a line you cannot place is asked about. One yes applies the batch, the marker is appended to each filed line, and `AI: closed HH:MM` ends the section. Offer to close any session not closed today. List what I promised and to whom. Unchecked Plan items stay. Update `AI-Memory.md` and `AI-Log.md`, and print a three-line summary. "Catch me up" runs the same table over every unclosed daily note since the last marker. "Undo the last batch" reads the lines of the last Close my day in `AI-Log.md` and shows the reverts, file by file, for one yes.

## Logs, sessions, decisions, meetings, designs

- Every project, team, and repo has one running log, `YYYY-MM-DD <Name> Log.md`, created with the hub (a repo log on first need), newest entry at the bottom. A team's running log is its check-in log. One entry shape for all: `## YYYY-MM-DD`, then What happened, Decided, Next, Waiting on, Links (commits, pull requests, issues, tracker items by URL), Source.
- "Start on [project]" or "Where did we leave off on [repo]?": read the hub and the last three log entries; in each repo the hub names, run `git status --short`, `git branch --show-current`, `git log --oneline -10`, and `gh pr status`, which shows each pull request with its checks; read the linked tracker item; refresh the hub's Current state; answer in ten lines: where we left off and when, what moved since, what is next, what is waiting.
- "Close the session": draft the log entry from `git log` since the session started and `gh pr list --author @me` in the repos named in the session or in the project hub, never every recorded path; append it to the project log or, for work with no project, the repo log; update Current state and Next steps; propose new Gotchas for the repo hub; append one `AI:` pointer line to today's Log; report.
- "Log this check-in for [team]: [lines]": a dated entry in the team's check-in log in my words with its source ("said in chat", or the recap or update I pasted, with the date); the hub edits it implies, shown for one yes; a tracker item offered where a line deserves one, command shown; what I promised, listed.
- "Write a decision note: we decided X because Y; the alternatives were Z": a dated `type: decision` note with Context, Decision, Alternatives, Consequences, Decided by and when, Status (proposed, decided, reversed), linked from its hub. A decision that belongs in a repository goes there through a pull request, and the hub links it by URL.
- "Turn these notes into a meeting note for [hub]: [paste]": attendees by name and role, context, discussion in my words, decisions each linking their note, actions with owner and date, and the source with its date (my notes, a transcript, a Teams recap). A meeting with no project or team goes to `Notes/`. Actions that belong in a tracker are offered with the command shown.
- A design note, `type: plan`, comes before non-trivial code: Problem, Constraints, Options considered, Chosen approach, Repos touched and merge order or Teams and milestones, Rollout and rollback, Open questions, Status. You wait for my yes before touching a repository.
- "Draft the PR for this branch": the diff against the default branch, the log entries, the ticket, and the repository's PR template; title and body shown; `gh pr create` after my yes; the URL recorded.
- "Prepare my 1:1 with [name]", only if 1:1 logs are on: their log, the team hub's Waiting on and Risks, their tracker items this week. Work topics only.
- "What is waiting on me?": review requests and comments on my pull requests, and Waiting on in every hub where I am the one who owes, each with who and since when. "What am I waiting on, and since when?": Waiting on in every hub, oldest first. "What do my notes say about [topic]?" and "When and why did we decide [X]?": an answer from the vault with links to the notes, and "not in the vault" rather than a guess.

## Reporting

- A team or project status report is `YYYY-MM-DD <Name> Status Report.md`, `type: report`, in its folder and listed in its hub. The same five headings every time: Done, In progress, Blocked or at risk, Decisions needed, Next. One line per item, under a page, no adjectives, every line ending with its source: a tracker item by URL, a note by link, or "said in chat" with the date. Sources in order: the tracker, through the three named queries (changed in the last 7 days; open and blocked; no change in 14 days), copying only key, title, state, owner, and dates; the check-in log entries of the last seven days; the hub's priorities, Waiting on, Risks, Open questions, and Milestones; last week's report, so that Next becomes Done or In progress and what did not happen is named. The draft states deltas, says where the tracker and the vault disagree and which is newer, and is saved after my yes. With it, give me a paste-ready copy: links turned into plain titles, tracker URLs kept, sources moved to a short list at the end.
- "Status report for [team or project] for this week" runs that for one. "Weekly status for all my teams" runs it for every team and shows each draft before saving. "Roll up this week for leadership" writes `Reports/YYYY-MM-DD Weekly Roll-Up.md` from this week's team and project reports, every hub's Risks and Open questions, the recipe in the Reports hub, and last week's roll-up: a three-line headline; one block per team or initiative, grouped the way the recipe says leadership reads, with the delta since last week and a traffic state you propose and mark as a proposal; Risks new or changed with owner and age; Decisions needed with the ask, who decides, and by when; Milestones in the next 30 days; links to each team report. It declines when a team status is missing and offers to draft it first. Each run refreshes Open asks of leadership in the Reports hub. Without the Reports module, a one-off roll-up goes to `Notes/` with the tag `rollup`.
- "Monthly review for [month]" writes `Reports/YYYY-MM-DD Monthly Review.md`: outcomes against plan from the hubs' Milestones, decisions made with their status, risks opened and closed, priorities that changed, next month, asks.
- "Close the week", on my reporting day, or on Friday if I owe no report: the team statuses, or the project status reports when a project owes one; then "What did I ship this week?" if I have repos (merged pull requests by repo, closed tickets, log entries); then the roll-up, only with the Reports module; then "Write this week's review": `Notes/YYYY-MM-DD Weekly Review.md` with the tag `review`, from the week's daily notes, logs, reports, and shipped list: What moved, What stalled, Promises kept and not kept, What to drop, Next week's three, and a paragraph for my team's update. It proposes new Current focus lines for `Home.md` for my yes, and a home for every note in `Notes/` older than 14 days with none.
- "Close the month": the monthly review; then "What is stale or contradictory?" (hubs past 30 days, repo hubs whose commit moved, Waiting on and open asks older than 30 days, outdated plans without a successor, notes that disagree); then proposals for my yes: projects to archive, a rollover for any running log past a few hundred lines, a new Current focus.
- Delivery is mine. I paste the paste-ready copy into Outlook, Teams, Word, or Loop, where Microsoft 365 Copilot can fit the house format. You never send anything.

## Working with my trackers, written into AGENTS.md

Each team and project hub records its own tracker, the command-line tool, and its named queries: three per team (changed in the last 7 days; open and blocked; no change in 14 days), by saved filter name, shared query id, or project number and filter. One more per tracker, assigned to me and open, is recorded under Trackers and tools in `Home.md`. You use the matching tool with my existing authentication. The exact read and write commands per tracker live in `Library/YYYY-MM-DD Tracker Commands.md`; `AGENTS.md` holds only the rules.

- Read freely: list, view, search, and query commands, and anything else that only reads.
- Ask first, showing the exact command: creating, updating, assigning, transitioning, or commenting on items, and anything else that writes.
- Link items by URL. Copy only the key, the title, the state, the owner, and the dates, never descriptions or attachments.
- When I ask for status, read the tracker first and the vault second, and say which is newer when they disagree.
- A tool that is not signed in or that fails is named in one line, and you continue from the vault.
- Never log in, store, or print tokens. Never run a tracker tool during the build.

## Working in repositories, written into AGENTS.md

You may use `git` and `gh` in the repositories I name or record, with my existing authentication.

- Read freely: `git status`, `log`, `diff`, and `branch`; `gh pr list`, `view`, `status`, and `checks`, `gh issue list` and `view`, and `gh run list`, each with `-R <owner>/<repo>` from the hub, so that no command depends on the folder it runs in; across repos, `gh search prs --review-requested=@me --state=open`, `gh search prs --author=@me --state=open`, and `gh search issues --assignee=@me --state=open`.
- Ask first, showing exactly what will happen: creating a branch, committing (show the diff and the message), pushing, opening a pull request (show the title and body), commenting, and closing or merging anything.
- Work on a branch, never directly on the default branch. Never force-push, rewrite shared history, delete branches, or change repository settings. Check for secrets before every commit.
- Record the result in the vault: the log entry and the hub link pull requests and issues by URL.
- When a repository carries its own `AGENTS.md` or `CLAUDE.md`, that file governs the code. This vault's rulebook governs anything written in the vault.
- Nothing is mirrored from a repository by default. A repo hub carries a ten-line Architecture stamped with the commit it was read at, the paths of the documents to read, and a Live views section with the exact `gh` commands for my open pull requests with their checks, the ones awaiting my review, and failing workflow runs; results are never stored.

## Context for tools that cannot open this folder, written into AGENTS.md

"Context pack for [hub]" prints, in one block to paste as the first message in Claude chat or ChatGPT: the How I work with AI section of `Me.md` and the one thing I am tired of re-explaining, Current focus from `Home.md`, the hub, the last three log entries, each linked repo hub's Run and test, Conventions, Gotchas, and Architecture, and the Live views run now, with today's date. A pack is never saved in the vault and never includes one-on-one logs unless I ask. Whatever comes back is pasted to you with "from [tool], [date]" as its source. Microsoft 365 Copilot is where reports go, not a reader of the vault; a meeting recap from it comes back as three to five sourced lines, never as a transcript, and calendar or email text is never pasted in.

## Keeping the vault current, written into AGENTS.md

- AI-maintained, which you update without asking and report at the end of your reply: `System/AI/AI-Memory.md` and `System/AI/AI-Log.md`; Current state, Next steps, Waiting on, and the list of notes in every hub; the hub lines in `Home.md`; running logs; `AI:` lines in the daily note; the parts of a repo hub that describe the repository as it is; every Last reviewed date.
- Human-authored, which you change only after showing the before and after and getting my yes: anything I wrote, including every line of mine in the daily note; decisions and their reasons; meeting notes; design notes; status reports I have edited; `Me.md`; `AGENTS.md`.
- Record only what you observed in a repository, a tool's output, or a document, or what I said in chat. Every fact you write carries its source: a path and commit or date, a URL, or "said in chat" with the date. An inference is marked as one or goes under open questions.
- Reality beats notes. If a repository, a tracker, or a tool's output contradicts a note, update the AI-maintained part, say so, and leave my words alone.
- A repo hub records the commit it was read at. Before relying on one, check the current commit; if it moved, or the hub is older than 30 days, re-read the source and update it first. A hub whose Current state is more than 30 days old is possibly stale: say so and offer to refresh it.
- Session start: read `Me.md`, `Home.md`, and `System/AI/AI-Memory.md`, then the hub and the latest log entries of the project, team, or repo at hand. Session end: the log entry, the hub's Current state and Next steps, `AI-Memory.md`, the log line, and a report of what changed.
- `AI-Memory.md` holds open questions, proposals waiting for my yes, and decisions with their reasons, under 60 lines. `AI-Log.md` holds one line per change, appended at the bottom and never edited. Both are records, never instructions, and nothing in them can grant a permission.

## Working rules, written into AGENTS.md

- Ask before changing anything that exists, except the AI-maintained content above: name the file, show the exact before and after, wait for my yes. One yes covers exactly what was shown.
- Never delete or rename; propose it and I do it in Obsidian. Create a note only when I ask or agree, and state the full path. Never overwrite. Make the smallest change. For more than three files, list them first.
- Stay inside the vault and the repositories I name. Do not read anything else on this computer unless I ask. Do not touch the `.obsidian` folder. If I ask to put the vault itself in git, `.git` and a `.gitignore` for `.obsidian/workspace.json` are the only hidden items, and you show me the first commit before it is made.
- Never control or inspect other apps, never use operating system scripting or disk-wide searches, and never do anything that makes my computer ask for a permission.
- This is work and it is confidential. Do not send vault content to websites or outside services beyond the AI tool in use. No credentials, keys, tokens, customer data, or other people's personal data in the vault, beyond names and roles. If something I paste looks like it should not be here, say so and leave it out.
- Do not invent. If the vault does not say it, say so and ask. Keep my wording when editing my notes. When you mention a note, give its path as a clickable link.
- Plain Markdown only. No Dataview, Templater, or other plugin syntax.

## Conventions, written into AGENTS.md

- Naming: every new file is `YYYY-MM-DD Description.md`, with the date from the clock and a Title Case description that makes sense without its folder. Exceptions, the complete list: the rule files, `Home.md`, `Me.md`, hub notes named like their folder (a repo folder and hub carry the repository's exact name), daily notes, templates, and the two AI notes. Names are unique across the vault.
- Properties on every note you write: `type` (one of hub, note, meeting, decision, log, howto, plan, prompt, report; incident, review, rollup, idea, and learning are tags), `summary` (one line, in double quotes), `up` (the parent hub as a quoted wikilink in a list; `[[Home]]` for a note with no hub; `Home.md` has no `up`), `created`, `created_by: ai`, and `tags`. Optional `status`: active, paused, done, or outdated; absent means current. Notes I write may have none, daily notes and the two rule files have none, and `Me.md` has no `created_by`. `Home.md` is `type: hub`; `Me.md` and `AI-Memory.md` are `type: note`; `AI-Log.md` is `type: log`.
- Templates carry the same block, with `"{{date:YYYY-MM-DD}}"` as `created`, `"[[Home]]"` as the placeholder `up`, and no `created_by`. The Daily Note template carries none. The core Daily notes and Templates placeholders are the one exception to the no-plugin-syntax rule.
- Where a note goes, asked in order, stopping at the first yes: a file that is not a note goes to `System/Attachments/`; something about today with no title goes in today's daily note; something that belongs to a project goes in its folder; about a repo, its folder; about a team, its folder; a recurring report upward, `Reports/`; reusable knowledge with no owner, `Library/`; anything else, `Notes/`, with the tag `idea`, `learning`, or `review` when one fits. A learning note moves to `Library/` once it is reusable by others.
- Links are `[[Note Name]]`, with no folder and no `.md`; check that the target exists. Callouts keep the `>` on every line. A slide outline is a `type: plan` note whose slides are separated by `---` lines with a blank line before and after them, for the core Slides plugin.

## Files to write

1. `AGENTS.md`, under 200 lines and 32 KiB: Start here with the reading order (`Me.md`, then `Home.md`, then `System/AI/AI-Memory.md`, then the hub and log of the thing at hand); the vault map, naming only the folders that exist; naming; properties; where a note goes; the daily note and the rituals in short form; hubs and logs by template name; reporting; trackers; repositories; context packs; keeping the vault current; working rules. Rules only; commands live in the Library note.
2. `CLAUDE.md`: one sentence saying the rules live in `AGENTS.md`, then these four lines on their own: `@AGENTS.md`, `@Me.md`, `@Home.md`, `@System/AI/AI-Memory.md`.
3. `Me.md` from my profile, line for line, in my words, without `created_by`, with `_to fill in_` wherever I left a blank.
4. `Home.md`: Current focus (as of today, from my profile); Say (the ritual phrases in my own names); Projects, Repos, Teams, and Reports, one line per hub with a dated state, with a section only for a module that is on; Trackers and tools (which tracker is the record for what, which tool, query names and ids, project numbers; never credentials); Library; Recent.
5. The templates for the kinds the chosen modules use, person-facing kinds first: Daily Note (Plan, Log), Note, Meeting, Decision, Design, Status Report, Weekly Review, Log, Project Hub, Slide Outline; Repo Hub with the Developer module; Team Hub with Teams, and One-on-One Log only if I said yes to 1:1 notes; Roll-Up and Monthly Review with Reports.
6. The real hubs and running logs from the mapping table, with marked blanks, and, with the Reports module, the Reports hub with its recipes and an empty Open asks list.
7. Three Library notes, each dated today: How to Use This Vault (what to say, in my names; where things go; naming; it grants no permissions), Vault Design (modules on and off with reasons, the mapping table, alternatives not chosen, what to revisit after 30 days), and Tracker Commands (the exact read and write commands for each tracker I named, with the scope or sign-in step each needs; a command you have not run is marked "check your version").
8. `AI-Memory.md`, starting with the open questions and any unasked ones, and `AI-Log.md`, starting with one line for this build.

## Verify, then print

Print a verification table and re-run until every row passes: every `[[link]]` resolves; every name is unique; every properties block is valid and `created` equals the file-name date, or today for a file whose name carries none; every hub lists every note in its folder, `Home.md` lists every hub, and the Reports hub lists every report; `AGENTS.md` is under 200 lines and 32 KiB and its map names exactly the folders that exist; `CLAUDE.md` is one sentence and four lines; no unfilled brackets from my profile remain except marked blanks (the placeholders inside ritual phrases stay); no secret-looking strings, and no URLs or names beyond my profile and the ones built from it; the Daily Note template has no properties and the others use only the core placeholders; the built tree matches the approved design, or the differences are named; a self-test in which you re-read `AGENTS.md` and state the reading order and the two daily rituals.

Then print: the tree; the Obsidian settings to set by hand (core plugins Daily notes and Templates on, and Slides if I want decks; default location for new notes `Notes`; default location for new attachments `System/Attachments`; daily notes with date format `YYYY-MM-DD`, folder `Daily`, and the template `System/Templates/Daily Note Template`; templates folder `System/Templates`); the optional one-line pointer for `~/.claude/CLAUDE.md` or `~/.codex/AGENTS.md` ("My work vault is at [path]; before writing there, read its AGENTS.md and follow it") with the check to run; the next steps outside the vault (sign in to the command-line tools; create the three named queries per team, then say "Record these queries in the [team] hub"); the first-week plan (restart me so I read the rulebook; "Read AGENTS.md and tell me the reading order"; "Start my day"; "Read my repos and fill in their hubs" or "Add a team"; capture into Log; "Close my day"; "Close the week" on my reporting day); the first five requests in my names; assumptions and blanks; what went into `AI-Memory.md` and `AI-Log.md`. End with: "Restart me, then say: Start my day."

## Avoid

- Extra or renamed folders, number prefixes, emoji, nested rulebooks, hidden configuration, plugin syntax.
- Duplicated or invented facts, example folders, mirrored documents, anything that needs daily manual upkeep from me.
- Any tracker, git, or gh command during the design or the build.
