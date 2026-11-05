# 4. Working day to day

The vault pays off when it is the place you and the AI start from, not a second system to maintain. This page is the rhythm that keeps it true with almost no manual upkeep: you type into today's note and say a few fixed phrases, the AI files, refreshes the hubs, and drafts the reports from sources, and you make the calls.

Every session with a tool opened on the vault has the same shape, because `AGENTS.md` tells the tool to:

1. Start by reading `Me.md`, `Home.md`, and `System/AI/AI-Memory.md`, then the hub and the latest log entries of the project, team, or repository at hand.
2. Work: a status report, a meeting note, a design note, code in a repository you name, a query against a tracker.
3. End with the log entry, the hub's Current state and Next steps, the memory note, a line in the change log, and a report of what it changed.

You open with a short brief, such as "Status report for Team Alpha for this week" or "Write up the decision from the design review, from these notes", and the tool explores the vault for the rest. The phrases below are the fixed ones. The Say section of your `Home.md` lists them with your own team, project, and repository names, and [prompts/first-week.md](../prompts/first-week.md) walks through the first week.

## The daily note

`Daily/YYYY-MM-DD.md` is where everything lands during the day. Obsidian creates it from the template with two headings and no properties:

- `## Plan`: checkboxes for today.
- `## Log`: one line per thing as it happens, in your words. A check-in, a promise, a decision, a gotcha, an idea.

A Log at mid-afternoon looks like this:

```
## Log
- Standup Team Alpha: retry logic is on staging; Alex Example owes the load test by Friday
- Decided: keep the feature flag until Team Beta is trained, because support is not ready
- [[checkout-api]] gotcha: the integration tests need the local cache running
- Idea: a Library note on how we name feature flags
```

The note is shared with the AI, so the rulebook fixes who owns what:

- Every line the AI writes starts with `AI:`. It never edits, reorders, or ticks a line you wrote.
- The only change it ever makes to your line is the filing marker ` → [[Hub]]`, appended after your yes at the end of the day. The marker says where the line went and keeps it from being filed twice.
- Starting a Log line with `[[Team Alpha]]` or `[[checkout-api]]` is an optional hint about where it belongs. The AI uses it when present and infers the home from the words when absent.
- The AI re-reads the note right before every write, because you may have typed in Obsidian in the meantime.

## "Start my day"

Say `Start my day` as the first thing in the morning. Two minutes, and the AI:

1. Takes the date from the clock, searches the vault for today's note, and creates it from the template if none exists.
2. Runs `Catch me up` first if any daily note since the last `AI: closed` marker still has unfiled Log lines.
3. Reads the vault: yesterday's unchecked Plan items, carried with the date first seen (on the third morning it flags the item: give it a date in a hub or drop it); every hub's Next steps with you as owner and Waiting on older than seven days; your week and each team's cadence, for today's commitments and the inputs a report due this week still lacks; teams with no check-in this week; hubs whose Current state is past 30 days; the open questions in `System/AI/AI-Memory.md`.
4. Reads the trackers: your open pull requests and the ones waiting for your review, items assigned to you through each tracker's assigned-to-me query, and each team's blocked query. A tool that is not signed in or that fails gets one `AI:` line saying so, and the ritual continues from the vault. `Start my day, vault only` skips the reads.
5. Appends at most ten `AI:` lines under Plan, each ending with its source.

It never reads a calendar or an inbox.

## During the day

You type in Obsidian, or say one of these:

