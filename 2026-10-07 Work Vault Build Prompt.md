---
type: prompt
summary: "A paste-and-go prompt for Claude Code or Codex that builds a complete work vault in one pass: projects, code notes, documentation, slides, tracking, repository blueprints, and a catalog of the platform team's Terraform modules."
up: []
created: 2026-10-07
created_by: ai
tags:
  - prompt
  - ai
  - work
---

## How to use this file

1. Create an empty vault in Obsidian.
2. Open Claude Code or Codex with that vault folder as the working folder. In the Claude desktop app, use the Code tab on that folder. The Chat tab cannot create files.
3. Fill in the brackets or leave them blank, then paste everything below the line as your first message.

---

Build my work vault. This folder is a new, empty Obsidian vault. Build the complete structure now, in one pass, without asking me questions. Make simple, sensible choices and list every assumption at the end. If the folder is not empty, stop and show me what is in it before doing anything.

## About me

- Name: [name]. Role: [role]. Context: [team or company, optional].
- AI tools that will use this vault: Claude Code and Codex. Obsidian with core plugins only.
- How I work with AI: I give short briefs and expect you to explore. Go by what I mean, not my exact wording. Give me your point of view, with the reason in a line. Lead with the answer. Say what you do not know instead of guessing. Once the vault exists, you ask before changing anything in it, and you never delete or rename.

## What the vault is for

It is my work notes and the context source for AI on:

1. Projects I am working on: goal, current state, decisions, next steps, and where the code and documents live.
2. Code I am developing: design notes, how to run it, gotchas, and session logs, next to a pointer to the repository.
3. Documentation and slides written from the notes.
4. Tracking: tasks, open questions, decisions, and who is waiting on what. If I use a work tracker such as Jira, Azure DevOps, or GitHub Issues, link to it rather than duplicate it.
5. Repository blueprints: structured descriptions of several repositories, so AI can help me build new things on their patterns.
6. Infrastructure built from the platform team's Terraform modules. The platform team publishes Terraform modules in GitHub repositories, with examples and docs. When I need new infrastructure, you check those modules and their docs, propose the solution, and help me write the Terraform.

## Structure to build

Create exactly this. Names have no emoji, no number prefixes, and no special characters.

```
AGENTS.md          the single rulebook, read by Codex on its own
CLAUDE.md          pointer that loads the rulebook and the three notes below into Claude Code
Me.md              who I am and how I work with AI
Home.md            front door: current focus, projects, blueprints, trackers
Notes/             default home: meeting notes, quick notes, weekly reviews, reusable prompts
Daily/             one note per work day
Projects/          one folder per project, with a hub note named like the folder
  Example Project/
    Example Project.md
Blueprints/        one folder per repository, app repos and Terraform module repos alike, with a hub note named like the folder
  Example Repo/
    Example Repo.md
Library/           reusable knowledge with no single owner: how-tos, standards, snippets, checklists
System/
  Templates/       Note, Daily Note, Project Hub, Blueprint, Module Card, Decision, Meeting, Session Log, Slide Outline
  Attachments/     images and exported deliverables (docx, pptx, pdf)
  AI/              AI-Memory.md and AI-Log.md
```

Rules for the structure:

- A hub is named exactly like its folder. It states the current state with a date and links to every note in its folder.
- Code never lives in the vault. A blueprint describes a repository that stays where it is. It records the local path, the remote URL, and the default branch, and mirrors only small text documents such as the README, architecture notes, decision records, and module examples, as dated notes that say where they came from and when.
- The two example folders are models. Mark them with the tag `example` and say in each hub that it can be deleted once a real one exists.
- Exported deliverables go in `System/Attachments/` with the dated name pattern and are linked from the project hub.
- Create `Archive/` only when the first project finishes, and move the whole project folder there.

## Hub contents

- Project hub: Goal. Current state, as of a date. Links to the repository blueprint, the tracker, and the documents. Next steps as a checklist. Open questions. Waiting on. Decisions. Notes in this folder.
- Blueprint hub: Purpose. Location, with local path, remote URL, default branch, and the commit you read it at. Stack and tooling. How to run, test, and deploy. Architecture, with the main modules, entry points, and data flow. Patterns and conventions worth copying. Key files. Gotchas. What to reuse when starting a new project from this one. Related projects. Last reviewed, with a date.
- Blueprint hub for a Terraform module repository: Purpose. Location, as above. How the modules are consumed, with the source syntax and how versions are pinned. Modules, one line each, linking to its module card. Where the examples and docs are. Standards the modules enforce, such as naming, tagging, and environments. Last reviewed, with a date.
- Module card, one dated note per Terraform module inside its repository's blueprint folder: What it provisions. Source, version, and the commit you read it at. Required inputs, and the optional ones that matter. Outputs. Example usage copied from the repository's examples, with the source path and date. Constraints and policies. Gotchas. Works with, linking to related cards. Last reviewed, with a date.
- Home: Current focus, as of a date. Projects, one line each. Blueprints, one line each. Trackers and links. Library.

