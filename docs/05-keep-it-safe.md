# 5. Keep it safe

The vault is work data on a work machine. Two things keep it safe: what you keep out of it, and what the AI tools are allowed to do with it.

## Know where the content goes

- When an AI tool reads a note, that text goes to the model provider your company has approved for that tool. Use only the tools your company has licensed and configured, signed in with your work account.
- The vault itself stays on your machine and in whatever backup your company allows. Obsidian uploads nothing unless you turn on a sync service.
- Treat the vault like an internal document. If something could not go on the company intranet, it does not go in the vault.

## What never goes in

- Credentials: passwords, API keys, tokens, connection strings, private keys. The command-line tools keep their own tokens in their own stores or in environment variables, never in a note.
- Customer data and other people's personal data. Names and roles in a team roster are fine. A customer record, a home address, or a health detail is not.
- HR matters: performance ratings, pay, disciplinary notes, anything from a 1:1 that the person would not want on a shared page. The vault tracks the work, not the person. A people file belongs in the HR system.
- Full copies of tracker items, documents, or emails that contain any of the above. Link, do not copy.
- Anything your company's AI policy or data classification rules exclude. When in doubt, leave it out. The rules tell the AI to flag anything that looks like it should not be there.

## What the AI tools are allowed to do

The build prompt writes these rules into `AGENTS.md`, and every tool reads them:

- Ask before changing anything you wrote. Show the before and after. One yes covers what was shown. Bookkeeping it owns, such as a hub's current state, the memory note, and the change log, it updates without asking and reports at the end.
- Never delete or rename. You do it in Obsidian, so links update.
- Stay inside the vault and the repositories you name. No other folders, no disk-wide searches, no controlling other apps, nothing that triggers an operating-system permission prompt.
- Read freely from trackers and repositories. Show every write command before running it.
- Never log in, store, or print tokens.

Keep the tool's own safety on as well. Claude Code and Copilot CLI ask before edits and commands by default. Codex's default preset edits inside the working folder on its own, so start it with the read-only sandbox if you want it to ask for every write. Never run a mode that skips permissions on the vault. Two layers: the rules in the vault, and the tool's own prompts.

## Backup and sync

- Preferred: a private repository in the company GitHub or Azure DevOps, under your work account. Ask the AI to turn the vault into a git repository, ignore Obsidian's workspace file, and show you the first commit before it is made.
- Also fine: the backup your company already runs on your machine.
- Not: personal cloud drives or sync accounts.
- Before the first push, ask the AI to check for anything that looks like a secret, or run the secret scanner your company provides.

## If something lands in the vault that should not be there

1. Delete it in Obsidian.
2. If the vault is in git, the content is still in the history. Recreate the repository, and if it was a credential, rotate it first and follow your company's incident process.
3. If an AI tool already read it, that text reached the provider. Report it the way your policy says.

## Sharing the setup with others

- Each person has their own vault. Nothing in it is shared by default.
- Share patterns, not notes: a template, a prompt, a how-to in `Library/`. This repository is the example: generic text, no names, no internal links, no company data.
