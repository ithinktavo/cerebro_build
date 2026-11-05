---
type: howto
summary: "What to say to the AI tools in this vault, in Alex's names, where things go, and how files are named. A reminder that grants no permissions."
up:
  - "[[Home]]"
created: 2026-11-05
created_by: ai
tags:
  - howto
  - vault
---

This note is a reminder for Alex. The rules are in `AGENTS.md`, and nothing written here grants a permission or changes a rule.

## What to say

| Say | What happens |
| --- | --- |
| "Start my day" | Today's note is created from the Daily Note template. Up to ten `AI:` lines land under Plan: carried-over items, hub next steps Alex owns, today's cadence, what the Friday status still lacks, teams with no check-in, stale hubs, open questions, then the trackers. "Start my day, vault only" skips the trackers. |
| "Add to today: [line]" | The words are appended to today's Log, verbatim. |
| "Close my day" | A filing table for today's Log lines. One yes files the batch, each filed line gets ` → [[Hub]]`, and `AI: closed HH:MM` ends the section. |
| "Catch me up" | The same table over every daily note not closed since the last marker. |
| "Start on Checkout Migration" or "Start on Observability Rollout" | The hub and the last three log entries, git and gh in the repos the hub names, the tracker item, a refreshed Current state, and a ten-line answer. |
| "Where did we leave off on checkout-api?" or "... on web-storefront?" | The same, for a repository. |
| "Close the session" | The log entry drafted from git and gh, the hub refreshed, new Gotchas proposed, a pointer line in today's Log. |
| "Log this check-in for Team Alpha: [lines]" or "... for Team Beta: [lines]" | A dated entry in the team's log, the hub edits it implies shown for one yes, tracker items offered with the command shown. |
| "Status report for Team Alpha for this week" or "... Team Beta ..." | One team's report, shown before saving, with a paste-ready copy. |
| "Weekly status for all my teams" | One status report draft per team, shown before saving, each with a paste-ready copy. |
| "Write a decision note: we decided X because Y; the alternatives were Z" | A dated decision note, linked from its hub. |
| "What is waiting on me?", "What am I waiting on, and since when?", "What do my notes say about [topic]?" | Answers from the hubs and notes, with links; nothing saved. |
| "Undo the last batch" | The last Close my day batch reverted, file by file, after a yes. |
| "Roll up this week for leadership" | `Reports/YYYY-MM-DD Weekly Roll-Up.md`, grouped by team. Declined if a team status is missing. |
| "What did I ship this week?" | Merged pull requests by repo, closed tickets, log entries. |
| "Write this week's review" | `Notes/YYYY-MM-DD Weekly Review.md` with the tag review. |
| "Close the week" | On Friday: team statuses, shipped list, roll-up, weekly review, and proposals for Current focus. |
| "Monthly review for [month]" and "Close the month" | `Reports/YYYY-MM-DD Monthly Review.md`, then the stale check and the archive proposals. |
| "What is stale or contradictory?" | Hubs past 30 days, repo hubs whose commit moved, old Waiting on and asks, outdated plans, notes that disagree. |
| "Context pack for [hub]" | One block to paste as the first message in ChatGPT. Never saved in the vault. |
| "Draft the PR for this branch" | Title and body from the diff, the logs, the ticket, and the PR template; `gh pr create` after a yes. |
| "Turn these notes into a meeting note for [hub]: [paste]" | A meeting note from the Meeting template, in the hub's folder. |
| "Read my repos and fill in their hubs" | The marked blanks in [[checkout-api]] and [[web-storefront]] are filled from the repositories, stamped with the commit. |
| "Add the repo at [path]" and "Add a team" | A new repo folder and hub, or a new team folder, hub, and log. |
| "Record these queries in the Team Alpha hub" or "... Team Beta hub" | The three named queries are written into the hub once the views or filters exist. |

"Prepare my 1:1 with [name]" is off, because 1:1 notes stay out of the vault ([[Me]]).

## Where things go

1. A file that is not a note: `System/Attachments/`, linked from a hub.
2. Something about today with no title: today's daily note.
3. Something about a project: `Projects/Checkout Migration/` or `Projects/Observability Rollout/`. About a repo: `Repos/checkout-api/` or `Repos/web-storefront/`. About a team: `Teams/Team Alpha/` or `Teams/Team Beta/`.
4. A roll-up or a monthly review: `Reports/`. A team status report stays in its team folder.
5. Reusable knowledge with no owner: `Library/`.
6. Anything else: `Notes/`, tagged idea, learning, or review when one fits.

## Naming

- New files are `YYYY-MM-DD Description.md`, the date from the clock, the description in Title Case and meaningful without its folder: `2026-11-05 Team Alpha Log.md`.
- The exceptions are the rule files, `Home.md`, `Me.md`, hubs named like their folder (repo hubs keep the repository's exact name), daily notes, templates, and the two AI notes.
- Names are unique across the vault. Links are `[[Note Name]]` with no folder and no `.md`.

## Hubs and logs

- Every hub starts with Current state and a date and lists every note in its folder. Project and team hubs also keep Next steps, Waiting on, Risks, Open questions, and Decisions; repo hubs keep what the repository is and how it runs; the Reports hub keeps the recipes and the open asks.
- Every project and team has one running log, newest entry at the bottom, with one entry shape: What happened, Decided, Next, Waiting on, Links, Source. A repo log is created on first need.
- The AI keeps the hubs' Current state, Next steps, Waiting on, and note lists, the logs, the `AI:` lines, and the two notes in `System/AI/` on its own and reports it. Everything Alex wrote changes only after a shown before and after and a yes.