- `Add to today: <line>` appends your words to Log, verbatim.
- `Log this check-in for Team Alpha: <three lines>`, after a standup or a sync. The AI writes a dated entry in the team's check-in log in your words with its source ("said in chat", or the recap you pasted, with the date), shows the hub edits it implies (priorities, Waiting on, Risks) for one yes, offers a tracker item where a line deserves one with the command shown, and lists what you promised. Prompt: [prompts/team-check-in.md](../prompts/team-check-in.md).
- `Start on <project>` or `Where did we leave off on <repo>?` reads the hub and the last three log entries, runs the git and gh read commands in each repository the hub names, reads the linked tracker item, refreshes the hub's Current state, and answers in ten lines: where we left off and when, what moved since, what is next, what is waiting.
- `Close the session`, at the end of a coding session. The AI drafts the log entry from the git log since the session started and your open pull requests in the repositories named in the session or in the project hub, appends it to the project log (or to the repo log for work with no project), updates Current state and Next steps, proposes new Gotchas for the repo hub, and appends one `AI:` pointer line to today's Log.
- `Turn these notes into a meeting note for <hub>: <paste>`: attendees by name and role, context, discussion in your words, decisions each linking their note, actions with owner and date, and the source with its date. A meeting with no project or team goes to `Notes/`. Actions that belong in a tracker are offered with the command shown. Prompt: [prompts/meeting-notes.md](../prompts/meeting-notes.md).
- `Write a decision note: we decided X because Y; the alternatives were Z`: a dated `type: decision` note with Context, Decision, Alternatives, Consequences, Decided by and when, and Status, linked from its hub. A decision that belongs in a repository goes there through a pull request, and the hub links it by URL.
- `What is waiting on me?`, at any time: review requests and comments on your pull requests, and the Waiting on lines in every hub, each with who and since when. The mirror question, `What am I waiting on, and since when?`, works the same way.

Away from your desk there is no capture path into the vault: personal sync services are out, so Obsidian on a phone is out as written. Send yourself a message in Teams or Outlook and paste the lines at the end of the day as `Add to today: [line]`, text only, never the thread.

What goes where, in short:

| What you have | Where it goes | How |
| --- | --- | --- |
| A quick thought, a reminder, something from today | Today's daily note, under Log | Type it in Obsidian, or say `Add to today: <line>` |
| Three lines after a standup or sync | The team's check-in log | `Log this check-in for Team Alpha: <lines>`, see [prompts/team-check-in.md](../prompts/team-check-in.md) |
| Meeting notes | A dated `type: meeting` note in the project or team folder, or `Notes/` | `Turn these notes into a meeting note for <hub>: <paste>`, see [prompts/meeting-notes.md](../prompts/meeting-notes.md) |
| A decision | A dated `type: decision` note, linked from its hub | `Write a decision note: we decided X because Y; the alternatives were Z` |
| A Jira item, work item, issue, or pull request to keep in view | A URL in the hub under Next steps or Waiting on | Link, never copy. At most the key, title, state, owner, and dates |
| A note of your own with a title | `Notes/`, or `Library/` once others can reuse it | Write it. Properties are optional, and the AI leaves it alone unless you ask |
| A status report | A dated `type: report` note in the team or project folder | `Status report for Team Alpha for this week`, see [prompts/weekly-status-report.md](../prompts/weekly-status-report.md) |
| A document or deck to produce | A note first, then an export in `System/Attachments/` | The note stays the source; the export is dated and linked from the hub |

## "Close my day"

Say `Close my day` at the end of the day. Five minutes, and the AI:

1. Re-reads today's note and takes the Log lines after the last `AI: closed` marker.
2. Shows a filing table, one row per line: the line, its destination, the action. A check-in line becomes a dated entry in that team's log plus the hub edits it implies. A promise goes under Next steps in the right hub with you as owner and a date; something someone owes you goes under Waiting on, with who and since when. A "decided" line becomes a dated decision note. A gotcha goes to the repo hub. An idea with a title becomes a note in `Notes/`. A line that belongs in a tracker is shown as a command on its own. A line that stays is marked stays. A line it cannot place, it asks about.
3. Applies the batch after one yes. Nothing lands in a hub without it. The marker is appended to each filed line, and `AI: closed HH:MM` ends the section.
4. Offers to close any coding session not closed today, lists what you promised and to whom, leaves unchecked Plan items in place for tomorrow, updates the two AI notes, and prints a three-line summary.

To take a batch back, say `Undo the last batch`. It reads the batch's lines in `System/AI/AI-Log.md` and shows the reverts, file by file, for one yes. Obsidian's File recovery and the vault's git history are the fallbacks.

The Log above ends the day like this:

```
- Standup Team Alpha: retry logic is on staging; Alex Example owes the load test by Friday → [[Team Alpha]]
- Decided: keep the feature flag until Team Beta is trained, because support is not ready → [[Checkout Migration]]
- [[checkout-api]] gotcha: the integration tests need the local cache running → [[checkout-api]]
- Idea: a Library note on how we name feature flags (stays)
AI: closed 17:40
```

After days away, say `Catch me up`. It runs the same table over every unclosed daily note since the last marker, in one pass. Skipping a day costs nothing, and the markers mean nothing is filed twice.

