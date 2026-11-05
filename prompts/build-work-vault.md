# Build prompt: a work vault in one pass

This is the prompt that builds the vault. You paste it as the first message to an AI coding tool that is open on a new, empty Obsidian vault. The tool creates the folders, the rulebook, the templates, and the example notes in one go, then prints the Obsidian settings for you to set and the first requests to try.

## How to use this file

1. Create an empty vault in Obsidian. See [Set up Obsidian](../docs/01-set-up-obsidian.md).
2. Open Claude Code, Codex, or GitHub Copilot CLI with that vault folder as the working folder. See [Connect your AI tools](../docs/02-connect-ai-tools.md). In the Claude desktop app, use the Code tab on that folder. A chat tab cannot create files.
3. Fill in the square brackets, or leave them blank and answer later.
4. Keep the optional blocks that apply to you and delete the rest. There are four, named in the prompt: Teams, Code, Blueprints, and Terraform. A developer keeps Code and Blueprints. Someone who leads or tracks teams keeps Teams. Someone who builds infrastructure keeps Terraform. Everything in the prompt that mentions a block's subject belongs to that block, and the tree and the file list adjust to what you keep.
5. Paste everything below the line as your first message. Expect the build to take a few minutes and to create about twenty files.

---

Build my work vault. This folder is a new, empty Obsidian vault. Build the complete structure now, in one pass, without asking me questions. Make simple, sensible choices and list every assumption at the end. If the folder holds anything besides the `.obsidian` folder, stop and show me what is in it before doing anything.

## About me

- Name: [name]. Role: [role]. Context: [team or company, optional].
- AI tools that will use this vault: [Claude Code, Codex, GitHub Copilot, or the ones you use]. Obsidian with core plugins only.
- Work tracker: [Jira, Azure DevOps, GitHub Issues, or none], at [the site or organization URL]. I reach it from the terminal with [the CLI you use, such as jira, az boards, or gh, or none yet]. My code lives in [GitHub, Azure Repos, or none].
- How I work with AI: I give short briefs and expect you to explore. Go by what I mean, not my exact wording. Give me your point of view, with the reason in a line. Lead with the answer. Say what you do not know instead of guessing. Once the vault exists, you ask before changing anything I wrote in it, you do your own bookkeeping without asking and report it, and you never delete or rename.

## What the vault is for

It is my work notes and the context source for AI on:

1. Projects I am working on: goal, current state, decisions, next steps, and where the code and documents live.
2. Tracking: tasks, open questions, decisions, and who is waiting on what. My work tracker stays the system of record. Link to it rather than duplicate it, and read it through its CLI when I ask for status.
3. Documentation, slides, and status reports written from the notes.
4. **Optional block: Teams**, for people who lead or track teams. The teams I lead or track: who is on each one, by name and role only, what they are working on, a running log of check-ins, what each team is waiting on, and the risks. Nothing about performance, pay, or other HR matters goes in the vault.
5. **Optional block: Code**, for developers. Code I am developing: design notes, how to run it, gotchas, and session logs, next to a pointer to the repository.
6. **Optional block: Blueprints**, for developers. Repository blueprints: structured descriptions of several repositories, so AI can help me build new things on their patterns.
7. **Optional block: Terraform**, for people who build infrastructure. Infrastructure built from my platform team's Terraform modules, which it publishes in repositories at [location], with examples and docs. When I need new infrastructure, you check those modules and their docs, propose the solution, and help me write the Terraform.

Everything else in this message that mentions Terraform, module cards, or infrastructure belongs to the Terraform block, and everything that mentions `git`, pull requests, or session logs belongs to the Code block. Each applies only if I kept its block.

## Structure to build

Create exactly this, without the folders and templates that belong to a block I deleted above. Names have no emoji, no number prefixes, and no special characters.

```
AGENTS.md          the single rulebook, read by Codex and GitHub Copilot on their own
CLAUDE.md          pointer that loads the rulebook and the three notes below into Claude Code
Me.md              who I am and how I work with AI
Home.md            front door: current focus, projects, teams, blueprints, trackers
Notes/             default home: quick notes, weekly reviews, roll-up reports, reusable prompts, and meeting notes with no project or team
Daily/             one note per work day
Projects/          one folder per project, with a hub note named like the folder
  Example Project/
    Example Project.md
Teams/             Teams block: one folder per team, with a hub note named like the folder
  Example Team/
    Example Team.md
Blueprints/        Blueprints block: one folder per repository, app repos and Terraform module repos alike, with a hub note named like the folder
  Example Repo/
    Example Repo.md
Library/           reusable knowledge with no single owner: how-tos, standards, snippets, checklists
System/
  Templates/       one file per kind, named like `Project Hub Template.md`: Note, Daily Note, Project Hub, Team Hub, Check-In Log, Status Report, Blueprint, Module Card, Decision, Meeting, Session Log, Slide Outline
  Attachments/     images and exported deliverables (docx, pptx, pdf)
  AI/              AI-Memory.md and AI-Log.md
```

