# Playbook: developers

You keep code in repositories and context in the vault. The vault tells the AI where the code is, what was decided and why, how to run things, and what happened last session, so a new session on a repository starts informed instead of from zero.

## Keep these blocks in the build prompt

Code and Blueprints. Teams as well if you lead one. Terraform only if you build infrastructure from a platform team's modules.

## What you get

- `Projects/<Name>/<Name>.md`: goal, current state as of a date, links to the repository blueprint and the tracker, next steps with owners, open questions, decisions.
- `Blueprints/<Repo>/<Repo>.md`: the repository described for reuse. Location, stack, how to run and test, architecture, patterns worth copying, key files, gotchas, and the commit it was read at.
- Dated session logs in the project folder: what changed, what is next, blockers, links to the commits and pull requests.
- Decision records with their alternatives, so the reasons survive the people.

## A coding session

1. Open the AI tool on the vault and name the project: "Project Alpha. Check the repository and the open pull requests, then tell me where we left off." The tool reads the hub, the last session log, `git status`, and the pull request list.
2. Work in the repository. The tool follows the blueprint and the hub for conventions, works on a branch, shows the diff and the commit message before committing, and shows the title and body before opening a pull request.
3. Close: "Write the session log and update the hub." The log links the commits and pull requests by URL; the hub's current state and next steps move forward.

## Teach the AI your repositories

"Make a blueprint of `/path/to/repo`." The tool reads the README, the structure, the build files, and the entry points, and writes the blueprint hub plus dated mirror notes for the small documents worth keeping close (architecture notes, decision records), each marked with its source path and commit.

The blueprint records the commit it was read at. Before relying on it, the tool checks the repository's current commit; if it moved, or the blueprint is older than 30 days, it re-reads the source first.

To start something new on a known pattern: "Scaffold a new service like the Billing blueprint, at `/path/new`, for [purpose]." The tool proposes the layout from the blueprint before writing a file.

## Trackers and repositories

`gh` for GitHub, `az repos` and `az boards` for Azure DevOps, the Jira command-line tool for Jira. Read commands run freely; write commands are shown first. Pull requests and issues are linked by URL from the session logs and the hub, never copied.

## Infrastructure, if you kept the block

1. "Catalog the modules in `/path/to/terraform-modules`." One blueprint hub for the module repository and one dated module card per module: inputs, outputs, example usage from the repository's examples, constraints, gotchas.
2. "Design the infrastructure for Project Alpha: [need]." The tool restates the need, reads the cards, and writes a design note as a plan: modules and versions, inputs, assumptions, open questions for the platform team, a code sketch. It waits for your yes.
3. The Terraform goes in the project's repository, with pinned module versions and no secrets. A decision note and a session log close the loop, and the module cards get updated with what was learned.

## Requests to try

1. "Add a project: [name]. Goal: [one line]. Repository: [path]. Tracker: [URL]."
2. "Make a blueprint of [path]."
3. "Where did we leave off on [project]?"
4. "Draft the pull request description from the diff on this branch."
5. "Write the session log and update the hub."
