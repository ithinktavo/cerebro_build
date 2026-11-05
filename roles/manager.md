# Playbook: managers and team leads

You track teams and initiatives, collect status, and report upward, while staying hands-on in some code. The vault gives each team a hub and a check-in log, lets the AI pull the live state from the tracker, and turns both into a weekly status report that you only have to edit.

## Keep these blocks in the build prompt

Teams. Code and Blueprints if you still ship code. Drop Terraform unless you build infrastructure.

## What you get

- `Teams/<Team>/<Team>.md`: purpose, members by name and role, current priorities as of a date, links to the board and shared queries, waiting on (who, what, since when), risks, decisions, and the notes in the folder.
- A running check-in log per team, a `type: log` note with one dated entry per check-in or sync.
- Dated status reports, `type: report`, in the team folder, with the same five headings every time.
- Projects for cross-team initiatives.
- Daily notes for your own day: promises made, people to follow up with.

## Getting status from teams without adding a process

Three sources, in this order:

1. **The tracker.** If the team keeps Jira or Azure DevOps current, the AI reads it: what closed this week, what is in progress, what has not moved, what is blocked. Nobody writes a status email for you. Set up one shared query or board filter per team, so the AI can run it by name. See [Connect your work tracker](../docs/03-connect-work-trackers.md).
2. **Your check-ins.** After a standup, a 1:1, or a sync, dictate or paste three lines: "Team Alpha: cutover moved to Thursday, waiting on the security review, [name] out next week." The AI adds a dated entry to the team's check-in log and updates Waiting on and Risks in the hub. The prompt is in [prompts/team-check-in.md](../prompts/team-check-in.md).
3. **The team's own words.** Where a team already sends a weekly update in chat or email, paste it. The AI logs it with "from the team's update" and the date as the source. The vault never claims more than its sources say.

## The weekly status report

"Status report for Team Alpha for this week." The AI:

1. Runs the team's tracker query: items changed, closed, or blocked in the last seven days.
2. Reads the team hub, the check-in log, and last week's report.
3. Drafts the report under five headings: Done, In progress, Blocked or at risk, Decisions needed, Next. Every line carries its source: a tracker URL, a note link, or "said in chat" with the date.
4. Saves it as a dated `type: report` note in the team folder and links it from the hub.

You edit the draft in ten minutes instead of writing it in an hour, then paste it where your reporting goes. For several teams: "Roll up this week's team reports for my manager, one paragraph per team, then the three things I need decided." The roll-up is saved as a dated report in `Notes/`. The prompt is in [prompts/weekly-status-report.md](../prompts/weekly-status-report.md).

## 1:1s and people

A 1:1 gets its own dated `type: meeting` note in the team folder, named after the person, holding work topics and actions only: priorities, blockers, asks, follow-ups. Only what concerns the team's work goes from there into the check-in log. Performance, compensation, and personal matters go in the HR system, never in the vault. The rules tell the AI to say so if something like that is pasted. See [Keep it safe](../docs/05-keep-it-safe.md).

## Keeping yourself honest

- "What am I waiting on, and since when?" The AI reads Waiting on in every hub.
- "What did I promise this week?" Daily notes and check-in logs.
- "Which team hubs are stale?" Anything with a current state older than 30 days.

## Requests to try

1. "Add a team: [name]. Members: [names and roles]. Board: [URL]. Shared query: [name or id]."
2. "Log this check-in for [team]: [three lines]."
3. "Status report for [team] for this week from the tracker."
4. "Roll up all team reports for this week."
5. "Prepare my 1:1 with [name] from the [team] hub and log: open items, decisions needed, what they are waiting on from me."
