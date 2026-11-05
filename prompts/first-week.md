# Your first week

The build ends with "Restart me, then say: Start my day." This page is the week that follows: what to say, in order, and what to expect at each step. Say each line to the AI tool opened on your vault root. Swap the placeholders (Team Alpha, checkout-api) for your own names; the Say section of your `Home.md` lists every phrase in those names.

Spread the steps over real days, so that the two daily rituals land on a real morning and a real evening. Stop at any step that does not behave as written and look at the list at the end of the page.

## The checklist

1. **Restart the tool.** Close the tool that ran the build, or end its session, and open it again on the vault folder. Rule files load at session start, so the build session has not read the `AGENTS.md` and `CLAUDE.md` it just wrote. Claude Code reads `CLAUDE.md`, which imports `AGENTS.md`; Codex and the GitHub Copilot CLI read `AGENTS.md` from the folder they start in; GitHub Copilot in VS Code reads it from the workspace root. See [Connect your AI tools](../docs/02-connect-ai-tools.md).

   ```
   /context all   # Claude Code only, inside the session: lists the memory files that loaded
   ```

2. **Check the reading order.** Say: "Read AGENTS.md and tell me the reading order." Expect: `Me.md`, then `Home.md`, then `System/AI/AI-Memory.md`, then the hub and the latest log entries of the thing at hand. Any other answer means the tool was opened on a subfolder or is still the build session. Fix that before going on.

3. **Start your day.** Say: "Start my day." Expect: today's note at `Daily/YYYY-MM-DD.md`, created from the template with `## Plan` and `## Log`, and under Plan at most ten lines that start with `AI:`, each ending with its source. On the first morning those lines are mostly the open questions from `AI-Memory.md` and the blanks from your profile. From the second morning on they also carry yesterday's unchecked Plan items, Waiting on items older than seven days, today's commitments from My week and each team's cadence, and the tracker reads: your open pull requests, the ones waiting for your review, the items assigned to you through the named queries, and each team's blocked query. A tool that is not signed in yet gets one `AI:` line saying so, and the ritual continues from the vault. "Start my day, vault only" skips the reads. The tool never reads a calendar or an inbox.

4. **Fill in the hubs.** Take the line for your role; a person who is both takes both.
   - Developer. Say: "Read my repos and fill in their hubs." Expect: for each repository in your profile, the tool reads the folder at the recorded path, runs the read-only git and gh commands the rulebook allows, and fills in `Repos/checkout-api/checkout-api.md`: Run and test, Conventions, Gotchas, a ten-line Architecture stamped with the commit it read, and Live views with the gh commands for your open pull requests, the ones awaiting your review, and failing checks. It writes nothing in the repository. Then try the loop: "Where did we leave off on checkout-api?" answers in ten lines. Work for a while. "Close the session" drafts the log entry from the git and gh history, appends it to the project or repo log, updates Current state and Next steps, proposes Gotchas, and adds one `AI:` pointer line to today's Log.
   - Manager, PM, or director. Say: "Add a team: Team Beta. Members: Alex Example, tech lead; [names and roles]. Reports through: [role]. Tracker: [GitHub Projects with the project number under YOURORG, Jira, or Azure DevOps]. Queries: [the three names or ids, or none yet]." Expect: a proposal for `Teams/Team Beta/` with its hub `Team Beta.md` and its running check-in log, shown in chat; the files after your yes; a line in `Home.md`; a line in `System/AI/AI-Log.md`. A team from your profile has its folder already; open its hub in Obsidian to see the blanks it still carries.

5. **Capture into Log.** During the day, type one line per thing as it happens under `## Log` in today's note, in Obsidian, in your own words. Or say "Add to today: [line]" and the tool appends your words as they are. Start a line with `[[Team Alpha]]` when you already know where it belongs; otherwise the tool infers the home from the words. Expect: nothing filed yet. The tool never edits, reorders, or ticks a line you wrote; its own lines start with `AI:`.

