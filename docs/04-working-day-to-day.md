# 4. Working day to day

The vault pays off when it is the place you and the AI start from, not a second system to maintain. This page is the rhythm that keeps it true with almost no manual upkeep: the AI does the bookkeeping, you make the calls.

## A session, start to finish

Every session with an AI tool on the vault has the same shape, because `AGENTS.md` tells the tool to:

1. **Start** by reading `Me.md`, `Home.md`, and the AI memory note, then the hub and the latest log of the project or team you name. If a repository is involved, it checks the status and the open pull requests first.
2. **Work**: a status report, meeting notes, a design note, code in the repository, a query against the tracker.
3. **End** by writing the session log or check-in entry, refreshing the hub's current state and next steps, updating the memory note, adding a line to the change log, and telling you what it changed.

You open with a short brief: "Status report for Team Alpha for this week" or "Write up the decision from the design review, from these notes". The tool explores the vault for the rest.

## Capture

| What you have | Where it goes | How |
| --- | --- | --- |
| A quick thought, a reminder, something from today | Today's daily note | Type it in Obsidian, or tell the AI "add to today" |
| Meeting notes | A dated `type: meeting` note in the project or team folder | Paste the raw notes; the AI shapes them into attendees, discussion, decisions, and actions with owners |
| A decision | A dated `type: decision` note with Context, Decision, Alternatives, Consequences | Ask the AI to write it; it links the decision from the hub |
| Something you learned that others could use | `Library/` | How-tos, checklists, standards |
| A document or deck to produce | A note first, then an export in `System/Attachments/` | The note stays the source; the export is dated and linked from the hub |

## Where a note goes

Ask these in order and stop at the first yes. The AI applies the same list.

1. Not a note (image, PDF, spreadsheet)? `System/Attachments/`, linked from a hub.
2. About today, with no title of its own? Today's daily note.
3. Belongs to a project? Its project folder.
4. About a team? Its team folder.
5. Describes a repository? Its blueprint folder.
6. Reusable knowledge with no owner? `Library/`.
7. Anything else: `Notes/`.

## Naming and properties

- Every new file is `YYYY-MM-DD Description.md`. The date comes from the system clock, the description is Title Case, two to six words that make sense without the folder name. Names are unique across the vault, so links never break.
- Exceptions: `AGENTS.md`, `CLAUDE.md`, `Home.md`, `Me.md`, hub notes, daily notes, templates, and the two AI notes.
- Every AI-written note starts with properties: `type`, `summary`, `status`, `up`, `created`, `created_by`, `tags`. Notes you write by hand may have none.
- The `summary` lines are an index of the whole vault. Searching for `summary:` lists every note's one-line summary without opening a file.

## The weekly rhythm

- **Your reporting day.** "Status report for [team or project] from the tracker." The AI reads the tracker through its command-line tool, then the hub and the logs, and drafts the five headings: Done, In progress, Blocked or at risk, Decisions needed, Next. You edit, then send it wherever it goes. The note stays in the folder as a dated `type: report`. The prompt is in [prompts/weekly-status-report.md](../prompts/weekly-status-report.md).
- **During the week.** Meeting notes, decisions, and check-ins as they happen. Anything you promised goes in the hub under Waiting on or Next steps, with the owner named.
- **End of the week.** "Write this week's review." A dated note in `Notes/` with the tag `review`: what moved, what stalled, what to drop.
- **Every 30 days, without you asking.** When a hub's current state or a blueprint is more than 30 days old, the AI says so before relying on it and offers to refresh it.

## Documents and slides from the notes

- Ask for a document. The AI writes a note from the hubs and notes it finds, you edit it, and then it is exported to Word or PDF into `System/Attachments/` if the tool can do that, or you paste it into your company template.
- Ask for a deck. The AI writes a slide outline note whose slides are separated by `---` lines with a blank line before and after them. Obsidian's core Slides plugin presents it directly. For a PowerPoint file, ask the AI tool to produce one from the outline if it supports that, and keep the file in `System/Attachments/`.

## Keeping it true

- One fact lives in one note. Hubs and `Home.md` quote it with a date and a link, so there is one place to fix.
- When a tool's output contradicts a note, the AI updates the AI-maintained part and says so. Your own words stay yours until you approve a change.
- The memory note is the running list of open questions and proposals. Look at it when you have five minutes; answering two questions there saves the AI from guessing later.
- The change log is the audit trail. Search it when you wonder when something changed.
- Once a quarter, ask: "What in the vault is stale or contradictory?" The AI lists hubs past 30 days, outdated plans without a successor, and notes that disagree.

Next: [Keep it safe](05-keep-it-safe.md).