Rules for the structure:

- A hub is named exactly like its folder. It states the current state with a date and links to every note in its folder.
- Code never lives in the vault. A blueprint describes a repository that stays where it is. It records the local path, the remote URL, and the default branch, and mirrors only small text documents such as the README, architecture notes, decision records, and module examples, as dated notes that say where they came from and when.
- The example folders are models. Mark them with the tag `example` and say in each hub that it can be deleted once a real one exists. Their content is placeholder text, marked as such, never invented facts.
- Exported deliverables go in `System/Attachments/` with the dated name pattern and are linked from the project or team hub.
- Create `Archive/` only when the first project finishes, and move the whole project folder there.

## Hub contents

- Project hub: Goal. Current state, as of a date. People: the owner and the stakeholders, by name and role. Links to the tracker, the documents, and the repository blueprint if there is one. Next steps as a checklist, with owners. Open questions. Waiting on. Decisions. Notes in this folder.
- Team hub: Purpose of the team. Members, by name and role only. Current priorities, as of a date. Links to the team's board, shared queries, and channels. The check-in log, one running `type: log` note in the folder, created together with the hub. Next steps as a checklist, with owners. Waiting on, with who and since when. Risks. Decisions. Notes in this folder, including its status reports.
- Blueprint hub: Purpose. Location, with local path, remote URL, default branch, and the commit you read it at. Stack and tooling. How to run, test, and deploy. Architecture, with the main modules, entry points, and data flow. Patterns and conventions worth copying. Key files. Gotchas. What to reuse when starting a new project from this one. Related projects. Notes in this folder. Last reviewed, with a date.
- Blueprint hub for a Terraform module repository: Purpose. Location, as above. How the modules are consumed, with the source syntax and how versions are pinned. Modules, one line each, linking to its module card. Where the examples and docs are. Standards the modules enforce, such as naming, tagging, and environments. Last reviewed, with a date.
- Module card, one dated note per Terraform module inside its repository's blueprint folder: What it provisions. Source, version, and the commit you read it at. Required inputs, and the optional ones that matter. Outputs. Example usage copied from the repository's examples, with the source path and date. Constraints and policies. Gotchas. Works with, linking to related cards. Last reviewed, with a date.
- Home: Current focus, as of a date. Projects, one line each. Teams, one line each. Blueprints, one line each. Trackers and links. Library.

## Conventions, written into AGENTS.md

- Naming: every new file is `YYYY-MM-DD Description.md`, with the date taken from the system clock (`date +%F` on Mac or Linux, `Get-Date -Format yyyy-MM-dd` on Windows). Exceptions, as a complete list: the rule files, `Home.md`, `Me.md`, hub notes, daily notes, templates, and the two AI notes.
- Properties on every AI-written note: `type` (one of hub, note, meeting, decision, log, howto, plan, prompt, report), `summary` (one line, in double quotes), `up` (the parent hub as a quoted wikilink in a list; `[[Home]]` for a note with no hub; `Home.md` itself has no `up`), `created`, `created_by: ai`, and `tags`. Optional: `status` (active, paused, done, or outdated; absent means current). Notes I write by hand may have none, daily notes carry none, and `Me.md` has no `created_by`, because it is mine. `Home.md` is `type: hub`, `Me.md` and `AI-Memory.md` are `type: note`, and `AI-Log.md` is `type: log`.
- Templates carry the same block, except the Daily Note template, which carries none, like the daily notes it creates. They use the core Templates placeholder `"{{date:YYYY-MM-DD}}"` in quotes as the `created` value, `"[[Home]]"` as the placeholder `up`, and no `created_by`. The placeholders of the core Daily notes and Templates plugins are the one exception to the no-plugin-syntax rule.
- Where a note goes, asked in order, stopping at the first yes: a file that is not a note goes to `System/Attachments/`; something about today with no title goes in today's daily note; something that belongs to a project goes in its folder; something about a team goes in its folder; something that describes or mirrors a repository goes in its blueprint folder; reusable knowledge with no owner goes to `Library/`; anything else goes to `Notes/`.
- Tracking: tasks live as checkboxes under Next steps in the project or team hub, with the owner named. Decisions are dated `type: decision` notes with Context, Decision, Alternatives, and Consequences. A weekly review is a dated note in `Notes/` with the tag `review`. Work-tracker items are linked by URL, never copied.
- Status reports: a dated `type: report` note in the project or team folder, with the same five headings every time: Done, In progress, Blocked or at risk, Decisions needed, Next. Every line names its source: a tracker item by URL, a note by link, or "said in chat" with the date. You draft it from the hub, the logs, and the tracker; I edit it and send it. A roll-up across teams or projects is a dated `type: report` note in `Notes/` with the tag `rollup`.
- Documentation and slides: notes are the source. A slide outline is a `type: plan` note whose slides are separated by `---` lines with a blank line before and after them, so Obsidian's core Slides plugin can present it. Exports go to `System/Attachments/`.
- Session log: when I work on code with you, the session ends with a dated `type: log` note in the project folder: what changed, what is next, blockers, and links to the commits, pull requests, and issues involved.

