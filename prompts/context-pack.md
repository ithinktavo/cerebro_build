# Context pack

Claude chat, ChatGPT, and Microsoft 365 Copilot cannot open the vault folder. A context pack is how the vault reaches the first two: one block, printed by a tool that can read the folder, that you paste as the first message of a chat. Nothing is saved, and the pack carries today's date so that its age is never in doubt.

## What to say

"Context pack for Team Alpha." For a repository: "Context pack for checkout-api." For a project: "Context pack for [project]." For a story: "Context pack for ALPHA-123."

Say it to the tool opened on your vault: Claude Code, Codex, or GitHub Copilot. In the Claude desktop app, the Code tab reads the folder and the Chat tab is a chat tool, so a pack goes from one to the other.

## What happens

1. The block. In one piece, dated today: the How I work with AI section of `Me.md` and the one thing you are tired of re-explaining; Current focus from `Home.md`; the hub; the last three entries of its running log; for each repository the hub links, its Run and test, Conventions, Gotchas, and Architecture from `Repos/checkout-api/checkout-api.md`; and the Live views run now, which are the gh commands the repo hub records for your open pull requests, the ones awaiting your review, and failing checks. Live views are read at pack time and never stored in the vault, which is why the pack carries its date. For a story, the pack is the project's pack plus the spec body, from the repository file when delivered and from the note before that, and the story's key, title, and state.

2. What it leaves out. A pack is never saved in the vault. It never includes one-on-one logs unless you ask. A hub holds other people by name and role only, so the pack does too.

3. The paste. The pack is the first message in Claude chat or ChatGPT; your question is the second. For standing context, a Claude Project or a ChatGPT Project holds `Me.md` and the hubs you use most, with the How I work part in the project instructions, and you refresh the files when the hubs change. To know which, ask the folder tool "Which hubs changed since [date]?"; it answers from `System/AI/AI-Log.md`, which holds one line per change. Markdown files are not on either tool's published upload list: test one upload first, and if the picker refuses it, paste the note's text or save a copy as `.txt`. [Connect your AI tools](../docs/02-connect-ai-tools.md) has what is confirmed for each tool.

4. What comes back. Paste the answer to the folder tool with its source: "from Claude chat, 2026-11-05: [paste]. Add to today." or "from ChatGPT, 2026-11-05: [paste]. Log this check-in for Team Alpha." Every fact in the vault carries its source, and that line is it.

5. Microsoft 365 Copilot. It is where reports go (Outlook, Teams, Word, Loop), not a reader of the vault. The one thing that comes back from it is a meeting recap, pasted as three to five sourced lines, never as a transcript. Calendar and email text are never pasted in.

A pack is work content leaving the folder. Paste it only into a chat tool your company has approved, signed in with your work account. See [Keep it safe](../docs/05-keep-it-safe.md).

## If your vault predates this ritual

A vault built with an older rulebook has hubs and logs but no Live views and no pack rule. Paste this to the tool opened on the folder.

---

Print a context pack for [hub] as one block I can paste into [Claude chat or ChatGPT]. Put today's date at the top. Include: the How I work with AI section of `Me.md` and the one thing I am tired of re-explaining; the Current focus from `Home.md`; the hub note in full; the last three entries of its log; for each repository the hub links, its Run and test, Conventions, Gotchas, and Architecture sections; and, if the hub lists gh commands for open pull requests, reviews, or checks, run them now and include the results with the date. If [hub] is a story key, print the project's pack plus the spec body, from the repository file when delivered and from the note before that, and the story's key, title, and state. Leave out one-on-one notes and anything about other people beyond names and roles. Do not save the pack in the vault. When I paste the answer back, record its source as "from [tool], [date]".

Next: [Example vault](../examples/README.md)
