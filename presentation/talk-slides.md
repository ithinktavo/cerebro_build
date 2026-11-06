# A work vault your AI tools can read

Obsidian, plus Claude Code, Codex, and GitHub Copilot, plus your tracker

---

## The problem

- Every AI session starts from zero
- Context is in heads, chats, documents, and the tracker
- Status reports get rebuilt from memory every week
- What you capture during the day lands in five places and gets filed in none

---

## The idea

One folder of plain Markdown notes

- Your notebook, in Obsidian: one daily note, your ideas, what you learn
- The AI's context, read first in every session
- One rulebook every tool follows: `AGENTS.md`

---

## The build

1. Profile: your roles, what you own, your tools, your week
2. Design: the AI proposes the folders, hubs, and rituals for you, in your names
3. Yes: it asks up to five questions, you say yes
4. Build: about twenty-five files in one pass

---

## What is in it

```
AGENTS.md   the rulebook       CLAUDE.md  its pointer for Claude Code
Me.md       who you are        Home.md    what is current
Daily/      one note per day: Plan and Log
Notes/      your own notes: ideas, learning, reviews
Library/    reusable knowledge: how-tos, checklists, prompts
Projects/   one hub and one running log per project
System/     templates, attachments, the AI's memory and change log
```

Modules, only when your profile calls for them:

```
Repos/      Developer: one hub per repository
Teams/      Teams: one hub and a check-in log per team
Reports/    Reports: roll-ups and monthly reviews
```

---

## The daily loop

1. "Start my day": today's note, with what matters at the top, each line with its source
2. Type into Log during the day, one line per thing, in your words
3. "Close my day": a filing table, one row per line, one yes files the batch

---

## The weekly loop

"Close the week", on your reporting day

1. A status report per team: five headings, every line with its source, a paste-ready copy
2. "What did I ship this week?" if you own repositories
3. The roll-up for leadership
4. Your weekly review: what moved, what stalled, next week's three

---

## The tracker stays the system of record

- GitHub Projects, Jira, Azure DevOps, through their command-line tools
- Three named queries per team feed the status report
- Reads freely, shows every write first
- Links, never copies

---

## Demo

Start my day, two Log lines, Close my day, then a status report for Team Alpha

---

## Who it is for

- Developers: repo hubs, project logs, "Where did we leave off?"
- Managers and PMs: team hubs, check-ins, weekly status reports
- Directors: roll-ups across teams, monthly reviews
- Product owners: a spec per story, delivered to the repository, read first by the developers' tools
- Most people are two of these: one vault, every module on

---

## The product owner

From a story to a spec the developers' tools read first

- "Spec for ALPHA-123": the story, your notes, and the code at a known commit, on one page
- Criteria AC1 and up, Given, When, Then, each with how it is verified; every AI proposal marked
- "Deliver the spec for ALPHA-123": a pull request into `specs/`, one comment on the story
- "Start on ALPHA-123": the developer's tool reads the spec first and proves each criterion in its PR
- No write access? The spec goes onto the story, and the first commit adds the file

---

## The chat tools

- Claude chat, ChatGPT, Microsoft 365 Copilot: paste the context pack
- "Context pack for [hub]" prints it as one block, pasted as the first message
- Microsoft 365 Copilot is where reports go, not a reader of the vault

---

## Safety

- Asks before changing your words, never deletes or renames
- Reads freely, shows every write first, never emails or posts to people
- No secrets, no customer data; names and roles only for other people
- Company-approved tools, work accounts, company backup

---

## Set up in 30 minutes

1. Install Obsidian, create an empty vault, turn on Daily notes and Templates
2. Open Claude Code, Codex, or GitHub Copilot on that folder
3. Fill in the profile and paste the build prompt
4. Read the design, say yes
5. Set the Obsidian settings it prints, sign in to your tracker's command-line tool

---

## Where to start

The repository: the build prompt, the docs, a page per role, the prompts, a sample vault

[repository URL]

Try it on one project or one team this week

Next: [Speaker notes and demo script](talk-notes.md).
