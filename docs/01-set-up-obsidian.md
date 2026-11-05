# 1. Set up Obsidian

Obsidian is a note-taking app that works on a folder of plain Markdown files on your own machine. Nothing leaves the machine unless you turn on a sync service, and you need no account to use it. That is what makes it a good home for notes that AI tools read: the tools see ordinary files, and you see linked notes.

## Install

1. Check your company's software policy before installing anything. Obsidian is a desktop app with a local folder of files and no server of its own. It has been free to use at work since February 2025; the commercial license is optional.
2. Download it from [obsidian.md/download](https://obsidian.md/download) and install it like any app. On a managed Windows machine, use the installer or store route your IT team allows.
3. Open Obsidian, choose **Create new vault**, give it a name such as `Work`, and pick a local folder you control, such as `Documents/Vaults/Work`. Keep the path short and free of special characters, because the AI tools take it as their working folder.

Where to put the folder:

- A local folder is the simplest. The vault is only files, so back it up like other files (see Backup below).
- A folder that OneDrive or a similar service syncs by company policy is fine. If files with "conflict" in the name start to appear, the sync and the app are writing at the same time; move the vault to a local folder and back it up another way.
- Not a personal cloud account. This is work data.

## Turn on the core plugins

Settings, then Core plugins. Turn on:

- **Daily notes**: one note per day, created with one click or command.
- **Templates**: inserts a template into a note.
- **Slides**: presents a note as slides, split on `---` lines that have a blank line before and after them. Start it from the command palette or by right-clicking the note's tab and choosing Start presentation.

Backlinks, Outline, Search, and Quick switcher are on by default. Leave them on.

No community plugins are needed. The build prompt writes plain Markdown that works without them, so every AI tool and every future app can read the vault.

## Settings to set after the build

The build prompt prints these at the end. Set them in Settings:

- **Files and links, Default location for new notes**: In the folder specified below, `Notes`.
- **Files and links, Default location for new attachments**: In the folder specified below, `System/Attachments`.
- **Daily notes**: Date format `YYYY-MM-DD`, New file location `Daily`, Template file location `System/Templates/Daily Note Template`.
- **Templates**: Template folder location `System/Templates`.

## Five things to know about Obsidian

- A note is a `.md` file in the folder. Rename or move it inside Obsidian, so that links update.
- `[[Note Name]]` links to a note by name, wherever it sits. Names must be unique, which is why new file names carry a date.
- The block between two `---` lines at the top of a note holds its properties. The AI tools use them to find notes without opening them all.
- Ctrl or Cmd+O opens any note by name. Ctrl or Cmd+Shift+F searches text. Ctrl or Cmd+P runs any command.
- Folders are for people. Links do not care about folders, so moving a note never breaks a link.

## Backup

The vault is a folder. Treat it like any work document folder.

- Preferred: a private git repository in your company's GitHub or Azure DevOps, pushed by you or by the AI after it shows you the commit. Ask the AI to set it up once the vault exists.
- Also fine: the backup your company already runs on your machine.
- Not: personal cloud drives or a sync service on a personal account.

Next: [Connect your AI tools](02-connect-ai-tools.md).