## The week

Say `Close the week` on your reporting day. It runs four things in order, each shown before it is saved. The prompt is [prompts/close-the-week.md](../prompts/close-the-week.md); the role page for managers, PMs, and directors is [roles/pm-director.md](../roles/pm-director.md).

1. **The team statuses.** `Weekly status for all my teams`, or `Status report for Team Alpha for this week` for one. Each is a dated `type: report` note in the team or project folder with the same five headings every time: Done, In progress, Blocked or at risk, Decisions needed, Next. One line per item, under a page, no adjectives, every line ending with its source: a tracker item by URL, a note by link, or "said in chat" with the date. The AI reads the tracker first, through the team's three named queries (changed in the last seven days; open and blocked; no change in 14 days), then the check-in log entries of the last seven days, the hub's priorities, Waiting on, Risks, Open questions, and Milestones, and last week's report, so that last week's Next becomes this week's Done or In progress and what did not happen is named. The draft states deltas and says where the tracker and the vault disagree, and which is newer. You edit, then it is saved. Prompt: [prompts/weekly-status-report.md](../prompts/weekly-status-report.md).
2. **`What did I ship this week?`**, if you have repositories: merged pull requests by repository, closed tickets, and the week's log entries.
3. **The roll-up.** `Roll up this week for leadership` writes `Reports/YYYY-MM-DD Weekly Roll-Up.md` from this week's team and project reports, every hub's Risks and Open questions, the recipe in the Reports hub, and last week's roll-up: a three-line headline; one block per team or initiative, grouped the way the recipe says leadership reads, with the delta since last week and a traffic state marked as the AI's proposal; risks new or changed, with owner and age; decisions needed, with the ask, who decides, and by when; milestones in the next 30 days; links to each team report. It declines when a team status is missing and offers to draft it first. Without the Reports module, a one-off roll-up goes to `Notes/` with the tag `rollup`.
4. **`Write this week's review`.** `Notes/YYYY-MM-DD Weekly Review.md` with the tag `review`, from the week's daily notes, logs, reports, and shipped list: What moved, What stalled, Promises kept and not kept, What to drop, Next week's three, and a paragraph for your own team's update. It then proposes new Current focus lines for `Home.md` and a home for every note in `Notes/` older than 14 days that has none.

Teams on different trackers are normal. Each team or project hub records its own tracker, the command-line tool, and its three named queries, so the status report for that team uses that tool, and the roll-up reads each hub's tracker in turn. The exact commands live in `Library/YYYY-MM-DD Tracker Commands.md`, set up in [Connect your work trackers](03-connect-work-trackers.md). A team on GitHub Projects, for example, answers its queries with commands like these:

```
gh project item-list <number> --owner YOURORG --format json --limit 100     # the board as JSON; the default limit is 30; needs the project scope on your gh login
gh project item-list <number> --owner YOURORG --query "status:Blocked"      # a server-side filter in the Projects filter syntax, if the board has that status; needs gh 2.87.0 or newer, so check your version
```

## The month

Say `Close the month`. It runs three things:

1. `Monthly review for <month>` writes `Reports/YYYY-MM-DD Monthly Review.md`: outcomes against plan from the hubs' Milestones, decisions made with their status, risks opened and closed, priorities that changed, next month, asks.
2. `What is stale or contradictory?` lists hubs past 30 days, repo hubs whose commit moved, Waiting on and open asks older than 30 days, outdated plans without a successor, and notes that disagree. This is also the only check on hubs nobody opened during the month.
3. Proposals for your yes: projects to archive (a finished project moves as a whole folder to `Archive/`, created on first need), a rollover for any running log past a few hundred lines, and a new Current focus for `Home.md`.

## Your own notes

The AI files what you capture. The notes you write yourself have a home too:

- An idea, a learning note, or a draft you are thinking through goes in `Notes/`, with the tag `idea`, `learning`, or `review` when one fits. Name it like every other note, `YYYY-MM-DD Description.md`, with a Title Case description that makes sense without its folder, so it sorts by date and its links never break.
- A how-to, a checklist, or a standard that others could reuse goes in `Library/`. A learning note moves there once it is reusable by others; the AI proposes the move and you do it in Obsidian, because the AI never renames or moves a file.
- Hand-written notes need no properties. The AI treats them as information and changes them only after showing the before and after and getting your yes. Notes it writes start with `type`, `summary`, `up`, `created`, `created_by`, and `tags`, plus `status` only when the note is paused, done, or outdated.
- The `summary` lines are an index. Search the vault for `summary:` and every AI-written note's one-line summary appears without opening a file.
- Ask the vault. `What do my notes say about [topic]?` and `When and why did we decide [X]?` answer with links to the notes, and say "not in the vault" rather than guess.
- When three notes on one topic pile up in `Notes/`, the AI proposes a project or a folder for them.

Where a note goes, asked in order, stopping at the first yes. The AI applies the same list:

1. Not a note (image, PDF, spreadsheet)? `System/Attachments/`, linked from a hub.
2. About today, with no title of its own? Today's daily note.
3. Belongs to a project? Its project folder.
4. About a repository? Its `Repos/` folder, if you have the Developer module.
5. About a team? Its `Teams/` folder, if you have the Teams module.
6. A recurring report upward? `Reports/`, if you have the Reports module.
7. Reusable knowledge with no owner? `Library/`.
8. Anything else: `Notes/`.

## Several repositories

For the developer who works across repositories. The full role page is [roles/developer.md](../roles/developer.md).

- A project can span repositories: a feature across three of them, a migration, a release. The project hub links each repo hub it touches, with the part it serves, the branch, the pull request, and the deploy order; a design note records the merge order for the one change it describes. Ticket-sized work is a log entry, not a project. Name the project in your brief, and the AI reads the repo hubs the project hub links.
- One running log per project, one entry per session. `Close the session` appends to it, with the commit and pull request links from every repository touched. Work that serves no project goes to the repository's own log, created on first need.
- Each repository has its own hub in `Repos/<repo-name>/`, named exactly like the repository on GitHub, with Run and test, Conventions, Gotchas, a ten-line Architecture stamped with the commit it was read at, and Live views: the exact `gh` commands for your open pull requests, the ones awaiting your review, and failing checks. Results are never stored.
- The per-repo history is Obsidian's Backlinks pane, a core plugin. Open the repo hub and show its backlinks: every log entry and daily line that links to the hub is listed there, across projects, with unlinked mentions below.

Which folder to open the tool on:

- A notes-heavy day: open the tool on the vault and name the repository path in your brief. The rulebook loads on its own, and it lets the AI run git and gh in the repositories you name.
- A code-heavy day: open the tool on the repository. The repository's own `AGENTS.md` or `CLAUDE.md` governs the code; the vault's rulebook governs anything written in the vault. Whether the tool can see the vault from there depends on the tool and the version, which is why the build prints an optional one-line pointer for `~/.claude/CLAUDE.md` or `~/.codex/AGENTS.md`, outside both folders: "My work vault is at [path]; before writing there, read its AGENTS.md and follow it". Check it once with `Read AGENTS.md and tell me the reading order`. If the tool cannot reach the vault, start the brief with `Read <vault path>/AGENTS.md first`, or run two sessions: close the coding session in the repository tool and paste its summary to a session on the vault with `Close the session: <paste>`. Claude Code, Codex, and Copilot CLI add a second folder to a session with `--add-dir`; [Connect your AI tools](02-connect-ai-tools.md) has both routes.
- Per tool: Claude Code reads `CLAUDE.md` from the folder it is opened in and every folder above it, plus `~/.claude/CLAUDE.md`. Codex reads `~/.codex/AGENTS.md` first, and in a folder that is not a git repository it reads `AGENTS.md` only from the folder it was started in, so start it at the vault root. Copilot in VS Code reads `AGENTS.md` at the workspace root; which files it reads depends on the harness you pick in the Session Target control, and `AGENTS.md` files outside the workspace root are off by default, so on a code day keep the repository as the workspace and start the brief with the read instruction. If a tool asks before writing outside the folder it was opened on, say yes only for the vault path or the repository you named. Details in [Connect your AI tools](02-connect-ai-tools.md).

## Where reports go

Delivery is yours. With every status report, roll-up, and review, the AI gives you a paste-ready copy: links turned into plain titles, tracker URLs kept, sources moved to a short list at the end. You paste it into Outlook, Teams, Word, or Loop, where Microsoft 365 Copilot can fit it to the house format. The AI never sends anything. The note in the vault stays the source, with its sources on every line.

