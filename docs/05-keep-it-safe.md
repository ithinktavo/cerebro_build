# 5. Keep it safe

The vault is work data on a work machine. Two things keep it safe: what you keep out of it, and what the AI tools are allowed to do with it. Settle both before the first note, then back the vault up where your company can see it.

## Know where the content goes

- When a tool that opens the folder reads a note, that text goes to the model provider your company has approved for that tool. Use only the tools your company has licensed and configured, signed in with your work account.
- Pasting a note into a chat app is the same as the tool reading it. Claude chat, ChatGPT, and Microsoft 365 Copilot cannot open the folder, so they see what you paste or upload. Use the licensed version of each, signed in with your work account, never the free or personal version of the same product. That is a different service with different data terms. On ChatGPT's consumer plans, for example, content it reads from other apps becomes chat history and may be used for training.
- Paste only what the task needs. "Context pack for Team Alpha" prints one hub with its context, not the whole vault, and it never includes one-on-one logs unless you ask. See [Connect your AI tools](02-connect-ai-tools.md) and [the context pack](../prompts/context-pack.md).
- A delivered spec leaves the vault only into the company's repository or tracker; a spec pasted into a chat tool follows the context-pack rule.
- Files you upload to a Claude Project or a ChatGPT Project stay in that project for every later chat. Use a project under your work account, and remove what the work no longer needs. In ChatGPT, set a work project to project-only memory. A file you upload to Microsoft 365 Copilot is saved as a copy in your OneDrive.
- The vault itself stays on your machine and in whatever backup your company allows. Obsidian uploads nothing unless you turn on a sync service.
- Treat the vault like an internal document. If something could not go on the company intranet, it does not go in the vault.

## What never goes in

- Credentials: passwords, API keys, tokens, connection strings, private keys. The command-line tools keep their own tokens in their own stores or in environment variables, never in a note.
- Customer data and other people's personal data. Names and roles are all the vault holds about other people. A team roster with names and roles is fine. A customer record, a home address, or a health detail is not.
- Customer records, production values, or log lines in a spec. A spec is committed to a repository that everyone with access and their coding agents read; it names fields and shapes with made-up sample values, and the AI replaces what looks like a record in a story or a pasted summary with a placeholder and says so: a customer, an account, a record, a log line, a production value, an internal hostname, an IP address, or a request, session, or trace id. An image or screenshot pasted into the chat is read for field names and shapes only, its values become placeholders, and it is never saved in the vault or linked from a spec. A tracker export (CSV, Excel, a board printed to PDF) is read like the story, for keys, titles, states, owners, and dates, pasted nowhere and never saved. A spec is as public as the repository it lands in and the story it is commented on.
- HR matters: performance ratings, pay, disciplinary notes, anything from a 1:1 that the person would not want on a shared page. The vault tracks the work, not the person. A people file belongs in the HR system. One-on-one logs are opt-in, off by default, and hold work topics only. There is no People folder anywhere in the vault.
- Full copies of tracker items, documents, or emails that contain any of the above. Link, do not copy. From a tracker item the AI copies only the key, title, state, owner, and dates, never descriptions or attachments.
- Teams transcripts and Copilot meeting recaps, pasted whole. They carry other people's words and side remarks. What lands in the vault is a meeting note: the decisions and the actions, attendees by name and role, and the source named with its date. A recap comes back as three to five sourced lines, never as a transcript. Link the recording if your policy keeps one. See [meeting notes](../prompts/meeting-notes.md).
- Calendar and email text. Never paste it into the vault. The AI never reads a calendar or an inbox.
- Anything your company's AI policy or data classification rules exclude. When in doubt, leave it out. The rules tell the AI to say so and leave it out when something you paste looks like it should not be there.

## Your own notes

- Work-adjacent notes are fine here: ideas, reading notes, how-tos, things you learn, career plans. They pass the intranet test.
- Private-life, health, and finance notes do not. They belong in a separate vault on a personal machine, never in this one.

