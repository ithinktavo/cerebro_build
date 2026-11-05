# Speaker notes and demo script

The slides are in [talk-slides.md](talk-slides.md). To present from Obsidian, copy that file into a vault, turn on the core Slides plugin, open the file, and start the presentation from the command palette. Each `---` line with a blank line before and after it is a slide break. The talk takes about ten minutes, plus five for the demo.

The deck follows the design in [prompts/build-work-vault.md](../prompts/build-work-vault.md). Nothing in the slides or the demo names a real team, repository, or person. The placeholders are Alex Example, Team Alpha, Team Beta, and example-org/checkout-api.

## Notes per slide

**Title.** One sentence: "This is how I set up my notes so that the AI tools we already have know what I am working on, so that my weekly status writes itself, and so that a coding session starts where the last one ended." Say which tools you mean. Claude Code, Codex, and GitHub Copilot read the folder. Claude chat, ChatGPT, and Microsoft 365 Copilot get a pasted pack, which comes later in the deck.

**The problem.** Ask who has explained the same project to an AI tool three times this week. The tracker has the tasks, but not the why, the decisions, or who is waiting on whom. The fourth bullet is the one people recognize last: things they wrote down and never filed.

**The idea.** Obsidian is a desktop app over a folder of Markdown files. Claude Code, Codex, and GitHub Copilot in the CLI or in VS Code can all open a folder and read files. Put the notes in that folder, add one rulebook, and every tool starts informed. No community plugins, no server, no new account. The folder is your notebook first: one daily note, your ideas, what you learn.

**The build.** The person fills in a short profile, reads the design the AI proposes, answers up to five questions, says yes, and the AI builds the vault in one pass: the rulebook, Home, hubs for the real things they own, templates, and the rituals. Nothing is built in case. A module the profile did not call for is created on first use. If someone asks what the design looks like, show [examples/design-pass.md](../examples/design-pass.md).

**What is in it.** Keep this short. Every vault has the spine. Every project, team, and repository gets one hub note named like its folder, with Current state and a date, and one running log. `Home.md` is the front door, `Me.md` is who you are. A fact lives in one note; hubs and Home quote it with a date and a link. The three modules switch on from the profile: name a repository and you get `Repos/`, name a team and you get `Teams/`, owe a report across teams and you get `Reports/`.

**The daily loop.** The daily note has two sections, Plan and Log. "Start my day" creates today's note and puts at most ten lines under Plan, each with its source: unchecked items from yesterday, what the hubs say is next or waiting, what your week says is due, a team with no check-in yet this week, then your open pull requests and the items assigned to you in the trackers. It never reads a calendar or an inbox. During the day you type into Log, one line per thing, in your words. "Close my day" shows a filing table, one row per line: a check-in line becomes a dated entry in the team's log, a promise goes under Next steps in the right hub, a decision becomes a note, a line that belongs in the tracker is shown as a command. One yes applies the batch. The AI never edits a line you wrote; every line of its own starts with `AI:`.

**The weekly loop.** "Close the week" on your reporting day runs four things in order: a status report per team, with the same five headings every time and a source on every line; "What did I ship this week?" if you own repositories; the roll-up for leadership, which declines if a team status is missing; and your weekly review. The draft states the delta against last week and says where the tracker and the vault disagree. You edit, then paste the paste-ready copy where your reporting goes. "Close the month" adds the monthly review and a check for what is stale.

**The tracker.** The vault does not replace Jira, Azure DevOps, or GitHub Projects. The AI reads the tracker through its command-line tool, with your own sign-in, through three named queries per team: changed in the last seven days, open and blocked, no change in fourteen days. It copies only the key, title, state, owner, and dates, and links each item by URL. Reads are free; writes are shown first as the exact command. That is the rule that makes managers comfortable. A tool that is not signed in gets one line saying so, and the work continues from the vault. Details are in [docs/03-connect-work-trackers.md](../docs/03-connect-work-trackers.md).

**Demo.** See the script below.

**Who it is for.** One line each, then the last bullet: most people in the room are a developer and a manager at once, and they get one vault with every module on, one daily note, and one set of rituals. Point at the two role pages, [roles/developer.md](../roles/developer.md) and [roles/pm-director.md](../roles/pm-director.md).

**The chat tools.** Claude chat, ChatGPT, and Microsoft 365 Copilot cannot open the folder. For the first two, say "Context pack for [hub]" to a tool that can, and paste the block it prints as the first message: how you work with AI, the current focus, the hub, the last three log entries, and the live views with today's date. Whatever comes back is pasted to the vault tool with "from [tool], [date]" as its source. Microsoft 365 Copilot works in the other direction: you paste the paste-ready report into Outlook, Teams, Word, or Loop, and it fits the house format. A meeting recap from it comes back as three to five sourced lines, never a transcript. See [docs/02-connect-ai-tools.md](../docs/02-connect-ai-tools.md) and [prompts/context-pack.md](../prompts/context-pack.md).

**Safety.** Two layers: the rules in the vault, and the tool's own permission prompts. The AI asks before changing anything you wrote, never deletes or renames, and never sends anything; delivery is yours. Say out loud what never goes in: secrets, customer data, anything about other people beyond names and roles. Company-approved tools, work accounts, a folder the company backs up. See [docs/05-keep-it-safe.md](../docs/05-keep-it-safe.md).

**Set up in 30 minutes.** The build prompt does the work. The person fills in the profile, reads the design, says yes, and sets the Obsidian settings the prompt prints at the end. Then, outside the vault: sign in to the tracker's command-line tool, create the three named queries per team, and say "Record these queries in the [team] hub". The first week is scripted in [prompts/first-week.md](../prompts/first-week.md).

