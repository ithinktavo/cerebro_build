# 2. Connect your AI tools

The vault works with any AI tool that can open a folder, read files, and run commands. Each tool reads a rule file when it starts in the vault folder, so the rules travel with the vault and not with the tool. Claude Code, Codex, and GitHub Copilot can open the folder, and they are set up first. Claude chat, ChatGPT, Microsoft 365 Copilot, and Copilot Chat on github.com cannot open a folder on your computer. The end of this page says how the vault serves them anyway.

## The one rule that matters

Open the tool with the vault folder as its working folder. From a terminal:

```bash
cd ~/Documents/Vaults/Work    # your vault folder
claude                        # or: codex   or: copilot
```

In the Claude desktop app, open the Code tab on the vault folder. In VS Code, open the vault folder as the workspace. A tool opened one level up or one level down does not find the rules. Codex is the strictest: when the folder is not a git repository, it looks for `AGENTS.md` only in the folder it was started in.

Sign in to each tool with your work account, the way your company's instructions say. If sign-in works but the tool says it is not available or not enabled, an admin has to turn it on for your account. The vault is not the problem. The vault never holds an API key or a token.

## Set up without a terminal

Pick one. Each reads the rulebook on its own once it is opened on the vault folder.

1. **The Claude desktop app.** Download it from claude.ai/download (macOS 13 or later, Windows 10 or later; Linux in beta). The Code tab, next to Chat and Cowork, is Claude Code with a window: pick the vault folder, and keep Manual mode so Claude proposes each edit. Nothing else needs installing. The Code tab needs a Pro, Max, Ultra, Team, or Enterprise plan.
2. **VS Code with GitHub Copilot.** Install VS Code and the GitHub Copilot extension, sign in, and open the vault folder as the workspace. When VS Code asks whether you trust the folder, say yes: in Restricted mode the agents are off. In the Session Target control, pick the Copilot harness, which VS Code recommends; it finds `AGENTS.md` by itself.
3. **Codex in an editor or in the ChatGPT desktop app.** The Codex IDE extension runs in VS Code, Cursor, Windsurf, and VS Code Insiders. Open the vault folder and it reads `AGENTS.md` through the same configuration layers as the CLI. The ChatGPT desktop app on macOS and Windows includes Codex (there is no separate Codex app) and can open a local folder in its Work or Codex view. A workspace admin has to allow local access, and messages and task context may be stored in the cloud even when the work runs locally. Check your version.

If your company's software catalog carries a tool, install it from there. The catalog wins over every command below.

## Set up in a terminal

The one-line installers pipe a script from the internet into your shell. Check your company's software policy before you run one, as [Set up Obsidian](01-set-up-obsidian.md) said, and prefer the catalog or a package manager when you have one.

**Claude Code.**

```bash
brew install --cask claude-code                        # macOS with Homebrew; update with: brew upgrade claude-code
curl -fsSL https://claude.ai/install.sh | bash         # macOS, Linux, WSL; the native install updates itself
claude --version                                       # in a new terminal window
```

```powershell
winget install Anthropic.ClaudeCode                    # Windows; update with: winget upgrade Anthropic.ClaudeCode
irm https://claude.ai/install.ps1 | iex                # Windows PowerShell; the native install updates itself
```

On Windows, install Git for Windows as well, so the tool has a Bash shell; without it, it falls back to PowerShell. The terminal `claude` and the desktop app's Code tab are separate copies that update separately, but they share `CLAUDE.md` and your settings and can run on the same folder. Docs: [code.claude.com/docs/en/setup](https://code.claude.com/docs/en/setup).

**Codex CLI.**

```bash
brew install --cask codex                              # macOS with Homebrew
npm install -g @openai/codex                           # with npm
curl -fsSL https://chatgpt.com/codex/install.sh | sh   # standalone installer; the same command updates it
codex                                                  # start it in the vault folder
```

