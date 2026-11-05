# Weekly status report

One note per team or project per week: five headings, one line per item, every line ending with its source, and a paste-ready copy for Outlook, Teams, Word, or Loop. The build prompt writes this ritual into your vault; this page says what to say and what to expect. The roll-up across teams, for a director or a program lead, is the last step on the page.

## What to say

- "Weekly status for all my teams" runs the report for every team, one draft at a time.
- "Status report for Team Alpha for this week" runs it for one team or project. Use your own names, as the Say section of `Home.md` lists them.
- "Roll up this week for leadership" writes the roll-up from this week's team and project reports.

On your reporting day, "Close the week" runs all three in order. See [Close the week](close-the-week.md).

## What happens

1. The tracker first. The tool runs the three named queries recorded in the hub: changed in the last 7 days; open and blocked; no change in 14 days. What the hub records depends on the tracker:
   - GitHub Projects: the project number under YOURORG and a filter per query in the Projects filter syntax, or the field to read when a filter cannot express the query. The read is `gh project item-list`, which needs the `project` scope on your gh login. Filtering on the server with `--query` needs gh 2.87.0 or newer; check your version.
   - Jira: a saved filter per query, by name.
   - Azure DevOps: a shared query per query, by id.
   - GitHub repositories, for a project served by repositories or for your own work: pull requests merged in the last seven days, the open ones, and the open issues, read with gh in each repository the hub names. Every command names the repository with `-R`, so that it never depends on the folder it runs in.

   ```
   gh project item-list <number> --owner YOURORG --format json --limit 100   # the items as JSON; the default limit is 30
   gh project item-list <number> --owner YOURORG --query "-status:Done"      # filtered on the server; gh 2.87.0 or newer
   ```

   It copies only key, title, state, owner, and dates, and links every item by URL. A tracker tool that is not signed in or that fails is named in one line, and the draft continues from the vault. The exact commands per tracker are in your `Library/YYYY-MM-DD Tracker Commands.md` note; [Connect your work trackers](../docs/03-connect-work-trackers.md) shows how to set each one up.

2. The vault second: the check-in log entries of the last seven days, or for a project its session log and the meeting and decision notes since last week; the hub's priorities, Waiting on, Risks, Open questions, and Milestones; and last week's report, so that last week's Next becomes Done or In progress and what did not happen is named. Daily notes are not a source. Run "Close my day" or "Catch me up" first, so that the week's Log lines are filed where the report will find them.

3. The draft. The same five headings every time: Done, In progress, Blocked or at risk, Decisions needed, Next. One line per item, under a page, no adjectives. Every line ends with its source: a tracker item by URL, a note by link, or "said in chat" with the date. The draft states the deltas since last week, and where the tracker and the vault disagree it says so and which is newer. Open questions go under Decisions needed. It writes nothing it cannot source.

4. Your yes. The draft is shown in chat and saved after you say yes, as `Teams/Team Alpha/YYYY-MM-DD Team Alpha Status Report.md` with `type: report`, listed in the hub. A project report goes in its project folder the same way. Nothing is sent anywhere.

5. The paste-ready copy. With the saved note you get a second copy to paste: wikilinks turned into plain titles, tracker URLs kept, the sources moved to a short list at the end. You paste it into Outlook, Teams, Word, or Loop, where Microsoft 365 Copilot can fit the house format. Delivery is yours; the tool never sends.

6. The roll-up. "Roll up this week for leadership" reads this week's team and project reports, every hub's Risks and Open questions, the recipe in the Reports hub (who reads it, on which day, and whether leadership reads by team or by initiative), and last week's roll-up. It writes `Reports/YYYY-MM-DD Weekly Roll-Up.md` with:
   - a three-line headline;
   - one block per team or initiative, grouped the way the recipe says leadership reads, with the delta since last week and a traffic state the tool proposes and marks as a proposal until you set it;
   - Risks new or changed, with owner and age;
   - Decisions needed, with the ask, who decides, and by when;
   - Milestones in the next 30 days;
   - links to each team report.

   It declines while a team status is missing and offers to draft that first. Each run refreshes Open asks of leadership in the Reports hub. A vault without the Reports module files a one-off roll-up in `Notes/` with the tag `rollup`. Ask for the paste-ready copy of the roll-up the same way as for a team report.

## If your vault predates this ritual

A vault built with an older rulebook has no named queries in its hubs and no Reports hub. Paste the block below with the brackets filled, or save it as a dated `type: prompt` note (`Library/` in a vault built with this prompt, `Notes/` in an older one) and run it by name.

---

Write this week's status report for [team or project].

1. Read the tracker first. [Jira: run the saved filter [name]. Azure DevOps: run the shared query [id]. GitHub Projects: read project [number] under [owner] and group by [status field]. GitHub repositories: read the pull requests merged in the last 7 days, the open ones, and the open issues in [owner/repo, one per line].] Group the items: closed this week, in progress, no change in 14 days, blocked. Copy only key, title, state, owner, and dates, and link each item by URL. If a tool is not signed in, say so in one line and continue from the vault.
2. Then read the vault: the hub, its check-in log or session log, the meeting and decision notes since last week, and last week's report. Say where the tracker and the vault disagree, and which is newer.
3. Draft the report with these five headings and nothing else: Done, In progress, Blocked or at risk, Decisions needed, Next. One line per item. Every line ends with its source: the tracker item URL, the note link, or "said in chat" with the date. Write nothing you cannot source. State what changed since last week's report and name what did not happen. Put open questions under Decisions needed.
4. Keep it under one page. Plain words, no adjectives.
5. Show me the draft. After my yes, save it as a dated `type: report` note in the [team or project] folder and add it to the hub's list of notes. Do not send it anywhere.
6. Then give me a paste-ready copy: wikilinks turned into plain titles, tracker URLs kept, the sources moved to a short list at the end. I paste it into [Outlook, Teams, Word, or Loop] myself.

For the roll-up, paste this once the team reports exist:

---

Roll up this week's reports for [Team Alpha, Team Beta]. Read each team's report for this week, the Risks and Open questions in every hub, and last week's roll-up if there is one. Write a three-line headline; one block per [team, or initiative, as leadership reads it] with the delta since last week and a traffic state marked as your proposal; risks new or changed with owner and age; the decisions I need from leadership with the ask, who decides, and by when; milestones in the next 30 days; a link to each team report. Keep every line's source. If a team's report is missing, stop and offer to draft it first. Show me the draft. After my yes, save it as a dated `type: report` note in [Reports/, or Notes/ with the tag rollup] and give me a paste-ready copy.

Next: [Team check-in](team-check-in.md)