**Where to start.** Fill in the repository URL on the slide before the talk. Offer to sit with anyone for thirty minutes to set it up. Suggest one project or one team as the first thing to put in. The sample vault in [examples/](../examples/README.md) shows the result before anyone runs the prompt.

## Demo script

Prepare the evening before:

1. A demo vault built with the build prompt for the sample persona: Alex Example, a developer and manager who owns Team Alpha and Team Beta and the repository example-org/checkout-api. Give Team Alpha a check-in log with two dated entries from last week and last week's status report, so that the new report has a delta to show. Use placeholder names and nothing from a real team. The result should look like [examples/sample-vault/](../examples/sample-vault/).
2. The tracker's command-line tool signed in on the demo machine, with the three named queries for Team Alpha recorded in its hub and returning a handful of items. Test each query in a plain terminal.
3. The AI tool already open on the demo vault, in a terminal or in the Code tab of the Claude desktop app, and Obsidian open on the same vault in a second window.
4. End the preparation with "Close my day", so that the morning starts clean and "Start my day" does not run "Catch me up" first.
5. A fallback: a screenshot of each step below, in case the network or the tool is slow.

The five-minute flow:

1. In the terminal, say: "Start my day, vault only". Narrate: it takes the date from the clock, creates today's note from the template, and appends `AI:` lines under Plan: a Plan item carried from yesterday with the date it was first seen, a Waiting on line from the Team Alpha hub, the report due this week, and Team Beta with no check-in yet. Each line ends with its source. "Vault only" skips the tracker reads, so this step does not depend on the network. Show the note in Obsidian. One minute.
2. In Obsidian, type two lines under Log, in your own words: "Team Alpha standup: checkout-api release moved to Thursday, waiting on the security review from Team Beta" and "Promised my manager a roll-up draft by Friday". Thirty seconds.
3. In the terminal, say: "Close my day". Show the filing table: the first line becomes a dated entry in the Team Alpha check-in log plus a Waiting on line in the Team Alpha hub; the second goes under Next steps in the Reports hub with you as the owner and Friday as the date, and is listed under what you promised. Say yes. Back in Obsidian: the filing marker after each line, the `AI: closed` line at the end of Log, and the new entry in the check-in log. One minute.
4. In the terminal, say: "Status report for Team Alpha for this week". Narrate while it runs: it reads the three named queries (show the commands it ran), then the check-in log entries of the last seven days, the hub, and last week's report, then drafts the five headings: Done, In progress, Blocked or at risk, Decisions needed, Next. Point at the source at the end of each line, and at the line that says where the tracker and the vault disagree. Say yes to saving it. Two minutes.
5. In Obsidian: the new dated report note in the Team Alpha folder, the hub listing it, the paste-ready copy, and the change-log line at the bottom of `System/AI/AI-Log.md`. Thirty seconds.
6. Close: "That took five minutes, and I edit it instead of writing it."

If time allows, the developer beat: "Where did we leave off on checkout-api?". It reads the hub and the last three log entries, runs the git and gh reads in the repository the hub names, refreshes Current state, and answers in ten lines: where we left off and when, what moved since, what is next, what is waiting. This needs a local clone of a placeholder repository on the demo machine; skip it if there is none.

If the tracker tool fails during the demo, let it. One `AI:` line says so, and the report draft continues from the vault. That is the designed behaviour and worth a sentence.

The fallback: keep one screenshot per step in a folder on the desktop, in the order above, and narrate them the same way. The two Log lines and the filing table are the screenshots that carry the argument, so take those first.

## Questions to expect

- "Does my data go to the AI provider?" Yes, the notes the tool reads go to the provider your company approved for that tool, the same as any file you open with it today. The vault adds nothing new; it organizes what you already give the tools.
- "Can the AI change the tracker?" Only after showing the exact command and getting a yes. Reads are free. It links items by URL and copies only the key, title, state, owner, and dates.
- "Does it replace Jira, Azure DevOps, or GitHub Projects?" No. They stay the system of record. The vault holds the why, the decisions, and who is waiting on whom.
- "What if I use a different tool?" Any tool that opens a folder and reads files works: Claude Code, Codex, or GitHub Copilot in the CLI or in VS Code. The rulebook is a plain file.
- "I only use Claude chat, ChatGPT, or Microsoft 365 Copilot." They cannot open the folder. Ask a tool that can for "Context pack for [hub]" and paste the block in as the first message, or paste `Me.md` and the hub yourself. Microsoft 365 Copilot is where your reports go, not a reader of the vault. Only the build and the bookkeeping need a tool that reads the folder; the rest works by paste.
- "Do I need the terminal?" Not for the daily work. The one-time sign-in to a tracker's command-line tool happens in a terminal; everything else runs in the Code tab of the Claude desktop app or in VS Code with the vault open as the workspace.
- "How much upkeep?" You type Log lines during the day and say yes at "Close my day". The AI does the bookkeeping: the logs, the hubs, its memory, the change log. You answer open questions when you have five minutes.
- "Can I keep my own notes in it?" Yes: ideas, learning notes, how-tos; it is your notebook first. Not private-life matters: it is a work machine, and the rulebook keeps performance, pay, health, and personal matters out.
- "I am a developer and a manager. Two vaults?" One vault with every module on, one daily note, one set of rituals. The daily loop is the same; the weekly loop adds "What did I ship this week?".
- "What about my 1:1 notes?" Off unless you said yes in the profile. Then one running log per direct report, work topics only, never included in a context pack unless you ask.
- "Can my team share one vault?" Each person has their own. Share templates and prompts, not notes.

Next: [The sample vault](../examples/README.md).
