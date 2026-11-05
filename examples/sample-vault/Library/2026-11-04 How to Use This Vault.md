---
type: howto
summary: "How to use this vault: capturing, where things go, naming, and how to ask the AI for summaries, projects, teams, reports, blueprints, documents, and decks."
up:
  - "[[Home]]"
created: 2026-11-04
created_by: ai
tags:
  - howto
  - vault
---

The rules behind this note are in `AGENTS.md`. This is the short, practical version.

## Capturing

- A quick thought, a one-off list, or something about today: a line in today's daily note, `Daily/YYYY-MM-DD.md`. Obsidian's Daily notes command opens it.
- Anything with a title of its own: name the place, or let the AI place it with the order below. The AI creates the note with its properties and its line in the hub in one step, after a yes.
- A file that is not a note (image, docx, pptx, pdf): `System/Attachments/`, linked from the hub it belongs to.
- A tracker item: link it by URL, never copy it.

## Where things go

Ask in order and stop at the first yes:

1. Not a note (image, docx, pptx, pdf): `System/Attachments/`.
2. About today, with no title of its own: today's daily note.
3. Belongs to a project: `Projects/<Name>/`.
4. About a team: `Teams/<Name>/`.
5. Describes or mirrors a repository: `Blueprints/<Name>/`.
6. Reusable knowledge with no owner: `Library/`.
7. Anything else: `Notes/`. Weekly reviews (tag `review`) and roll-ups (tag `rollup`) live here.

## Naming

- `YYYY-MM-DD Description.md`, with the date from the system clock (`date +%F`) and a short Title Case description that makes sense without its folder.
- Exceptions: `AGENTS.md`, `CLAUDE.md`, `Home.md`, `Me.md`, hubs (named like their folder), daily notes, templates, `AI-Memory.md`, and `AI-Log.md`.
- Names are unique across the vault. No emoji, number prefixes, or special characters.

## How to ask the AI

Short briefs work. Examples, with what happens next:

- **A project summary.** "Summarize <project>." The AI reads the hub, the notes in its folder, and the tracker items linked from it, then answers with the state, next steps, open questions, and what is waiting, each with its source.
- **A new project.** "New project: <name>, goal <one line>, owner <name>, tracker <URL>." The AI proposes `Projects/<Name>/<Name>.md` from the Project Hub Template plus its line in `Home.md`, and creates both after a yes.
- **A new team.** "New team: <name>, members <names and roles>, board <URL>." The AI proposes the hub, its running check-in log, and the `Home.md` line.
- **A status report.** "Status report for <project or team>." The AI reads the tracker first (`az boards`), then the hub and its logs, and drafts a dated `type: report` note in that folder with Done, In progress, Blocked or at risk, Decisions needed, and Next. You edit it and send it. "Roll-up across all teams" gives one dated note in `Notes/` with the tag `rollup`.
- **A blueprint from a repository path.** "Blueprint <local path>." The AI reads the repository there with read-only `git` and `gh` commands, then proposes `Blueprints/<Name>/<Name>.md` from the Blueprint Template, with the commit it read, plus the `Home.md` line.
- **A document.** "Write the <kind of document> for <project> from the notes." The AI drafts it as a dated note in the project folder from the hub and its notes. An export (docx, pdf) goes to `System/Attachments/` and is linked from the hub.
- **A deck.** "Slide outline for <topic>." The AI writes a dated `type: plan` note with slides separated by `---` lines, which the core Slides plugin presents. A pptx export goes to `System/Attachments/`.
- **Open items.** "What is open on <project>?" The AI lists the unchecked Next steps, Open questions, and Waiting on from the hub, plus the open tracker items linked from it.
- **This week's review.** "Write this week's review." The AI drafts a dated note in `Notes/` with the tag `review` from the week's daily notes, logs, and hubs.

The AI asks before changing anything you wrote, keeps `System/AI/AI-Memory.md` and `System/AI/AI-Log.md` on its own, and reports what it changed at the end of each reply.