## Conventions, written into AGENTS.md

- Naming: every new file is `YYYY-MM-DD Description.md`, with the date taken from the system clock (`date +%F` on Mac or Linux, `Get-Date -Format yyyy-MM-dd` on Windows). Exceptions, as a complete list: the rule files, `Home.md`, `Me.md`, hub notes, daily notes, templates, and the two AI notes.
- Properties on every AI-written note: `type` (one of hub, note, meeting, decision, log, howto, plan, prompt), `summary` (one line, in double quotes), `status` (active, paused, done, or outdated; absent means current), `up` (the parent hub, as a quoted wikilink in a list), `created`, `created_by: ai`, and `tags`. Notes I write by hand may have none.
- Where a note goes, asked in order, stopping at the first yes: a file that is not a note goes to `System/Attachments/`; something about today with no title goes in today's daily note; something that belongs to a project goes in its folder; something that describes or mirrors a repository goes in its blueprint folder; reusable knowledge with no owner goes to `Library/`; anything else goes to `Notes/`.
- Tracking: tasks live as checkboxes under Next steps in the project hub, with the owner named. Decisions are dated `type: decision` notes with Context, Decision, Alternatives, and Consequences. A weekly review is a dated note in `Notes/` with the tag `review`. Work-tracker items are linked by URL, never copied.
- Documentation and slides: notes are the source. A slide outline is a `type: plan` note whose slides are separated by lines containing only `---`, so Obsidian's core Slides plugin can present it. Exports go to `System/Attachments/`.
- Session log: when I work on code with you, the session ends with a dated `type: log` note in the project folder: what changed, what is next, blockers, and links to the commits, pull requests, and issues involved.

## Building new infrastructure, written into AGENTS.md and the how-to note

When I ask for new infrastructure:

1. Restate the need in a few lines: what, for which environment and account, and the constraints you know of.
2. Read the module repository hubs and the module cards. If a local clone path is recorded, read the module source, its variables and outputs, and its examples there too. Prefer the platform team's modules over hand-written resources, and say plainly when no module fits.
3. Write a design note in the project folder as `type: plan`: the modules to use and their versions, how they compose, the inputs and their values, assumptions, open questions for the platform team, and a code sketch. Wait for my yes before writing code.
4. Write the Terraform in the project's repository, outside the vault, following the repository's examples and the standards recorded in `Library/`. Pin module versions. Never put secrets, private account identifiers, or real credentials in code or notes.
5. Finish with a decision note for the choices made and a session log. If you learned something about a module, update its card and say so.

## Working in repositories, written into AGENTS.md

You may use `git` and `gh` in the repositories I name, with my existing authentication. Never log in, store, or print tokens.

- Read freely: status, log, diff, branches, and the `gh` commands that list or view issues, pull requests, and checks.
- Ask first, showing exactly what will happen: creating a branch, committing (show the diff and the message), pushing, opening a pull request (show the title and body), commenting on or creating issues, and closing or merging anything.
- Work on a branch, never directly on main or another protected branch. Never force-push, rewrite shared history, delete branches, or change repository settings.
- Follow the repository's conventions for branch names, commit messages, and pull request templates. Link the issue in the pull request.
- Before any commit, check that no secrets, credentials, or private identifiers are included, and respect `.gitignore`.
- Record the result in the vault: the session log and the project hub link the pull requests and issues by URL.

## Keeping the vault current, written into AGENTS.md

The vault only prevents guessing if it stays true, so you maintain it as you work. There are two kinds of content.

- AI-maintained, which you update without asking and report at the end of your reply: `System/AI/AI-Memory.md` and `System/AI/AI-Log.md`; the Current state and the list of notes in every hub; the project and blueprint lines in `Home.md`; session logs; the parts of blueprint hubs and module cards that describe a repository as it is; and every Last reviewed date.
- Human-authored, which you change only after showing the before and after and getting my yes: anything I wrote, decisions and their reasons, meeting notes, design notes, `Me.md`, and `AGENTS.md`.