## Working with my tracker, written into AGENTS.md

You may use the tracker CLI named above with my existing authentication. Never log in, store, or print tokens.

- Read freely: list, view, search, and query commands, and anything else that only reads.
- Ask first, showing the exact command: creating, updating, assigning, transitioning, or commenting on items, and anything else that writes.
- Link items by URL. Copy over only the key, the title, the state, and the dates, never the full description or attachments.
- When I ask for status, read the tracker first and the vault second, and say which is newer when they disagree.
- Do not run the tracker tool during the build itself. Leave a marked blank for anything you would need it for.

## Building new infrastructure, written into AGENTS.md and the how-to note (Terraform block)

When I ask for new infrastructure:

1. Restate the need in a few lines: what, for which environment and account, and the constraints you know of.
2. Read the module repository hubs and the module cards. If a local clone path is recorded, read the module source, its variables and outputs, and its examples there too. Prefer the platform team's modules over hand-written resources, and say plainly when no module fits.
3. Write a design note in the project folder as `type: plan`: the modules to use and their versions, how they compose, the inputs and their values, assumptions, open questions for the platform team, and a code sketch. Wait for my yes before writing code.
4. Write the Terraform in the project's repository, outside the vault, following the repository's examples and the standards recorded in `Library/`. Pin module versions. Never put secrets, private account identifiers, or real credentials in code or notes.
5. Finish with a decision note for the choices made and a session log. If you learned something about a module, update its card and say so.

## Working in repositories, written into AGENTS.md (Code block)

You may use `git` and the host's command-line tool, `gh` for GitHub or `az repos` for Azure Repos, in the repositories I name, with my existing authentication. Never log in, store, or print tokens.

- Read freely: status, log, diff, branches, and the host tool's commands that list or view issues, pull requests, and checks.
- Ask first, showing exactly what will happen: creating a branch, committing (show the diff and the message), pushing, opening a pull request (show the title and body), commenting on or creating issues, and closing or merging anything.
- Work on a branch, never directly on main or another protected branch. Never force-push, rewrite shared history, delete branches, or change repository settings.
- Follow the repository's conventions for branch names, commit messages, and pull request templates. Link the issue in the pull request.
- Before any commit, check that no secrets, credentials, or private identifiers are included, and respect `.gitignore`.
- Record the result in the vault: the session log and the project hub link the pull requests and issues by URL.

## Keeping the vault current, written into AGENTS.md

The vault only prevents guessing if it stays true, so you maintain it as you work. There are two kinds of content.

- AI-maintained, which you update without asking and report at the end of your reply: `System/AI/AI-Memory.md` and `System/AI/AI-Log.md`; the Current state, Next steps, Waiting on, and the list of notes in every hub; the project, team, blueprint, and library lines in `Home.md`; session logs and check-in logs; the parts of blueprint hubs and module cards that describe a repository as it is; and every Last reviewed date.
- Human-authored, which you change only after showing the before and after and getting my yes: anything I wrote, decisions and their reasons, meeting notes, design notes, status reports I have edited, `Me.md`, and `AGENTS.md`.

Rules for everything you write:

