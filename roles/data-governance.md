# Playbook: data governance and other tracking-heavy roles

Governance work is tracking: initiatives across teams, policies and standards, decisions with their reasons, stakeholders, and a weekly account of where everything stands. Most of it already lives in Azure DevOps or Jira. The vault adds the context the tracker lacks (why, who decided, who is waiting on whom) and turns both into status reports.

## Keep these blocks in the build prompt

Teams. Projects are always built. Drop Code, Blueprints, and Terraform unless you use them. Name Azure DevOps and `az boards`, or Jira and its command-line tool, as your tracker.

## What you get

- `Projects/<Initiative>/`: one hub per governance initiative, such as a catalog rollout, a retention policy, or a quality program. Goal, current state, decisions, next steps with owners, open questions, waiting on.
- `Teams/<Team>/`: one hub per team you coordinate or oversee, with its check-in log, priorities, and risks.
- Decision records: dated `type: decision` notes with Context, Decision, Alternatives, and Consequences. These are the vault's most valuable notes. Six months later someone asks why, and the answer is there.
- `Library/`: standards, definitions, a glossary, and links to the official policy documents. Link to the source of record; do not copy it.
- Weekly `type: report` notes per team or initiative.

## Azure DevOps from the command line

The AI reads Azure DevOps through the `az boards` commands. Setup is in [Connect your work tracker](../docs/03-connect-work-trackers.md). What makes it useful for governance:

- Two shared queries per team or initiative in Azure DevOps, one for what changed in the last 7 days and one for everything open, such as "Governance, Team Alpha, changed in the last 7 days" and "Retention policy, all open". The AI runs them by id and never has to invent a query.
- Area paths or tags that mark governance items, so one query spans teams.
- The AI copies only the key, title, state, owner, and dates into notes and links everything else by URL.

Requests that work well:

- "Run the Alpha shared query and tell me what closed, what moved, and what is stuck."
- "Which open items across the governance queries have had no change in 14 days?"
- "Create a task in Azure DevOps for [thing]. Show me the command first."

Jira works the same way through its command-line tool, with JQL and saved filters.

## The weekly status report

Same as the manager playbook: "Status report for [initiative or team] for this week." Five headings, a source on every line, saved as a dated note, edited by you. For leadership: "Roll up this week's governance reports into one page: progress, risks, decisions needed." The roll-up is saved as a dated report in `Notes/`. The prompt is in [prompts/weekly-status-report.md](../prompts/weekly-status-report.md).

## Meetings and stakeholders

Paste raw meeting notes. The AI writes a `type: meeting` note with attendees, discussion, decisions, and actions with owners and dates, and files it in the initiative folder. Each decision gets its own decision note. Actions land in the hub's Next steps or Waiting on. The prompt is in [prompts/meeting-notes.md](../prompts/meeting-notes.md).

## What stays out

Governance works on data about data. The vault holds classifications, policies, owners, and decisions. It never holds samples of the data itself, customer records, or anything a classification rule keeps out of general systems. See [Keep it safe](../docs/05-keep-it-safe.md).

## Requests to try

1. "Add an initiative: [name]. Goal: [one line]. Azure DevOps query: [id or URL]. Stakeholders: [names and roles]."
2. "Add a team: [name]. Members: [names and roles]. Query: [id]."
3. "Status report for [initiative] for this week from Azure DevOps."
4. "Write a decision note: we decided [X] because [Y]. The alternatives were [Z]."
5. "What is waiting on me, and what has not moved in two weeks?"