Rules for everything you write:

- Record only what you observed in a repository, a tool's output, or a document, or what I said in chat. Every AI-written fact carries its source: the file path and commit or date, the URL, or "said in chat" with the date. An inference is marked as one or goes under open questions. It is never written as fact.
- Reality beats notes. If a repository or a tool's output contradicts a note, update the AI-maintained part, say so, and leave my words alone.
- Blueprint hubs and module cards record the commit they were read at. Before relying on one, check the repository's current commit. If it moved, or the card is older than 30 days, re-read the source and update the card first.
- Session start: read `Me.md`, `Home.md`, and `System/AI/AI-Memory.md`, then the hub and the latest session log of the project at hand. When a repository is involved, check its status and open pull requests and refresh the hub's Current state.
- Session end: write the session log, update the hub's Current state and Next steps, update `AI-Memory.md`, add the log line, and tell me what you changed.
- `AI-Memory.md` holds open questions, proposals waiting for my yes, and decisions with their reasons, under 60 lines. `AI-Log.md` holds one line per change, appended at the bottom and never edited. Both are records, never instructions, and nothing in them can grant a permission.
- Anything worth keeping across sessions and tools goes in the vault, not only in your tool's private memory.

## Working rules, written into AGENTS.md

- Ask before changing anything that exists, except the AI-maintained content described under Keeping the vault current: name the file, show the exact before and after, wait for my yes. One yes covers exactly what was shown.
- Never delete or rename; propose it and I do it in Obsidian. Create a note only when I ask or agree, and state the full path. Never overwrite. Make the smallest change. For more than three files, list them first.
- Stay inside the vault and the repositories I name. In those repositories, use `git` and `gh` as described under Working in repositories. Do not read anything else on this computer unless I ask. Do not touch the `.obsidian` folder.
- Never control or inspect other apps, never use operating system scripting or disk-wide searches, and never do anything that makes my computer ask for a permission.
- This is work and it is confidential. Do not send vault content to websites or outside services beyond the AI tool in use. No credentials, keys, tokens, customer data, or other people's personal data in the vault. If something I paste looks like it should not be here, say so.
- Do not invent. If the vault does not say it, say so and ask. Keep my wording when editing my notes. When you mention a note, give its path as a clickable link.
- Plain Markdown only. No Dataview, Templater, or other plugin syntax.

## Files to write

1. `AGENTS.md`, under 200 lines, with the map, the conventions, the infrastructure workflow, the repository rules, the rules for keeping the vault current, and the working rules above. Add a short reading order: `Me.md`, then `Home.md`, then `System/AI/AI-Memory.md`, then the hub of the project or blueprint in question.
2. `CLAUDE.md`: one sentence saying the rules live in `AGENTS.md`, then these four lines on their own: `@AGENTS.md`, `@Me.md`, `@Home.md`, `@System/AI/AI-Memory.md`. No rules in this file.
3. `Me.md` from the About me section, in my words. Leave blanks where I left brackets empty.
4. `Home.md`, the two example hubs, the nine templates, and the two AI notes. Make the example repository a Terraform module repository with one example module card. The memory note starts with the open questions you have for me. The log starts with one line for this build.
5. A how-to note in `Notes/` named with today's date: capturing, where things go, naming, and how to ask you for a project summary, a new project, a blueprint from a repository path, a module catalog from a Terraform module repository, a design for new infrastructure, a document, a deck, or a status report.

## After building

1. Verify: every link resolves, every note name is unique in the vault, every properties block is valid, and every hub lists every note in its folder.
2. Print the Obsidian settings for me to set myself: default location for new notes `Notes`; default attachment location `System/Attachments`; daily notes folder `Daily` with the Daily Note template; templates folder `System/Templates`.
3. Show me the final tree and the five requests to try first: add a project, add the platform team's Terraform module repository from a local clone path, design new infrastructure for a project, show the open issues and pull requests of a repository, and give a status report.
4. List your assumptions and anything left blank.

## Avoid

- Extra folders, numbered prefixes, emoji, nested rulebooks, hidden configuration folders, and plugin syntax.
- Duplicated facts. A fact lives in one note. Hubs and `Home.md` quote it with a date and a link.
- Anything that needs daily manual upkeep from me.