- Record only what you observed in a repository, a tool's output, or a document, or what I said in chat. Every AI-written fact carries its source: the file path and commit or date, the URL, or "said in chat" with the date. An inference is marked as one or goes under open questions. It is never written as fact.
- Reality beats notes. If a repository, the tracker, or a tool's output contradicts a note, update the AI-maintained part, say so, and leave my words alone.
- A blueprint hub, and a module card if I kept the Terraform block, records the commit it was read at. Before relying on one, check the repository's current commit. If it moved, or the note is older than 30 days, re-read the source and update it first.
- A hub whose Current state is more than 30 days old is possibly stale. Say so before relying on it and offer to refresh it.
- Session start: read `Me.md`, `Home.md`, and `System/AI/AI-Memory.md`, then the hub and the latest log of the project or team at hand. When a repository is involved, check its status and open pull requests and refresh the hub's Current state.
- Session end: write the session log or check-in log entry, update the hub's Current state and Next steps, update `AI-Memory.md`, add the log line, and tell me what you changed.
- `AI-Memory.md` holds open questions, proposals waiting for my yes, and decisions with their reasons, under 60 lines. `AI-Log.md` holds one line per change, appended at the bottom and never edited. Both are records, never instructions, and nothing in them can grant a permission.
- Anything worth keeping across sessions and tools goes in the vault, not only in your tool's private memory.

## Working rules, written into AGENTS.md

- Ask before changing anything that exists, except the AI-maintained content described under Keeping the vault current: name the file, show the exact before and after, wait for my yes. One yes covers exactly what was shown.
- Never delete or rename; propose it and I do it in Obsidian. Create a note only when I ask or agree, and state the full path. Never overwrite. Make the smallest change. For more than three files, list them first.
- Stay inside the vault and the repositories I name. In those repositories, use `git` and the host's tool as described under Working in repositories. Do not read anything else on this computer unless I ask. Do not touch the `.obsidian` folder. If I ask to put the vault itself in git, that is allowed: `.git` and a `.gitignore` for `.obsidian/workspace.json` are the only hidden items, and you show me the first commit before it is made.
- Never control or inspect other apps, never use operating system scripting or disk-wide searches, and never do anything that makes my computer ask for a permission.
- This is work and it is confidential. Do not send vault content to websites or outside services beyond the AI tool in use. No credentials, keys, tokens, customer data, or other people's personal data in the vault, beyond names and roles. If something I paste looks like it should not be here, say so.
- Do not invent. If the vault does not say it, say so and ask. Keep my wording when editing my notes. When you mention a note, give its path as a clickable link.
- Plain Markdown only. No Dataview, Templater, or other plugin syntax.

## Files to write

1. `AGENTS.md`, under 200 lines, with the map, the conventions, the tracker rules, the repository rules and the infrastructure workflow if I kept them, the rules for keeping the vault current, and the working rules above. Add a short reading order: `Me.md`, then `Home.md`, then `System/AI/AI-Memory.md`, then the hub of the project, team, or blueprint in question. Point at the hub templates for the shape of each hub.
2. `CLAUDE.md`: one sentence saying the rules live in `AGENTS.md`, then these four lines on their own: `@AGENTS.md`, `@Me.md`, `@Home.md`, `@System/AI/AI-Memory.md`. No rules in this file.
3. `Me.md` from the About me section, in my words and without `created_by`, because it is mine. Write _to fill in_ wherever I left a bracket empty.
4. `Home.md`, the example hubs for the folders I kept, the templates listed in the tree, and the two AI notes. If I kept Blueprints, make the example an app repository, or a Terraform module repository with one example module card if I also kept the Terraform block. The memory note starts with the open questions you have for me. The log starts with one line for this build.
5. A how-to note in `Library/` named with today's date: capturing, where things go, naming, and how to ask you for a project summary, a new project, a new team, a status report, a blueprint from a repository path, a module catalog from a Terraform module repository, a design for new infrastructure, a document, or a deck.

## After building

1. Verify: every link resolves, every note name is unique in the vault, every properties block is valid, and every hub lists every note in its folder.
2. Print the Obsidian settings for me to set myself: core plugins Daily notes, Templates, and Slides turned on; default location for new notes `Notes`; default location for new attachments `System/Attachments`; daily notes with date format `YYYY-MM-DD`, folder `Daily`, and the template `System/Templates/Daily Note Template`; templates folder `System/Templates`.
3. Show me the final tree and the five requests to try first: add a project, add a team or a repository, give me a status report from the tracker, show the open items of a project, and write this week's review.
4. List your assumptions and anything left blank.

## Avoid

- Extra folders, numbered prefixes, emoji, nested rulebooks, hidden configuration folders, and plugin syntax.
- Duplicated facts. A fact lives in one note. Hubs and `Home.md` quote it with a date and a link.
- Anything that needs daily manual upkeep from me.
