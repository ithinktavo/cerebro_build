# Cerebro: a notebook you and your AI tools share

Cerebro is a way to set up [Obsidian](https://obsidian.md) on your work machine so that one folder of plain Markdown notes is both your own notebook and the context your AI tools read first. One prompt builds it. You fill in a short profile, the AI proposes a design for your roles and tools, you say yes, and it builds the vault. From then on you type into one daily note, say a dozen fixed requests, and the AI files what you wrote, keeps the hubs current, and drafts your reports from sources instead of memory.

No plugins, no database, no account. Files you own, on a machine your company manages, that every tool with file access can read and that you paste into the ones without it.

## The problem it solves

- Every AI session starts from zero. You explain the project, the team, the decisions, and where the code is, again.
- Context lives in your head, in chat histories, in a dozen documents, and in the tracker. None of it is in one place.
- Status reports get rebuilt from memory every week.
- Things you capture during the day land in five places and get filed in none.

The vault gives the AI one place to read first, one rulebook that every tool follows, and the duty to keep the notes current as you work. You still decide what changes: the tools ask before they touch anything you wrote, and they never delete or rename.

## How it works

```
you ──► today's note ──► AI files it ──► hubs (projects, repos, teams, reports)
             ▲                              │
             └── "Start my day" ◄───────────┘ ◄── trackers and GitHub, read through their CLIs
```

1. The vault is a folder. Obsidian shows it as linked notes; the AI tools see files.
2. `AGENTS.md` at the root is the single rulebook. Codex and GitHub Copilot read it on their own. Claude Code reads `CLAUDE.md`, a pointer of one sentence and four `@` lines that loads it.
3. Every session starts the same way: the tool reads `Me.md` (who you are), `Home.md` (what is current), the AI memory note (open questions and decisions), then the hub of the project, repository, or team at hand.
4. Your day has two fixed moments. "Start my day" puts what matters at the top of today's note, from the hubs and the trackers. "Close my day" shows where each line you wrote belongs, and one yes files the batch.
5. Your week has one: "Close the week" drafts the team statuses, the roll-up for leadership, what you shipped, and the weekly review, every line with its source.

Your work trackers (GitHub Projects, Jira, Azure DevOps) and GitHub stay the systems of record. The vault links to items and never copies them, and the AI reads them through their command-line tools when you ask.

## Who it is for

| You are | You get | Start with |
| --- | --- | --- |
| A developer across several GitHub repositories | A hub per repository with how it really runs, projects that span repositories, one running log per project, pull requests linked from the notes, "Where did we leave off?" answered in ten lines | [roles/developer.md](roles/developer.md) |
| A manager, PM, or director across several teams | A hub per team with a check-in log, three named tracker queries per team, weekly status reports and a leadership roll-up drafted from sources, a monthly review | [roles/pm-director.md](roles/pm-director.md) |
| Both | One vault with every module on, one daily note, one set of rituals. Read both playbooks. | Either, then the other |

## Your notebook first

- Today's note is yours. Type into its Log as the day goes: a thought, a promise, what a standup said, a gotcha. The AI adds its own lines only under a visible `AI:` prefix and never edits yours.
- Ideas and things you learn go in `Notes/` with a tag. How-tos and checklists go in `Library/` once they are reusable.
- Notes you write by hand need no properties block. The AI treats them as information and changes them only with your yes.

## Set it up in 30 minutes

1. **Install Obsidian, create an empty vault, and turn on the Daily notes and Templates core plugins.** [docs/01-set-up-obsidian.md](docs/01-set-up-obsidian.md)
2. **Open a tool that can read and write the folder on the vault.** Claude Code (terminal or the desktop app's Code tab), Codex, or GitHub Copilot (CLI, or VS Code with the vault as the workspace). Claude chat, ChatGPT, and Microsoft 365 Copilot cannot create files; they join at step 6. [docs/02-connect-ai-tools.md](docs/02-connect-ai-tools.md)
3. **Fill in the profile in the build prompt and paste it.** Read the design it proposes, answer its questions or take the defaults, say yes. [prompts/build-work-vault.md](prompts/build-work-vault.md)
4. **Set the Obsidian settings it prints.** New note location, attachment folder, daily notes, templates.
5. **Connect your trackers.** Sign in once to `gh`, Jira's tool, or `az`, create three named queries per team, and say "Record these queries in the Team Alpha hub". [docs/03-connect-work-trackers.md](docs/03-connect-work-trackers.md)
6. **Say "Start my day".** The first week is laid out in [prompts/first-week.md](prompts/first-week.md). For chat tools, [prompts/context-pack.md](prompts/context-pack.md).

## What the vault looks like

Every vault shares the spine. The three modules switch on from your profile: Repos for people who name a repository, Teams for people who name a team, Reports for people who owe a recurring report across teams. A typical result for someone who is both a developer and a manager:

```
AGENTS.md        the single rulebook
CLAUDE.md        pointer for Claude Code
Me.md            who you are, what you own, your week, how you work with AI
Home.md          front door: current focus, what to say, one line per hub, trackers
Daily/           one note per work day, with Plan and Log
Notes/           ideas, learning notes, weekly reviews, notes with no hub
Library/         how-tos, checklists, the tracker commands, the vault's design record
Projects/        one folder per thing with a finish line: hub, running log, designs, decisions
Repos/           one folder per repository you work in: hub, log on first need, incidents
Teams/           one folder per team you lead or track: hub, check-in log, status reports
Reports/         recipes, open asks of leadership, weekly roll-ups, monthly reviews
System/
  Templates/     one template per kind of note
  Attachments/   images and exported documents
  AI/            the AI's own memory and change log
```

A complete example, with the design the AI proposed before building it and what it looks like after a week, is in [examples/](examples/).

## The rules it bakes in

- **One rulebook.** `AGENTS.md` holds every rule. Pointer files hold none.
- **Ask before changing what you wrote.** The tool shows the before and after and waits for your yes. One yes covers exactly what was shown. Its own bookkeeping, such as a hub's current state, the running logs, and its memory and log notes, it updates without asking and reports.
- **Never delete or rename.** The tool proposes it; you do it in Obsidian, so links stay intact.
- **Your lines are yours.** In the daily note the AI never edits, reorders, or ticks a line you wrote. Its lines start with `AI:`.
- **A fact lives in one note.** Hubs and `Home.md` quote it with a date and a link.
- **Code stays in repositories.** The vault records how each one really runs and what matters about it, and links pull requests and issues by URL.
- **Reality beats notes.** When a repository or a tracker contradicts a note, the tool updates the AI-maintained part and says so. Your words stay until you approve a change.
- **Every AI-written fact names its source.** A file and commit, a URL, or "said in chat" with the date. An inference is marked as one or goes under open questions.
- **Dated file names.** `YYYY-MM-DD Description.md`, so notes sort by time and names never collide.
- **No secrets, no customer data, no HR matters.** Names and roles only for other people. [docs/05-keep-it-safe.md](docs/05-keep-it-safe.md)

## Repository map

| Path | What it is |
| --- | --- |
| [prompts/build-work-vault.md](prompts/build-work-vault.md) | The build prompt: profile, design pass, build. The whole setup in one paste. |
| [prompts/](prompts/) | The rituals, one file each: the first week, the weekly status report, a team check-in, meeting notes, closing the week, the context pack for chat tools. |
| [docs/](docs/) | Step-by-step setup: Obsidian, AI tools, trackers, the daily and weekly rhythm, safety. |
| [roles/](roles/) | Playbooks for developers and for managers, PMs, and directors. |
| [examples/](examples/) | A vault built by the prompt for a placeholder persona, the design the AI proposed for it, and what the vault looks like after a week of use. |
| [presentation/](presentation/) | A short talk that introduces the setup, with speaker notes and a demo script. |

## Questions and fixes

Open an issue or a pull request in this repository. Keep contributions generic: no names, no internal URLs, no company data.
