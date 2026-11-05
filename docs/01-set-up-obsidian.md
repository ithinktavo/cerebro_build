# 1. Set up Obsidian

Obsidian is a note-taking app that works on a folder of plain Markdown files on your own machine. Nothing leaves the machine unless you turn on a sync service, and you need no account to use it. That is what makes it a good home for notes that AI tools read: the tools see ordinary files, and you see linked notes. It is also your own notebook: today's daily note, meeting notes, decisions. The AI reads those too, which is the point.

## Install and create the vault

1. Check your company's software policy before installing anything. Obsidian is a desktop app with a local folder of files and no server of its own. It has been free to use at work since February 2025; the commercial license is optional.
2. Download it from [obsidian.md/download](https://obsidian.md/download) and install it like any app. On a managed Windows machine, use the installer or store route your IT team allows.
3. Open Obsidian, choose **Create new vault**, give it a name such as `Work`, and pick a local folder you control, such as `Documents/Vaults/Work`. Keep the path short and free of special characters, because the AI tools take it as their working folder. Where to put it:
   - Not inside a code repository, and no repository inside it. Code stays in its own folders; the vault only records where they are. Obsidian indexes every Markdown file under the vault folder, and the AI's "stay inside the vault" rule only means something when the vault is a folder of its own.
   - A local folder is the simplest. The vault is only files, so back it up like other files (see Backup below).
   - A folder that OneDrive syncs by company policy puts the vault inside Microsoft 365. Company search and Microsoft 365 Copilot may then reach its notes: you can attach the folder to a Copilot prompt yourself, and whether Copilot finds Markdown notes on its own depends on your tenant, so check your version. Choose that on purpose. This guide uses Microsoft 365 Copilot as the place reports go, not as a reader of the vault, so a local folder loses nothing. Sync can also leave files with "conflict" in the name when OneDrive and Obsidian or an AI tool write the same note at the same time. If they appear, move the vault to a local folder and back it up with git.
   - Not a personal cloud account. This is work data.
4. Turn on the core plugins. Settings, then Core plugins:
   - **Daily notes**: one note per day, created with one click or command. The build prompt expects it on.
   - **Templates**: inserts a template into a note. The build prompt expects it on.
   - **Slides**, optional: presents a note as slides, split on `---` lines that have a blank line before and after them. Start it from the command palette or by right-clicking the note's tab and choosing Start presentation. Turn it on if you want decks from your notes.
   - Backlinks, Outline, Search, and Quick switcher are on by default. Leave them on.
5. Leave the vault empty. The build prompt stops if the folder holds anything besides the `.obsidian` folder and offers only additions, so create no notes yet. The next page opens an AI tool on the folder, and [the build prompt](../prompts/build-work-vault.md) builds the vault. If you do not use a terminal, the Code tab of the Claude desktop app or VS Code with the vault open as the workspace can open the folder too; see [Connect your AI tools](02-connect-ai-tools.md).

No community plugins are needed. The build prompt writes plain Markdown that works without them, so every AI tool and every future app can read the vault.

## Settings to set after the build

Come back to this after the build prompt has run. The folders below do not exist before it, and Obsidian's folder pickers only offer folders that exist. The prompt prints the same list at the end of the build; the core plugins from step 4 are already on. Set these in Settings:

- **Files and links, Default location for new notes**: In the folder specified below, `Notes`.
- **Files and links, Default location for new attachments**: In the folder specified below, `System/Attachments`.
- **Files and links**: leave **Use [[Wikilinks]]** on and **New link format** at Shortest path when possible, so that links stay `[[Note Name]]`, the form the rulebook `AGENTS.md` and the AI's link checks expect.
- **Daily notes**: Date format `YYYY-MM-DD`, New file location `Daily`, Template file location `System/Templates/Daily Note Template`.
- **Templates**: Template folder location `System/Templates`.

## Six things to know about Obsidian

- A note is a `.md` file in the folder. Rename or move it inside Obsidian, so that links update.
- `[[Note Name]]` links to a note by name, wherever it sits. Names must be unique, which is why new file names carry a date.
- The block between two `---` lines at the top of a note holds its properties. The AI tools use them to find notes without opening them all.
- Today's daily note opens from the calendar icon in the ribbon, or with "Open today's daily note" in the command palette. It is where everything lands during the day, and the AI files it from there.
- Ctrl or Cmd+O opens any note by name. Ctrl or Cmd+Shift+F searches text. Ctrl or Cmd+P opens the command palette, which runs any command.
- Folders are for people. Links do not care about folders, so moving a note never breaks a link.

## If you already have notes

The build wants an empty folder, so existing notes come in afterwards. Current facts about a project or team fold into its hub: say "Fold these into the Team Alpha hub: [paste]" and approve the before and after. A how-to or checklist others could reuse goes to `Library/`. An old page you may need once becomes a dated attachment in `System/Attachments/`, linked from a hub. The rest stays where it is. Notes you write by hand need no properties, and the AI leaves them alone unless you ask.

## Backup

The vault is a folder. Treat it like any work document folder.

- Preferred: a private repository in your company's GitHub organization, under your work account. Not Azure DevOps, which this guide uses only as a tracker, and not a personal account. Ask the AI to set it up once the vault exists. It shows you the first commit before making it, and the only hidden items it adds are `.git` and a `.gitignore` for `.obsidian/workspace.json`. Pushes are yours, or the AI's after it shows you the commit.
- Once the vault is on GitHub, the tools that read GitHub repositories can read it too: Copilot on github.com, the GitHub app in ChatGPT, and the GitHub integration in Claude chat. Fine for work notes; know it, and see [Keep it safe](05-keep-it-safe.md).
- Also fine: the backup your company already runs on your machine.
- Not: personal cloud drives or a sync service on a personal account.

Next: [Connect your AI tools](02-connect-ai-tools.md).
