# Cerebro: a work vault your AI tools can read

Cerebro is a way to set up [Obsidian](https://obsidian.md) on your work machine so that one folder of plain Markdown notes is both your work notebook and the context that AI tools such as Claude Code, Codex, and GitHub Copilot read before they help you. It ships as one prompt: paste it into an AI coding tool opened on an empty vault, and the tool builds the whole structure in one pass.

No plugins, no database, no account. Files you own, on a machine your company manages, that every tool can read.

## The problem it solves

- Every AI session starts from zero. You explain the project, the team, the decisions, and where the code is, again.
- Context lives in your head, in chat histories, in a dozen documents, and in the tracker. None of it is in one place.
- Status reports get rebuilt from memory every week.

The vault gives the AI one place to read first, one rulebook that every tool follows, and the duty to keep the notes current as you work. You still decide what changes: the tools ask before they touch anything you wrote, and they never delete or rename.

## How it works

```
you ──► Obsidian vault ◄── AI tool ──► tracker and repository CLIs
        plain Markdown     Claude Code,    jira, az boards, gh
        on your machine    Codex, Copilot
```

1. The vault is a folder. Obsidian shows it as linked notes; the AI tools see files.
2. `AGENTS.md` at the root is the single rulebook. Codex and Copilot read it on their own. Claude Code reads `CLAUDE.md`, a pointer of one sentence and four `@` lines that loads it.
3. Every session starts the same way: the tool reads `Me.md` (who you are), `Home.md` (what is current), the AI memory note (open questions and decisions), then the hub of the project or team at hand.
4. The work happens: notes, status reports, meeting notes, session logs, code in the repositories outside the vault.
5. Every session ends with the tool updating the hub, the memory note, and the change log, and telling you what it changed.

Your work tracker (Jira, Azure DevOps, GitHub Issues) stays the system of record. The vault links to items and never copies them, and the AI reads the tracker through its command-line tool when you ask for status.

## Who it is for

| You are | You get | Start with |
| --- | --- | --- |
| A developer | Project hubs, repository blueprints, session logs, pull requests and issues linked from the notes | [roles/developer.md](roles/developer.md) |
| A manager or team lead | A hub per team, a check-in log, weekly status reports drafted from the tracker | [roles/manager.md](roles/manager.md) |
| In data governance or another tracking-heavy role | Initiative and team hubs, decision records, Azure DevOps or Jira queries turned into weekly reports | [roles/data-governance.md](roles/data-governance.md) |

## Set it up in 30 minutes

1. **Install Obsidian and create an empty vault.** [docs/01-set-up-obsidian.md](docs/01-set-up-obsidian.md)
2. **Open an AI coding tool on the vault folder.** Claude Code, Codex, or GitHub Copilot CLI. [docs/02-connect-ai-tools.md](docs/02-connect-ai-tools.md)
3. **Paste the build prompt.** Fill in the brackets, keep the optional blocks that apply to you, paste. The tool builds the vault and prints the Obsidian settings to set. [prompts/build-work-vault.md](prompts/build-work-vault.md)
4. **Set the four Obsidian settings it printed.** New note location, attachment folder, daily notes, templates.
5. **Connect your tracker.** Install the command-line tool for Jira, Azure DevOps, or GitHub, sign in once, and the AI can read it. [docs/03-connect-work-trackers.md](docs/03-connect-work-trackers.md)
6. **Try the first requests.** Add a project, add a team, ask for a status report. [prompts/first-session.md](prompts/first-session.md)

## What the vault looks like

```
AGENTS.md        the single rulebook
CLAUDE.md        pointer for Claude Code
Me.md            who you are and how you work with AI
Home.md          front door: current focus, projects, teams, blueprints
Notes/           default home: quick notes, weekly reviews, roll-ups, notes with no project or team
Daily/           one note per work day
Projects/        one folder per project, with a hub note named like the folder
Teams/           one folder per team you lead or track (optional)
Blueprints/      one folder per repository you want the AI to learn from (optional)
Library/         reusable knowledge: how-tos, standards, checklists
System/
  Templates/     note templates
  Attachments/   images and exported documents
  AI/            the AI's own memory and change log
```

A complete vault built by the prompt, for a placeholder persona, is in [examples/sample-vault/](examples/sample-vault/).

## The rules it bakes in

- **One rulebook.** `AGENTS.md` holds every rule. Pointer files hold none.
- **Ask before changing what you wrote.** The tool shows the before and after and waits for your yes. One yes covers exactly what was shown. Its own bookkeeping, such as a hub's current state and its memory and log notes, it updates without asking and reports.
- **Never delete or rename.** The tool proposes it; you do it in Obsidian, so links stay intact.
- **A fact lives in one note.** Hubs and `Home.md` quote it with a date and a link.
- **Code stays in repositories.** The vault records where the code is and what matters about it.
- **Reality beats notes.** When a repository or the tracker contradicts a note, the tool updates the note and says so.
- **Every AI-written fact names its source.** A file and commit, a URL, or "said in chat" with the date. An inference is marked as one or goes under open questions.
- **Dated file names.** `YYYY-MM-DD Description.md`, so notes sort by time and names never collide.
- **No secrets, no customer data, no HR matters.** [docs/05-keep-it-safe.md](docs/05-keep-it-safe.md)

## Repository map

| Path | What it is |
| --- | --- |
| [prompts/build-work-vault.md](prompts/build-work-vault.md) | The one-pass build prompt. The whole setup in one paste. |
| [prompts/](prompts/) | Reusable prompts: first session, weekly status report, team check-in, meeting notes. |
| [examples/](examples/) | A vault built by the prompt for a placeholder persona, so you can see the result before running it. |
| [docs/](docs/) | Step-by-step setup: Obsidian, AI tools, trackers, daily use, safety. |
| [roles/](roles/) | Playbooks for developers, managers, and data governance. |
| [presentation/](presentation/) | A short talk that introduces the setup, with speaker notes and a demo script. |

## Questions and fixes

Open an issue or a pull request in this repository. Keep contributions generic: no names, no internal URLs, no company data.