6. **Close your day.** Say: "Close my day." Expect: a filing table with one row per Log line since the last `AI: closed` marker: the line, its destination, the action. A check-in line becomes a dated entry in that team's log; a promise or a waiting-on line goes under Next steps or Waiting on in the right hub; a decided line becomes a decision note; a gotcha goes to the repo hub; an idea with a title becomes a note in `Notes/`; a line that belongs in a tracker is shown as a command on its own; a line that stays is marked stays; a line it cannot place is asked about. One yes applies the batch, each filed line gets ` → [[Hub]]` appended, and `AI: closed HH:MM` ends the section. You also get the list of what you promised and to whom, and a three-line summary. If you skip an evening, the next "Start my day" runs "Catch me up" over the unfiled lines first.

7. **Record your queries.** Outside the vault, sign in to the command-line tool of each tracker and create the three named queries per team: changed in the last 7 days; open and blocked; no change in 14 days; and one assigned-to-me query per tracker, recorded under Trackers and tools in `Home.md`. [Connect your work trackers](../docs/03-connect-work-trackers.md) shows how for each tracker. In Jira a query is a saved filter by name; in Azure DevOps a shared query by id; in GitHub Projects the project number under YOURORG plus a filter in the Projects filter syntax, or the field the tool should read when a filter cannot express the query. The gh project commands need the `project` scope on your login, and filtering with `--query` needs gh 2.87.0 or newer; check your version.

   ```
   gh auth refresh -s project   # add the project scope to an existing gh login
   ```

   Then say: "Record these queries in the Team Alpha hub: [the three names, ids, or filters]." Expect: the tracker lines of `Teams/Team Alpha/Team Alpha.md` and the Trackers and tools line in `Home.md` shown as before and after, written after your yes. Until the queries are recorded, status drafts carry marked blanks where the tracker items would be.

8. **Close the week.** On the reporting day from your profile, say: "Close the week." Expect, in order: a status draft per team, each shown before it is saved; "What did I ship this week?" if you have repositories; the roll-up in `Reports/`, which declines while a team status is missing and offers to draft it first; the weekly review in `Notes/`; then proposals for your yes: new Current focus lines for `Home.md` and a home for every note in `Notes/` older than 14 days. Each piece is also its own request. With no Teams module it runs the project status report if one is owed, what you shipped, and the review, and skips the roll-up. [Close the week](close-the-week.md) has the sequence; [Weekly status report](weekly-status-report.md) has the report and the paste-ready copy you deliver yourself.

9. **Reach the chat tools.** Say: "Context pack for Team Alpha." Expect one block printed in chat and nothing saved: the How I work with AI part of `Me.md`, Current focus from `Home.md`, the hub, the last three log entries, and for a repository its Run and test, Conventions, Gotchas, Architecture, and Live views run now, dated today. Paste it as the first message in Claude chat or ChatGPT. Paste what comes back to the folder tool with "from Claude chat, [date]" as its source. [Context pack](context-pack.md) has the detail. Microsoft 365 Copilot is where your reports go, not a reader of the vault.

By the end of the week you have five daily notes with filed Log lines, a hub with real content for each thing you own, a status report per team, and a weekly review. From here, [Working day to day](../docs/04-working-day-to-day.md) is the routine.

## If something goes wrong

- The tool edits without asking: "Stop. Re-read AGENTS.md. Show the before and after from now on." Check that it was opened on the vault root, not a subfolder, and that you restarted it after the build.
- It ticks, reorders, or rewrites a line you wrote in the daily note: "Stop. Lines I wrote are mine. Your lines start with AI:." The rule is in `AGENTS.md`; a reminder is enough.
- It cannot run the tracker command-line tool: the tool must work in a plain terminal first, signed in with your own account. See [Connect your work trackers](../docs/03-connect-work-trackers.md). Until then, "Start my day, vault only" and the vault side of every ritual still work.
- It states something you did not say and the vault does not hold: "Where does that come from? Mark it as an inference or remove it."
- It wants to rename or delete: it should propose it instead. Do it yourself in Obsidian, so links update.
- It reads a calendar, an inbox, or a folder outside the vault and the repositories in your hubs: "Stop. Stay inside the vault and the repos the hubs name." Never paste calendar or email text in.

Next: [Weekly status report](weekly-status-report.md)
