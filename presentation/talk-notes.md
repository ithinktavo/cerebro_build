# Speaker notes and demo script

The slides are in [talk-slides.md](talk-slides.md). To present from Obsidian, copy that file into a vault and run the core Slides plugin's "Start presentation" command. Each `---` line with a blank line before and after it is a slide break. The talk takes about ten minutes plus the demo.

## Notes per slide

**Title.** One sentence: "This is how I set up my notes so that the AI tools we already have know what I am working on, and so that my weekly status writes itself."

**The problem.** Ask who has explained the same project to an AI tool three times this week. The tracker has the tasks, but not the why, the decisions, or who is waiting on whom.

**The idea.** Obsidian is a desktop app over a folder of Markdown files. The AI coding tools the company provides, such as Claude Code, Codex, or Copilot, can all open a folder and read files. Put the notes in that folder, add one rulebook, and every tool starts informed. No plugins, no server, no new account.

**What is in it.** Keep this short: hubs. Every project, team, and repository has one note named like its folder that says what is current, with a date, and links to everything else. Home is the front door.

**How a session goes.** The rulebook makes every session the same shape. The tool reads before it writes, and ends by updating the hub and its own memory, so the next session, with any tool, starts where this one ended.

**The tracker.** The vault does not replace Jira or Azure DevOps. The AI reads the tracker through its command-line tool, with your own permissions, and links to items. Reads are free; writes are shown first. That is the rule that makes managers comfortable.

**Demo.** See the script below.

**Who it is for.** One line each. Point at the playbooks in the repository.

**Safety.** Two layers: the rules in the vault, and the tool's own permission prompts. Say out loud what never goes in: secrets, customer data, HR matters. Company tools, work accounts, company backup.

**Set up in 30 minutes.** The build prompt does the work. The person fills in a few brackets, keeps the blocks that apply to their role, pastes it, and sets four Obsidian settings.

**Where to start.** Offer to sit with anyone for thirty minutes to set it up. Suggest one project or one team as the first thing to put in.

## Demo script

Prepare the evening before:

1. A demo vault built with the build prompt, holding one example team with three or four members by role only, a check-in log with two dated entries, and last week's report. Use placeholder names and nothing from a real team.
2. The tracker command-line tool signed in on the demo machine, with one shared query or filter that returns a handful of items. Test it in a plain terminal.
3. A terminal window with the AI tool already open on the demo vault, and Obsidian open on the same vault in a second window.
4. A fallback: screenshots of each step, in case the network or the tool is slow.

The two-minute flow:

1. In Obsidian, show the team hub: priorities as of a date, waiting on, the check-in log. Thirty seconds.
2. In the terminal, say: "Status report for [team] for this week from the tracker." Narrate while it runs: it reads the query (show the command it ran), then the hub and the log, then drafts five headings.
3. Show the draft in chat. Point at the sources on each line. Say yes to saving it.
4. Back in Obsidian: the new dated report note in the team folder, the hub listing it, and the change log line at the bottom of the AI log.
5. Close: "That took two minutes and I edit it instead of writing it."

If time allows: "Log this check-in for [team]: [three lines]" and show the hub's Waiting on update with the before and after it asks you to approve.

## Questions to expect

- "Does my data go to the AI provider?" Yes, the notes the tool reads go to the provider your company approved for that tool, the same as any file you open with it today. The vault adds nothing new; it organizes what you already give the tools.
- "Can the AI change the tracker?" Only after showing the exact command and getting a yes. Reads are free.
- "What if I use a different tool?" Any tool that opens a folder and reads files works. The rulebook is a plain file.
- "How much upkeep?" The AI does the bookkeeping at the end of each session. You answer open questions when you have five minutes.
- "Can my team share one vault?" Each person has their own. Share templates and prompts, not notes.
