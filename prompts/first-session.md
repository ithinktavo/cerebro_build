# Your first session: five requests to try

After the build, say these one at a time to the AI tool opened on your vault. Each one exercises a part of the setup, so you see what the tool does and where it asks for your yes.

**Check first.** "Read AGENTS.md and tell me the reading order, then summarize Home.md." Expect the four-file reading order and a nearly empty Home with the example hubs. If the tool cannot do this, it was not opened on the vault root.

1. **Add a project.** "Add a project: [name]. Goal: [one line]. Tracker: [URL]. Repository: [path, or none]." Expect a proposal for the folder and the hub shown in chat, the files after your yes, a line in `Home.md`, and a line in the change log.
2. **Add a team or a repository.** "Add a team: [name]. Members: [names and roles]. Board: [URL]." Or: "Make a blueprint of [repository path]." Expect a hub, read from the repository when you gave one, with sources and dates.
3. **Status from the tracker.** "Status report for [team or project] from [tracker] for this week." Expect the read commands to be visible as they run, then a five-heading draft, saved as a dated report note after your yes.
4. **Show open items.** "What is open on [project], who owns it, and what are we waiting on?" Expect an answer from the hub with links, and a warning if the hub is stale.
5. **Weekly review.** "Write this week's review." Expect a dated note in `Notes/` tagged `review`, built from the daily notes, the logs, and the reports.

Then delete the example folders in Obsidian once you have a real project and team. The tool will offer to update `Home.md`.

## If something goes wrong

- The tool edits without asking: "Stop. Re-read AGENTS.md. Show the before and after from now on." Check that it was opened on the vault root, not a subfolder.
- It cannot run the tracker command-line tool: the tool must work in a plain terminal first. See [Connect your work tracker](../docs/03-connect-work-trackers.md).
- It states something you did not say and the vault does not hold: "Where does that come from? Mark it as an inference or remove it." The rule is in `AGENTS.md`; a reminder is enough.
- It wants to rename or delete: it should propose it instead. Do it yourself in Obsidian, so links update.
