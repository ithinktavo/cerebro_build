# Meeting notes

Turns your notes, a transcript, or a Teams recap into a filed meeting note: decisions with their own notes where they deserve one, actions with owners and dates, the source on the note, and the actions offered to the tracker. For anyone who sits in meetings that decide things.

## What to say

"Turn these notes into a meeting note for Team Alpha: [paste]."

Name the hub the meeting belongs to: a team, a project, or a repository. For a meeting with no hub, such as an all-hands or a cross-team review, leave the hub out: "Turn these notes into a meeting note: [paste]." It goes to `Notes/`.

## What happens

1. The draft. A dated `type: meeting` note with Attendees (names and roles only), Context in two lines, Discussion as short bullets in your words, Decisions, each linking its decision note, Actions as checkboxes with an owner and a date, and Source with its date: your notes, a transcript, or a Teams recap. A recap from Microsoft 365 Copilot is pasted as its summary lines, not as a transcript, and never with calendar or email text.

2. The preview. It shows the note in chat before saving. After your yes it saves the note in the hub's folder, for example `Teams/Team Alpha/YYYY-MM-DD Team Alpha Planning.md`, and lists it in the hub. With no hub, the note goes to `Notes/` and is listed nowhere else.

3. The decisions. It lists the decisions and proposes which deserve their own dated `type: decision` note: Context, Decision, Alternatives, Consequences, Decided by and when, Status (proposed, decided, reversed). It writes those after your yes, linked from the meeting note and from the hub. A decision that belongs in a repository goes there through a pull request, and the hub links it by URL.

4. The actions. It adds them to the hub's Next steps, with owner and date, or Waiting on, with who, what, and since when, and reports the change; those two fields are AI-maintained. An action that belongs in Jira, Azure DevOps, or GitHub Projects is offered with the create command shown. It runs the command only on your yes and links the item by URL from the action. The commands per tracker are in your `Library/YYYY-MM-DD Tracker Commands.md` note.

5. What stays out. It flags personal matters, credentials, and customer data in what you pasted and leaves them out. Other people appear by name and role only.

6. A 1:1. Say so and name the person. With one-on-one logs off, the default, the note is named after the person and keeps work topics only: priorities, blockers, asks, follow-ups. With them on, the entry goes to that person's running log instead, and "Prepare my 1:1 with Alex Example" reads it before the next one. Only the team's work from a 1:1 belongs in the check-in log; see [Team check-in](team-check-in.md).

## If your vault predates this ritual

A vault built with an older rulebook files meeting notes but records no source and offers no tracker items. Paste this with the brackets filled.

---

Turn these raw notes into a meeting note for [project or team, or no hub]: [paste].

1. Write a dated `type: meeting` note with: Attendees (names and roles only), Context in two lines, Discussion as short bullets in my words, Decisions, Actions as checkboxes with an owner and a date, and Source. Record what I pasted as the source with today's date: my notes, a transcript, or a Teams recap. If the meeting has no project or team, file it in `Notes/`.
2. List the decisions and propose which deserve their own dated `type: decision` note (Context, Decision, Alternatives, Consequences, Decided by and when, Status). Write those after my yes, linked from the meeting note and from the hub.
3. Add the actions to the hub's Next steps or Waiting on. Show me the hub change and wait for my yes. If an action belongs in [Jira, Azure DevOps, or GitHub Projects], show me the create command, run it only on my yes, and link the item by URL from the action.
4. Flag anything that should not be in the vault (personal matters, credentials, customer data) and leave it out.
5. For a 1:1, name the note after the person and keep work topics only: priorities, blockers, asks, follow-ups.
6. Show me the meeting note in chat before you save it.

Next: [Close the week](close-the-week.md)
