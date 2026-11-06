This is the design the AI proposed for the sample persona Jordan Example, a product owner, before building anything, printed in chat as the first reply to the build prompt.
No vault has been built from it yet. The week after the yes, one story from "Spec for ALPHA-123" to merged code, is in `story-spec.md`, and every value in both files is placeholder text.

## The profile Jordan filled in

- Name or handle: Jordan Example. Roles: product owner.
- Teams: none. Projects: Checkout Migration, goal: move checkout to the new service by the end of the quarter; Team Alpha builds it; repos checkout-api and web-storefront. Repositories: /Users/jordan/code/checkout-api at https://github.com/example-org/checkout-api, read only; /Users/jordan/code/web-storefront at https://github.com/example-org/web-storefront, read only.
- I report to the head of product. Reporting to me: none.
- AI tools that read this folder: Claude Code, GitHub Copilot in VS Code. Chat tools I also use: ChatGPT, Microsoft 365 Copilot.
- Trackers: Checkout Migration uses Jira (example.atlassian.net, project ALPHA; acli). Signed in from the terminal: gh and acli.
- Reports I owe: none.
- My week: refinement on Tuesdays, planning every other Thursday.
- Note habits: I keep a daily note; to-dos in the vault; nothing else to preserve.
- 1:1 notes in the vault: no.
- Specs for my stories: yes. checkout-api keeps specs in: none yet. Reviewer: Alex Example, tech lead. Access: left blank.
- The one thing I am tired of re-explaining: which validation rules the old checkout already enforces.
- Operating system: macOS. Mode: Design first.
- How I work with AI: as written in the prompt.

Every marked blank in the design below is something this block leaves open.

# Design for Jordan Example's work vault

## 1. Modules

- Developer: on. You named two repositories, both read only. Nothing is read from them until you ask.
- Teams: off. Team Alpha appears only as the team that builds Checkout Migration. Say "Add a team" if you want its check-in log.
- Reports: off. You owe none.
- Specs: on, as a switch, no folder. Specs for my stories says yes: the Spec template, a Specs section in the Checkout Migration hub and in both repo hubs, the four spec phrases, and two morning lines.

## 2. Mapping table

| Item | Module | Links |
| --- | --- | --- |
| Checkout Migration | Project | record: Jira project ALPHA at example.atlassian.net through acli; built by Team Alpha; repos checkout-api and web-storefront; specs folder: a marked blank until gh reads the repositories |
| checkout-api | Repo, read only | /Users/jordan/code/checkout-api; https://github.com/example-org/checkout-api; serves Checkout Migration; access `_left blank, needs gh_` |
| web-storefront | Repo, read only | /Users/jordan/code/web-storefront; https://github.com/example-org/web-storefront; serves Checkout Migration; access `_left blank, needs gh_` |

## 3. Tree

- `AGENTS.md`, `CLAUDE.md`, `Me.md`, `Home.md`: the rulebook, the Claude Code pointer, your profile, the front door.
- `Daily/`: one note per work day, created by "Start my day". Empty until then.
- `Notes/`: ideas, learning notes, weekly reviews, one-off meeting notes. Empty at the start.
- `Library/`: How to Use This Vault, Vault Design, Tracker Commands, all dated today.
- `Projects/Checkout Migration/`: hub and running log. Your specs are notes in this folder, next to the log, one per story; no Specs folder. The validation-rules fact you are tired of re-explaining lives in this hub.
- `Repos/checkout-api/` and `Repos/web-storefront/`: one hub each, with a Specs section; no repo log. Nothing is read from the repositories until you ask.
- `System/Templates/`, `System/Attachments/`, `System/AI/`: 12 templates; files and exports; `AI-Memory.md` and `AI-Log.md`.
- No `Teams/` and no `Reports/`: no new folder comes from the switch.

## 4. Hubs, templates, and the daily note

- The project hub opens with Current state (dated) and ends with Notes in this folder. It keeps Goal, People (Alex Example as the reviewer, name and role only), Teams, Repos, Tracker and queries (with the next-up and spec-question queries as marked blanks), Specs (one line per story, newest first), Priorities, Milestones, Next steps, Waiting on, Risks, Open questions, Decisions, Log. Repo hubs keep Repository, Serves, Architecture stamped with the commit, Documents to read, Run and test, Conventions, Specs (the folder, the file rule, the key prefix, the PR template path, the test layout, whether the rulebook names specs, the reviewer, your access, who can read story comments, each stamped), Gotchas, Live views.
- Templates, 12: Daily Note, Note, Meeting, Decision, Design, Status Report, Weekly Review, Log, Project Hub, Slide Outline, Repo Hub, Spec. No Team Hub, Roll-Up, or Monthly Review, because Teams and Reports are off; no One-on-One Log, because 1:1 logs are off.
- Daily note: `## Plan` with checkboxes and `## Log` with one line per thing in your words, no properties. The morning pulls: carried-over Plan items; Next steps you own and Waiting on older than seven days in every hub; today's cadence (Tuesday refinement, planning every other Thursday); stale hubs; open questions. Then, through gh and acli: your open pull requests, spec pull requests among them with their age; items assigned to you; stories next up with no spec; developer questions on delivered stories.

## 5. Report recipes

- None, because Reports is off. A status report for Checkout Migration is still available on request, from the Status Report template.

## 6. Rituals, in your names

- Daily: "Start my day", "Start my day, vault only", "Add to today: [line]", "Close my day", "Catch me up".
- Specs: "Spec for ALPHA-[n]", "Review the spec for ALPHA-[n]", "Deliver the spec for ALPHA-[n]", "Revise the spec for ALPHA-[n]: [what changed]".
- Work: "Start on Checkout Migration", "Close the session".
- Setup and context: "Read my repos and fill in their hubs", "Record these queries in the Checkout Migration hub", "Context pack for ALPHA-[n]" for ChatGPT.
- Week: "Close the week" on Friday, with "What did I ship this week?" and the weekly review. Not available: "Log this check-in", the roll-up, and "Prepare my 1:1 with [name]", since Teams, Reports, and 1:1 logs are off.

## 7. Repository paths, first requests, assumptions

- Read only when you later ask: /Users/jordan/code/checkout-api and /Users/jordan/code/web-storefront.
- First five requests: "Start my day"; "Read my repos and fill in their hubs"; "Record these queries in the Checkout Migration hub", after you create the next-up and spec-question filters in Jira; "Spec for ALPHA-123"; "Close my day".
- Assumptions: the validation-rules fact lives in the Checkout Migration hub as a marked blank for you to fill in. The specs folder of each repository, the reviewer's GitHub handle, your access, the Jira filter names, the default branches, and the current commits are marked blanks. No tracker, git, or gh command runs during the build.

## 8. Questions, each with the default a bare yes takes

1. Is Team Alpha a team you track, with check-ins and a status, or only the team that builds your stories? Default: only builds, so no Teams module.

Reply yes to build with these defaults, or tell me what to change.
