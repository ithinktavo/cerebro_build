# Close the week

On your reporting day, one phrase runs the week's reports in order: a status per team, what you shipped, the roll-up for leadership, and your own review. You read each draft and say yes; you paste what goes out. The tool never emails or posts to people; its only writes outside the vault are the push, the pull request, and the story comment, each shown first and run on your yes.

## What to say

"Close the week."

Each step is also its own request, for a week when you need only one of them:

- "Weekly status for all my teams", or "Status report for Team Alpha for this week".
- "What did I ship this week?"
- "Roll up this week for leadership".
- "Write this week's review".

At the end of the month, "Close the month" runs the monthly review and a staleness pass; it is the last step below.

## What happens

Before you start: the three named queries per team are recorded in the hubs, and the week's Log lines are filed. If an evening was skipped, say "Catch me up" first, so that the reports draw on filed entries and not on raw daily notes. With no Teams module, the sequence is the project status report if one is owed, what you shipped, and the review; the roll-up needs the Reports module.

1. The team statuses. One draft per team, from the tracker first and the vault second: five headings, one line per item, a source on every line, shown before it is saved as `Teams/Team Alpha/YYYY-MM-DD Team Alpha Status Report.md`. With each saved note you get the paste-ready copy. [Weekly status report](weekly-status-report.md) has the detail.

2. What you shipped, if you have repositories. Merged pull requests by repository, read with gh in each repository your hubs name, plus closed tickets and the week's log entries. The list is printed for the review; nothing is saved unless you ask. With the Specs switch on, the merged spec pull requests appear here on their own, the project status report takes spec lines under its headings, and the bookkeeping sets `status: done` and the Built by line on the note of every story that closed and refreshes each hub's Specs section.

3. The roll-up. `Reports/YYYY-MM-DD Weekly Roll-Up.md`, from this week's team and project reports, every hub's Risks and Open questions, the recipe in the Reports hub, and last week's roll-up: a three-line headline, one block per team or initiative with the delta since last week and a proposed traffic state, Risks new or changed, Decisions needed, Milestones in the next 30 days, and links to each team report. It declines while a team status is missing and offers to draft it first, and it refreshes Open asks of leadership in the Reports hub. Without the Reports module, a one-off roll-up goes to `Notes/` with the tag `rollup`.

4. Your review. `Notes/YYYY-MM-DD Weekly Review.md` with the tag `review`, from the week's daily notes, logs, reports, and the shipped list: What moved, What stalled, Promises kept and not kept, What to drop, Next week's three, and a paragraph for your team's update.

5. Proposals for your yes: new Current focus lines for `Home.md`, and a home for every note in `Notes/` older than 14 days that has none.

6. Delivery. You paste the paste-ready copies into Outlook, Teams, Word, or Loop, where Microsoft 365 Copilot can fit the house format.

7. Once a month, "Close the month". "Monthly review for [month]" writes `Reports/YYYY-MM-DD Monthly Review.md`, or `Notes/YYYY-MM-DD Monthly Review.md` with the tag `review` without the Reports module: outcomes against plan from the hubs' Milestones, decisions made with their status, risks opened and closed, priorities that changed, next month, asks. Then "What is stale or contradictory?": hubs past 30 days, repo hubs whose commit moved, Waiting on and open asks older than 30 days, outdated plans without a successor, notes that disagree, and, with the Specs switch on, spec notes in draft past 14 days, and a delivered spec whose note body differs from the repository file beyond its Delivered, Built by, and Revisions lines. Then proposals for your yes: projects to archive, a rollover for any running log past a few hundred lines, a new Current focus.

Where it asks: each team status is saved after your yes; the `Home.md` lines and the moves out of `Notes/` are proposals; a tracker tool that is not signed in gets one line, and the step continues from the vault.

## If your vault predates this ritual

A vault built with an older rulebook has no Reports hub and no named queries. Paste this on your reporting day with the brackets filled.

---

Close my week. Today is [date]. My teams are [Team Alpha, Team Beta]. My repositories are [owner/repo, one per line, or none]. My reports go to [audience, and where].

1. For each team, draft this week's status report: tracker first ([the filter, query, or project per team]), vault second (the hub, its check-in log or session log, last week's report), five headings (Done, In progress, Blocked or at risk, Decisions needed, Next), one line per item, every line ending with its source. Show each draft. After my yes, save it as a dated `type: report` note in the team folder, list it in the hub, and give me a paste-ready copy.
2. If I have repositories, list what I shipped this week: merged pull requests by repository with their URLs, including spec pull requests if I write stories, closed tickets, and the week's log entries.
3. Roll the team reports up for leadership: a three-line headline; one block per [team, or initiative] with the delta since last week and a traffic state marked as your proposal; risks new or changed with owner and age; the decisions I need with the ask, who decides, and by when; milestones in the next 30 days; links to each team report. Stop and offer to draft a missing team report first. After my yes, save it as a dated `type: report` note in [Reports/, or Notes/ with the tag rollup].
4. Write this week's review as a dated note in `Notes/` with the tag `review`, from the week's daily notes, logs, reports, and the shipped list: What moved, What stalled, Promises kept and not kept, What to drop, Next week's three, and a paragraph for my team's update.
5. Propose new Current focus lines for `Home.md` and a home for every note in `Notes/` older than 14 days that has none. Wait for my yes. Send nothing.

Next: [Context pack](context-pack.md)