Documents and decks work the same way:

- Ask for a document. The AI writes a note from the hubs and notes it finds. You edit it, then paste it into Word and let Microsoft 365 Copilot format it there. A file that comes back goes in `System/Attachments/` with a dated name, linked from the hub. The note stays the source.
- Ask for a deck. The AI writes a slide outline note, a `type: plan` note whose slides are separated by `---` lines with a blank line before and after them. Obsidian's core Slides plugin presents it directly. For a PowerPoint file, build it from the outline in PowerPoint and keep the file in `System/Attachments/`. Whether your chat tool can write a .pptx from a pasted outline depends on the tool and the plan, so check your version.

## When the tool cannot open the folder

Claude chat, ChatGPT, and Microsoft 365 Copilot cannot read the vault or create files in it. The vault still serves them:

1. In a tool opened on the vault, say `Context pack for Team Alpha`, or for any other hub. It prints one block to paste as the first message: the How I work with AI section of `Me.md` and the one thing you are tired of re-explaining, Current focus from `Home.md`, the hub, the last three log entries, each linked repo hub's Run and test, Conventions, Gotchas, and Architecture, and the Live views run now, with today's date. A pack is never saved in the vault and never includes one-on-one logs unless you ask. Prompt: [prompts/context-pack.md](../prompts/context-pack.md).
2. Paste the pack into Claude chat or ChatGPT and work there.
3. Paste whatever comes back to the vault tool with its source: `Add to today: <line>, from ChatGPT, 2026-11-05`, or a decision or meeting note whose Source line names the tool and the date. The AI records it as a tool's output, never as something it observed itself.
4. Microsoft 365 Copilot is where reports go, not a reader of the vault. With a Microsoft 365 Copilot license it can recap a Teams meeting; the recap comes back as three to five sourced lines, `Log this check-in for Team Alpha: <lines>, from Microsoft 365 Copilot, 2026-11-05`, never as a transcript. Calendar or email text is never pasted in.

For standing context, a Claude Project or a ChatGPT Project can hold the rulebook, `Me.md`, `Home.md`, and the hubs. Markdown is not on either upload list, so test one `.md` upload first, and paste the text or save a `.txt` copy if the picker refuses it. Set-up is in [Connect your AI tools](02-connect-ai-tools.md).

## Keeping it true

- One fact lives in one note. Hubs and `Home.md` quote it with a date and a link, so there is one place to fix.
- The AI maintains, without asking and with a report at the end of its reply: the two AI notes; Current state, Next steps, Waiting on, and the list of notes in every hub; the hub lines in `Home.md`; running logs; `AI:` lines in the daily note; the parts of a repo hub that describe the repository as it is; every Last reviewed date. Everything you wrote, decisions and their reasons, meeting notes, design notes, status reports you have edited, `Me.md`, and `AGENTS.md` change only after you see the before and after and say yes.
- Reality beats notes, for the AI-maintained part only. When a repository, a tracker, or a tool's output contradicts a note, the AI updates that part and says so. Your words stay yours.
- Whenever it reads a stale hub. A hub whose Current state is more than 30 days old, or a repo hub whose commit moved, is possibly stale: the AI says so before relying on it and offers to refresh it. Nothing runs on its own, so a hub nobody opens stays stale silently. That is what `What is stale or contradictory?` at the end of the month is for.
- Every fact the AI writes carries its source: a path and commit or date, a URL, or "said in chat" with the date. An inference is marked as one or goes under open questions.
- `System/AI/AI-Memory.md` is the running list of open questions and proposals. Look at it when you have five minutes; answering two questions there saves the AI from guessing later.
- `System/AI/AI-Log.md` is the audit trail. Search it when you wonder when something changed.
- To add a standing rule, say `Add this rule to AGENTS.md: [rule]`. The AI shows the before and after, keeps the file under 200 lines, and you restart the tool. A newer build prompt is applied to an existing vault the same way: paste it, and the stop on a non-empty folder becomes a proposal of additions only.
- What it costs: each ritual is a handful of reads. `Start my day` reads every hub and runs a few tracker commands per team, which counts against your plan's usage like any other request. With more than about ten hubs, run it vault-only on busy days and keep the tracker reads for the reporting day.

Next: [Keep it safe](05-keep-it-safe.md).
