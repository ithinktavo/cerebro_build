# 2. Connect your AI tools

The vault works with any AI coding tool that can open a folder, read files, and run commands. Each tool reads a rule file when it starts in the vault folder, so the rules travel with the vault and not with the tool. Claude Code, Codex, and GitHub Copilot are covered here. Another tool works the same way if it reads `AGENTS.md`.

## The one rule that matters

Open the tool with the vault folder as its working folder. From a terminal:

```bash
cd ~/Documents/Vaults/Work
claude        # or: codex   or: copilot
```

In the Claude desktop app, open the Code tab on the vault folder. In VS Code, open the vault folder as the workspace. A tool opened one level up or one level down does not find the rules.

## Install and sign in

Sign in to each tool with your work account, the way your company's instructions say. The vault never holds an API key or a token. All three tools run natively on Windows as well as on macOS and Linux.

**Claude Code.** The Claude desktop app includes it as the Code tab. For the terminal:

```bash
curl -fsSL https://claude.ai/install.sh | bash        # macOS, Linux, WSL
```

```powershell
irm https://claude.ai/install.ps1 | iex                # Windows PowerShell
```

Also available as `brew install --cask claude-code`, `winget install Anthropic.ClaudeCode`, or `npm install -g @anthropic-ai/claude-code` with Node.js 22 or later. On Windows, install Git for Windows as well, so the tool has a Bash shell; without it, it falls back to PowerShell. Docs: [code.claude.com/docs/en/setup](https://code.claude.com/docs/en/setup).

**Codex CLI.**

```bash
npm install -g @openai/codex                           # or: brew install --cask codex
```

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"   # Windows
```

On Windows it runs natively with its own sandbox; WSL works too. Docs: [learn.chatgpt.com/docs/codex/cli](https://learn.chatgpt.com/docs/codex/cli).

**GitHub Copilot CLI.** Needs a Copilot subscription.

```bash
npm install -g @github/copilot                         # Node.js 22 or later; or: brew install --cask copilot-cli
```

```powershell
winget install GitHub.Copilot                          # Windows, needs PowerShell 6 or later
```

On first start it asks you to trust the folder; `/login` signs you in. Docs: [docs.github.com, install Copilot CLI](https://docs.github.com/en/copilot/how-tos/set-up/install-copilot-cli).

**GitHub Copilot in VS Code.** Install the GitHub Copilot extension and open the vault folder as the workspace.

## Which file each tool reads

| Tool | Reads on its own at start | What that means for the vault |
| --- | --- | --- |
| Claude Code | `CLAUDE.md` in the working folder and in every folder above it. It reads `AGENTS.md` by itself only when there is no `CLAUDE.md` (version 2.1.277 or later). | `CLAUDE.md` is a pointer: one sentence plus the lines `@AGENTS.md`, `@Me.md`, `@Home.md`, and `@System/AI/AI-Memory.md`. The `@` lines load those files at the start of every session. |
| Codex CLI | `~/.codex/AGENTS.md` for your personal defaults, then `AGENTS.md` from the project root down to the working folder, up to 32 KiB in all. | The rulebook is read as is. The build keeps it under 200 lines, which leaves room. |
| GitHub Copilot CLI | `AGENTS.md`, `CLAUDE.md`, and `.github/copilot-instructions.md`. | It reads both the rulebook and the pointer. No conflict, because the pointer holds no rules. |
| Copilot in VS Code | `AGENTS.md` at the workspace root (setting `chat.useAgentsMdFile`, on by default) and `.github/copilot-instructions.md` (on by default). | Open the vault folder as the workspace and the rulebook rides along with every chat request. |

So the vault needs exactly two rule files, and the build prompt writes both: `AGENTS.md` with every rule, and `CLAUDE.md` with none.

## Permission modes: keep the defaults

The rulebook tells the tool to ask before changing anything that exists. The tool's own permission mode is the second layer, so keep it on:

- Claude Code: the default mode asks before edits and commands. Do not use the flag that skips permissions on the vault.
- Codex: the default preset, Auto, lets it edit files inside the working folder without asking and asks only to go beyond it. In the vault, the rulebook is what makes it show changes first. If you want the tool itself to ask for every write, start it with `codex --sandbox read-only`. `/permissions` shows the current setting inside a session; newer versions call these permission profiles. Never use the flag that bypasses approvals and the sandbox.
- Copilot CLI: approve each command as it asks. Trust only the vault folder.

## After the build: check the setup

1. Restart the tool. Instruction files are read at the start of a session, so a tool that was open during the build has not read the new rulebook. The same applies after any later change to the rule files.
2. Say: "Read AGENTS.md and tell me the reading order, then summarize Home.md." If the tool can do that, it is set up.
3. Use one tool at a time on the same vault. Every tool updates the shared memory and log notes, so what one learned the next one sees.

## Working across tools

- The memory note `System/AI/AI-Memory.md` holds open questions, proposals waiting for your yes, and decisions. Every tool reads it at the start and updates it at the end, so you do not repeat yourself.
- The change log `System/AI/AI-Log.md` lists every change any tool made, one line each, never edited.
- If a tool ignores the rules, edits without asking, or renames, stop it and say "Read AGENTS.md again". If it keeps happening, check that you opened it on the vault root and not on a subfolder.

## Chat apps without file access

Claude chat, ChatGPT, and Copilot chat in the browser cannot read the folder. Paste `Me.md` and the hub of the project in question at the start of the conversation, or ask a tool that can read the vault to print a context pack for you to copy.

Next: [Connect your work tracker](03-connect-work-trackers.md).