## What the AI tools are allowed to do

The build prompt writes these rules into `AGENTS.md`, and every tool opened on the folder reads them:

- Ask before changing anything you wrote. Show the before and after. One yes covers what was shown. Bookkeeping it owns, such as a hub's current state, the running logs, the memory note, and the change log, it updates without asking and reports at the end.
- Never delete or rename. You do it in Obsidian, so links update.
- Stay inside the vault and the repositories you name. No other folders, no disk-wide searches, no controlling other apps, nothing that triggers an operating-system permission prompt.
- Read freely from trackers and repositories. Show every write command before running it. In a repository: work on a branch, never force-push or rewrite shared history, never change repository settings, and check for secrets, and for customer or production data in a spec, before every commit.
- Never log in, store, or print tokens.
- Write nothing it cannot source. Every fact names a file, a URL, or "said in chat" with the date. An inference is marked as one or goes under open questions.

A chat app gets none of these rules. It cannot change the vault, so there is nothing to approve. What you paste in and what you copy back are your call, and anything you copy back carries its source, such as "from ChatGPT, 2026-11-05".

Keep each tool's own safety on as well. Two layers: the rules in the vault, and the tool's own prompts.

- Claude Code: in the desktop app's Code tab, keep Manual mode, so Claude proposes each edit, and do not switch to Auto. In the terminal, keep the default mode and never start it with the flag that skips permissions.
- GitHub Copilot in VS Code: it applies file edits as pending changes that you keep or undo, so review the pending changes before you keep them (check your version). New sessions start on Manual permissions, and a terminal command that is not auto-approved asks you first. Leave the auto-approve settings off: keep `chat.tools.global.autoApprove` at its default, false, because VS Code says that turning it on disables critical security protections, and keep `chat.permissions.default` at its default, Manual permissions. To send every terminal command through the prompt, set `chat.tools.terminal.enableAutoApprove` to false.
- GitHub Copilot CLI: it does not inherit VS Code's settings. Check your version for its own approval prompts before you point it at the vault.
- Codex: start it with the read-only sandbox if you want it to ask before every write. Check your version for how the sandbox is set.
- Never run a mode that skips permissions on the vault, in any tool.

## Backup and sync

- Preferred: a private repository in your company's GitHub organization (YOURORG), not under your personal GitHub user. A repository under your own user is not company-controlled and leaves with you. One in the organization can be read by organization administrators and by anyone granted access, which is one more reason the HR and customer-data rules above are absolute. Ask the AI to turn the vault into a git repository. `.git` and a `.gitignore` for `.obsidian/workspace.json` are the only hidden items it adds, and it shows you the first commit before it is made.
- Also fine: the backup your company already runs on your machine.
- Not: personal cloud drives or sync accounts.
- Before the first push, ask the AI to check for anything that looks like a secret, or run the secret scanner your company provides. Ask your administrators whether the organization's repositories have secret scanning and push protection turned on. They catch what you miss, and they are not a reason to skip the check.

## If something lands in the vault that should not be there

1. Delete it in Obsidian. Then empty the system trash, because Obsidian moves deleted files there by default, and clear the File recovery snapshots in Obsidian's settings, because that core plugin keeps copies of recent changes. Check your version for where these settings sit.
2. If the vault is in git, the content is still in the history. Recreate the repository. If it was a credential, rotate it first and follow your company's incident process.
3. If an AI tool already read it, that text reached the provider. Report it the way your policy says. The coding tools may also keep session history on your machine. Ask the tool where it keeps its sessions and delete the one that saw it (check your version).

## Sharing the setup with others

- Each person has their own vault. Nothing in it is shared by default. If it is backed up to the company organization, that repository's administrators can read it.
- Share patterns, not notes: a template, a prompt, a how-to in `Library/`. This repository is the example: generic text, no names, no internal links, no company data.

Next: your playbook, [Developer](../roles/developer.md), [Managers, PMs, and directors](../roles/pm-director.md), or [Product owners](../roles/product-owner.md).