The Windows installer is on the docs page; check your version. Docs: [learn.chatgpt.com/docs/codex/cli](https://learn.chatgpt.com/docs/codex/cli).

**GitHub Copilot CLI.** Needs a Copilot subscription.

```bash
npm install -g @github/copilot                         # Node.js 22 or later; or: brew install --cask copilot-cli
```

```powershell
winget install GitHub.Copilot                          # Windows, needs PowerShell 6 or later
```

On first start it asks you to trust the folder. Docs: [docs.github.com, install Copilot CLI](https://docs.github.com/en/copilot/how-tos/set-up/install-copilot-cli).

## Which file each tool reads

| Tool | Reads on its own at start | What that means for the vault |
| --- | --- | --- |
| Claude Code, terminal and Code tab | `CLAUDE.md` in the working folder and in every folder above it, plus `~/.claude/CLAUDE.md` for your personal rules. It reads `AGENTS.md` by itself only when there is no `CLAUDE.md` (version 2.1.277 or later). | `CLAUDE.md` is a pointer: one sentence plus the lines `@AGENTS.md`, `@Me.md`, `@Home.md`, and `@System/AI/AI-Memory.md`. The `@` lines load those files at the start of every session. `/context all` inside a session lists what loaded. |
| Codex, CLI, IDE extension, and desktop app | `~/.codex/AGENTS.md`, then `AGENTS.md` from the project root down to the working folder, each file up to 32 KiB. When the folder is not a git repository, it checks only the folder it was started in. | The rulebook is read as is, so start Codex on the vault root. The build keeps the rulebook under 200 lines, which leaves room. |
| GitHub Copilot CLI | `AGENTS.md`, `CLAUDE.md`, and `.github/copilot-instructions.md`, combined with no precedence order. | It follows the pointer's `@` lines too, so the rulebook can load twice. Harmless; keep `AGENTS.md` short. |
| Copilot in VS Code | `AGENTS.md` at the workspace root. The Copilot harness finds it on its own; the Local harness attaches it through the setting `chat.useAgentsMdFile`, on by default. `.github/copilot-instructions.md` is read as well. | Open the vault folder as the workspace and the rulebook rides along with every request. An `AGENTS.md` outside the workspace root is off by default. |

So the vault needs exactly two rule files, and the build prompt writes both: `AGENTS.md` with every rule, under 200 lines and 32 KiB, and `CLAUDE.md` with none. Keep it that way. GitHub asks you to avoid instruction files that contradict each other, because most clients combine every file they find.

## Working on a repository with the vault as context

A developer's day runs in a repository, and a tool started there never sees the rulebook or the hubs. Two routes bring the vault in.

**Route A, start in the vault and add the repository.** The rules load because the session starts on the vault root, and the added folder becomes writable too:

```bash
cd ~/Documents/Vaults/Work
claude --add-dir ~/code/checkout-api    # the repository the hub records
```

The tool's permission prompts still apply in the added folder. Codex takes `codex --add-dir <path>` the same way, and Copilot CLI takes `--add-dir=<path>` on start or `/add-dir <path>` inside a session.

**Route B, start in the repository and point at the vault.** The build prints an optional one-line pointer for `~/.claude/CLAUDE.md` or `~/.codex/AGENTS.md`: "My work vault is at [path]; before writing there, read its AGENTS.md and follow it". Claude Code reads `~/.claude/CLAUDE.md` in every session and Codex reads `~/.codex/AGENTS.md` first, so the pointer travels into every repository session. Check it with "Tell me the reading order". Copilot CLI reads `~/.copilot/copilot-instructions.md` on its own, so the same pointer line goes there; until you add it, open the session with "Read [vault path]/AGENTS.md and the hub for this project first". If the tool says it cannot write in the vault from the repository, add the vault with `claude --add-dir <vault path>`, or switch to route A.

In both routes the repository's own `AGENTS.md` or `CLAUDE.md` governs the code, and the vault's rulebook governs anything written in the vault. "Start on [project]", "Where did we leave off on [repo]?", and "Close the session" then run `git` and `gh` in the repositories the hub names. See [Working day to day](04-working-day-to-day.md) and [the developer page](../roles/developer.md).

In VS Code, keep the repository as the workspace and add `Me.md` and the hub of the project to the chat as context when you need them; the Codex IDE extension brings open files and selections into the prompt. Copilot reads the repository's `AGENTS.md` from the workspace root, and an `AGENTS.md` outside the root is off by default.

A product owner who never codes uses route A with a read-only clone: `claude --add-dir ~/code/checkout-api`, `codex --add-dir ~/code/checkout-api` (write access to the clone is what delivery needs), or `copilot --add-dir=~/code/checkout-api`; in the Code tab, add the clone with + next to the prompt box and Add folder (in a terminal session, `/add-dir ~/code/checkout-api`); in VS Code, Add Folder to Workspace (check your version). The spec pull request, and the Specs-block pull request when the team asks for it, are the only writes there. See [the product owner page](../roles/product-owner.md).

## Permission modes: keep the defaults

The rulebook tells the tool to ask before changing anything that exists, except its own bookkeeping notes. The tool's own permission mode is the second layer, so keep it on:

- Claude Code: the default mode asks before edits and commands. In the desktop app that mode is called Manual; the others are Accept edits, Plan, and Auto. Do not use the flag that skips permissions on the vault.
- Codex: the default preset, Auto, lets it edit files inside the working folder without asking and asks only to go beyond it. In the vault, the rulebook is what makes it show changes first. If you want the tool itself to ask for every write, start it with `codex --sandbox read-only`. `/permissions` shows the current setting inside a session; newer versions call these permission profiles. Never use the flag that bypasses approvals and the sandbox.
- Copilot CLI: approve each command as it asks. Trust only the vault folder.
- Copilot in VS Code: edits land as pending changes that you keep or undo. Under the default Manual permissions, a terminal command that is not auto-approved asks first, and Allow Once is the default answer; the default deny list already covers `rm`, `del`, `curl`, and the like. Leave global auto-approval off, which is the default. Copilot CLI does not inherit these settings.

## Build the vault

With the tool open on the empty vault, open [the build prompt](../prompts/build-work-vault.md), fill in the profile, and paste everything below its line as your first message. Read the design it proposes, answer its questions or take the defaults, and say yes. It builds about twenty-five files, verifies them, and prints the Obsidian settings to set, which [Set up Obsidian](01-set-up-obsidian.md) lists. In a mode that asks before each write, expect one approval per file.

## After the build: check the setup

1. Restart the tool. Instruction files are read at the start of a session, so a tool that was open during the build has not read the new rulebook. The same applies after any later change to the rule files.
2. Say: "Read AGENTS.md and tell me the reading order, then summarize Home.md." If the tool can do that, it is set up. In Claude Code, `/context all` shows which files loaded.
3. Use one tool at a time on the same vault. Every tool updates the shared memory and log notes, so what one learned the next one sees.

## Working across tools

- The memory note `System/AI/AI-Memory.md` holds open questions, proposals waiting for your yes, and decisions. Every tool reads it at the start and updates it at the end, so you do not repeat yourself.
- The change log `System/AI/AI-Log.md` lists every change any tool made, one line each, never edited.
- If a tool ignores the rules, edits without asking, or renames, stop it and say "Read AGENTS.md again". If it keeps happening, check that you opened it on the vault root and not on a subfolder.

## Tools that cannot open the folder

Claude chat, ChatGPT, and Microsoft 365 Copilot cannot open a folder on your computer. The vault still serves them, in three ways.

**The context pack.** Say "Context pack for [hub]" to a tool that can read the vault. It prints one block to paste as the first message in Claude chat or ChatGPT: the How I work with AI section of `Me.md` and the one thing you are tired of re-explaining, Current focus from `Home.md`, the hub, the last three log entries, each linked repo hub's Run and test, Conventions, Gotchas, and Architecture, and the Live views run now, with today's date. A pack is never saved in the vault and never includes one-on-one logs unless you ask. Whatever comes back, you paste to the vault tool with "from [tool], [date]" as its source. The request is spelled out in [the context pack prompt](../prompts/context-pack.md).

**Claude chat: one Claude Project per role.** Projects exist on every plan. Project instructions apply to every chat in the project, and chats in a project do not see each other, so anything Claude should always know goes into the instructions or the project knowledge. Put the How I work with AI part of `Me.md` in the instructions, upload the hub once as knowledge, and upload it again when its Current state changes. Markdown is not on the official upload list, so test one `.md` upload; if the picker refuses it, paste the text or save a copy as `.txt`. If the vault lives in a GitHub repository, the GitHub integration adds chosen files and folders from one branch to a private Project's knowledge and refreshes them with Sync now. A private repository needs the Claude GitHub App, and on Team or Enterprise an owner turns the connector on first.

**ChatGPT: one ChatGPT Project per role.** The same caveat: Markdown is not on the upload table, which names DOCX, PDF, and TXT for text, so paste the note text as a project source or save a `.txt` copy. The number of files per project depends on the plan, ten at a time. Put the standing rules in the project instructions, which override your custom instructions, and set the project to project-only memory. If the vault lives in a GitHub repository, the GitHub app in ChatGPT reads it on demand, read-only. The new ChatGPT desktop app can open a local folder in its Work or Codex view, as above, and Work with Apps on macOS reads editors and terminals but not Obsidian. Check your version for both. A project there can attach several folders (Edit project, Add folder); only the primary folder gets Git operations and `AGENTS.md` discovery, so the vault is the primary folder and a repository clone is attached to it. The admin setting is "Allow members to use Codex locally" (the labels differ by plan, workspace, and rollout; check your version).

**Microsoft 365 Copilot: where reports go.** It does not read folders on your PC, only uploaded or cloud-hosted files, and it never reads the rulebook. Its place is downstream. Paste the paste-ready copy of a status report or roll-up into Outlook, Teams, Word, or Loop and let Copilot fit the house format; nothing comes back into the vault except what you write there. If the vault folder sits inside your OneDrive sync folder, Copilot Chat can attach a single file or an entire folder to a prompt, through the plus icon and Attach cloud files or by typing "/" and the note's name, and Markdown is on its supported-format list. Do not rely on it finding vault notes by itself: Markdown is not on its index list, so attach the folder or the files. Uploading a local file saves a copy to OneDrive. Whether the vault should be cloud-hosted at all is a decision to make on purpose; see [Keep it safe](05-keep-it-safe.md). A meeting recap from Copilot comes back into the vault as three to five sourced lines, never as a transcript, and calendar or email text is never pasted in.

**GitHub Copilot Chat on github.com.** If the vault lives in a GitHub repository, Copilot Chat on github.com can read it there. Open the chat with "Read AGENTS.md first"; which instruction file each GitHub client loads on its own differs, so check your version. The Copilot cloud agent, formerly the Copilot coding agent, and in GitHub's newer GitHub.com experience called Copilot in the cloud, picks up an issue assigned to Copilot and always opens a pull request; it reads `AGENTS.md`, a root `CLAUDE.md`, and `.github/copilot-instructions.md` on its own, receives the issue's title, description, and existing comments at assignment, and is not documented to follow links, so an issue names a spec by its repository path.

Next: [Connect your work trackers](03-connect-work-trackers.md).
