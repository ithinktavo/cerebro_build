# Team check-in

For anyone who runs a standup, a sync, or a working group. After the meeting you give the tool your notes, a Teams recap, or someone's written update. It writes a dated entry in the team's check-in log with its true source, shows the hub edits for one yes, and offers tracker items for the lines that deserve one. A 1:1 is not a check-in; see the end of the section below.

## What to say

"Log this check-in for Team Alpha: [your lines]."

For example: "Log this check-in for Team Alpha: payments retry shipped to staging. Alex Example is waiting on the security review since Monday. We decided to move the cutover to the 20th."

The shorter route during the day: type the same lines under `## Log` in today's daily note, or say "Add to today: [line]", and let "Close my day" file them. A check-in line in the Log becomes the same dated entry, with the same hub edits, at the end of the day.

## What happens

1. The entry. The tool appends a dated entry to the team's running check-in log, `Teams/Team Alpha/YYYY-MM-DD Team Alpha Log.md`, where the date is the day the log was created and the newest entry sits at the bottom. The entry has the one shape every log in the vault uses: `## YYYY-MM-DD`, then What happened, Decided, Next, Waiting on, Links, Source. The words are yours, cleaned up, not rewritten. Running logs are AI-maintained, so it writes the entry and reports it rather than asking.

2. The source. What you said yourself is "said in chat" with the date. If you pasted a Teams recap, a transcript, or someone's written update, that is the source, with its date: "from the Teams recap, 2026-11-05" or "from Alex Example's update, 2026-11-05". A recap from Microsoft 365 Copilot goes in as three to five lines, never as a transcript, trimmed of anything about other people beyond names and roles. Calendar and email text are never pasted in.

3. The hub edits. It shows the edits the entry implies in `Teams/Team Alpha/Team Alpha.md` as before and after, for one yes: Current priorities if they changed, Waiting on as who, what, and since when, Risks with owner and date, and Decisions. Current state, Next steps, and Waiting on are otherwise AI-maintained; a check-in shows them anyway, the stricter choice, because the lines are your account of what the team said.

4. Tracker items. Where a line deserves a ticket, it says which and shows the create command. It runs the command only on your yes and links the item by URL from the entry. For GitHub Projects the command adds a draft item, or an existing issue or pull request, to the project:

   ```
   gh project item-create <number> --owner YOURORG --title "Retry on timeout" --body "From the check-in of 2026-11-05"   # a draft item
   gh project item-add <number> --owner YOURORG --url https://github.com/example-org/checkout-api/issues/23           # an existing issue or pull request
   ```

   For Jira and Azure DevOps the create command comes from your `Library/YYYY-MM-DD Tracker Commands.md` note.

5. Your promises. It lists what you promised and to whom. Say yes to put them under Next steps in the hub with the date, or leave them in today's Log and let "Close my day" file them.

6. What stays out. Performance, pay, health, and personal matters are left out, and it tells you that it left them out. Other people appear by name and role only. See [Keep it safe](../docs/05-keep-it-safe.md).

The 1:1 is a different note. Log only the team's work from it here. The conversation itself becomes a meeting note named after the person, with work topics only (see [Meeting notes](meeting-notes.md)), or, if you turned on one-on-one logs in the build, an entry in that person's running log, which "Prepare my 1:1 with Alex Example" reads before the next one.

## If your vault predates this ritual

A vault built with an older rulebook has a team folder and hub but may have no check-in log. Paste this with the brackets filled.

---

Log a check-in for [team]: [paste or dictate the raw notes].

1. Add a dated entry to the team's check-in log with what I said, in my words, cleaned up: What happened, Decided, Next, Waiting on (who, what, since when), Links, Source. If the team has no running log yet, propose one named `YYYY-MM-DD [team] Log.md` in the team folder and create it after my yes.
2. Source: "said in chat" with today's date for what I say myself. If I pasted a Teams recap, a transcript, or someone's written update, record that as the source with its date instead.
3. Show me the before and after for the team hub: Current priorities if they changed, Waiting on (who, what, since when), Risks, Decisions. Wait for my yes.
4. If a line should become an item in [Jira, Azure DevOps, or GitHub Projects], say which and show me the create command. Run it only on my yes, and link the item by URL from the entry.
5. List what I promised and to whom. Offer to add them to the hub's Next steps with the date and to today's daily note; wait for my yes.
6. Leave out anything about performance, pay, health, or personal matters, and tell me you did. Names and roles only for other people.

Next: [Meeting notes](meeting-notes.md)
