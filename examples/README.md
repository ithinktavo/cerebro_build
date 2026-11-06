# Example: what the build prompt produces

This folder holds a vault that the build prompt built for a placeholder persona, Alex Example. Alex is both a developer and an engineering manager, with two repositories, two teams, two projects, and a weekly status to write, so every module is on: Developer, Teams, and Reports. Open `sample-vault/` in Obsidian with "Open folder as vault" to browse it, or start with its `AGENTS.md`.

`design-pass.md` opens with the profile Alex filled in and then shows the design the AI proposed before building anything: the modules, the mapping table, the tree, the rituals in Alex's names, and four questions with their defaults. Alex replied "yes", and `sample-vault/` is the result. `after-one-week.md` shows what the same vault looks like after a week of use: a filed daily note, the filing table, a status report with its paste-ready copy, the roll-up, the weekly review, and a decision note, all illustration with placeholder data.

## What to look at

For everyone:

- `sample-vault/AGENTS.md`: the rulebook the prompt writes, with the reading order, the vault map, naming, properties, the two daily rituals, and the working rules.
- `sample-vault/CLAUDE.md`: the one-sentence pointer with four `@` lines that loads the rulebook into Claude Code.
- `sample-vault/Me.md`: the profile, line for line, in Alex's words.
- `sample-vault/Home.md`: the front door: current focus, what to say, one line per hub, trackers and tools, library.
- `sample-vault/Daily/2026-11-05.md`: the first daily note, created by "Start my day, vault only", with `AI:` lines under Plan and a source on each.
- `after-one-week.md`: the payoff, one week in: the filed daily note, the filing table, the ten-line "Where did we leave off" answer, the status report, the roll-up, the weekly review, and a decision note.
- `sample-vault/Library/2026-11-05 How to Use This Vault.md`: what to say and where things go.
- `sample-vault/Library/2026-11-05 Vault Design.md`: modules on and off with reasons, the mapping table, alternatives not chosen, what to revisit after a month.
- `sample-vault/Library/2026-11-05 Tracker Commands.md`: the gh and acli commands, read and write, with the sign-in step each needs.
- `sample-vault/System/Templates/`: the 14 templates, one per kind of note, from Daily Note to Monthly Review.
- `sample-vault/System/AI/AI-Memory.md`: the open questions and the decisions the build left behind.
- `sample-vault/System/AI/AI-Log.md`: one line per change the AI made.

If you write code:

- `sample-vault/Repos/checkout-api/checkout-api.md`: a repo hub with marked blanks for everything that needs git or gh, and a Live views section with the exact commands.
- `sample-vault/Repos/web-storefront/web-storefront.md`: the same for the second repository.
- `sample-vault/Projects/Checkout Migration/Checkout Migration.md`: a project hub; its Repos and deploy order section holds the one fact Alex is tired of re-explaining.
- `sample-vault/Projects/Checkout Migration/2026-11-05 Checkout Migration Log.md`: a running log with the one entry shape.
- `sample-vault/System/Templates/Design Template.md`: the design note that comes before non-trivial code.

If you track teams:

- `sample-vault/Teams/Team Alpha/Team Alpha.md`: a team hub with cadence, tracker, and the three named queries, on GitHub Projects.
- `sample-vault/Teams/Team Beta/Team Beta.md`: the same team hub, on Jira.
- `sample-vault/Teams/Team Alpha/2026-11-05 Team Alpha Log.md`: a check-in log, where "Log this check-in for Team Alpha" lands.
- `sample-vault/Projects/Observability Rollout/Observability Rollout.md`: a standing responsibility as a project whose Goal says ongoing.
- `sample-vault/Reports/Reports.md`: the recipes for the Friday status, the weekly roll-up, and the monthly review, with an empty Open asks list.
- `sample-vault/System/Templates/Status Report Template.md`: the five headings every status report uses.
- `sample-vault/System/Templates/Roll-Up Template.md`: the roll-up grouped the way leadership reads.

If you write stories:

- `product-owner-design-pass.md`: the profile Jordan Example filled in as a product owner, and the design the AI printed from it: the Specs switch on with no new folder, two read-only repositories, one question with its default.
- `story-spec.md`: one story from "Spec for ALPHA-123" to merged code: the spec note in full, the review table, the delivery as one set of commands, the developer's ten-line plan, the revision, the pull request body with its Acceptance criteria section, and the week's close.

## What was tested

The sample was built on 2026-11-05 by Claude acting as the coding tool, with no tracker, git, or gh access, and verified by the script the prompt asks for. Two more personas, a Windows developer in Build now mode and a director with one-on-one logs and Azure DevOps in Design first mode, were built the same way the same day, and each verified clean. The prompt has not yet been run with Codex or GitHub Copilot, and no vault built by it has been opened in Obsidian. The Obsidian settings and the tool facts come from the vendors' documentation, checked on 2026-11-04 and 2026-11-05. No product-owner vault has been built yet; the spec, the commands, and the pull request body in `story-spec.md` are illustration.

## What this example is not

- Every value is placeholder text. No real team, repository, or tracker was read. Everything that needs a tool is a marked blank such as `_left blank, needs gh_`.
- The trackers shown are GitHub Projects and Jira. With Azure DevOps only the tracker lines differ: the hub's Tracker section and the commands note.
- The `AGENTS.md` and `CLAUDE.md` inside `sample-vault/` belong to the sample and apply only in that folder.
- The `.gitkeep` files in `Notes/` and `System/Attachments/` only keep those empty folders in git. Obsidian ignores them.

Do not copy this folder as your own vault. Run the prompt on an empty vault instead, so that the build fits your roles, your tools, and your trackers, and so that the dates and names are yours.

Next: [the build prompt](../prompts/build-work-vault.md).
