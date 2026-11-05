# Example: the vault after one week

Everything on this page is an illustration with placeholder data, written by hand to show the shapes a week of use leaves behind: Alex Example, Team Alpha and Team Beta, example-org/checkout-api and example-org/web-storefront, the Director of Platform, the Platform manager, and Sam Example as the tech lead on Team Alpha.
No tracker or repository was read to write it. The issue and pull request numbers, commits, times, and tool output are made up, and the AI replies are what the rituals in [the build prompt](../prompts/build-work-vault.md) describe, not a transcript.

## 1. A daily note at the end of the day

`Daily/2026-11-10.md`, a Tuesday in the second week: the vault was built on Thursday 2026-11-05, and the repos were read and the first reports written on Friday 2026-11-06. The Plan lines are the AI's, from "Start my day", each ending with its source. The two checkboxes and the Log lines are Alex's; the only thing the AI added to them is the marker after the yes at "Close my day".

```markdown
## Plan
- AI: 1:1s today. One-on-one logs are off, so nothing to prepare from the vault. Source: [[Me]], My week and Note habits.
- AI: Carried from 2026-11-06, third morning: fill in the last day of the quarter under Milestones. Give it a date in [[Checkout Migration]] today or drop it. Source: [[2026-11-06]] and [[2026-11-09]], Plan.
- AI: Waiting on the Platform manager for payments sandbox access, issue 418, since 2026-10-28, 13 days. Source: [[Team Alpha]], Waiting on.
- AI: Weekly status for both teams and the roll-up are due Friday 2026-11-13. Team Beta's still lacks the three saved Jira filters. Source: [[Reports]], Recipes; [[Team Beta]], Tracker and queries.
- AI: Team Beta has no check-in this week. Last entry 2026-11-06. Source: [[2026-11-05 Team Beta Log]].
- AI: Open pull requests: PR 421 in checkout-api, Sam Example's flag plumbing, waits for your review since 2026-11-09, checks passing; your PR 423 in checkout-api has one failing check; your PR 233 in web-storefront, checks passing. Source: gh search prs and gh pr status, 2026-11-10.
- AI: Assigned to you in Jira: OBS-141, alert routing for the checkout dashboards, In progress, due 2026-11-18. Source: acli, assigned to me, 2026-11-10.
- AI: [[web-storefront]] was read at commit 3f9c2ab on 2026-11-06 and main has moved since, so its Architecture is stale until re-read; say "Where did we leave off on web-storefront?". Source: [[web-storefront]], Read at commit; git log, 2026-11-10.
- [x] review Sam's flag PR
- [ ] cut-over options for the Director

## Log
- [[Team Alpha]] standup: 412 merged, Sam's flag PR 421 is up and wants my review, 418 still stuck on the payments sandbox, Sam wants a cut-over date before planning Thursday → [[Team Alpha]]
- told the Director of Platform I'd send cut-over options by Thursday → [[Checkout Migration]]
- decided with Sam: 418 waits for the real sandbox, no local mocks, not worth a week → [[Checkout Migration]]
- checkout-api gotcha: make test hangs instead of failing when the payments sandbox is down, check the sandbox before blaming the branch → [[checkout-api]]
- idea: Checkout Error Budget Dashboard, one page with the error budget per checkout path so the cut-over has a number to watch → [[2026-11-10 Checkout Error Budget Dashboard]]
- stop reading the board during standup, listen first (stays)
- AI: closed 17:40
```

## 2. The filing table before the yes

"Close my day" re-read the note and showed this table. Nothing was written until Alex answered.

| Line | Destination | Action |
| --- | --- | --- |
| [[Team Alpha]] standup: 412 merged, Sam's flag PR 421 ... | `Teams/Team Alpha/2026-11-05 Team Alpha Log.md`, then [[Team Alpha]] | Append the entry `## 2026-11-10` in your words, shown in the next section. Hub: refresh Current state and keep 418 under Waiting on with its date. |
| told the Director of Platform I'd send cut-over options by Thursday | [[Checkout Migration]], Next steps | Add `- [ ] Send cut-over options to the Director of Platform (owner Alex, due 2026-11-12)`. Also offered, runs only on its own yes: `gh project item-create 7 --owner example-org --title "Cut-over options for checkout" --body "Owner Alex Example, due 2026-11-12"` |
| decided with Sam: 418 waits for the real sandbox, no local mocks | `Projects/Checkout Migration/2026-11-10 Wait For Payments Sandbox Decision.md` | Create from Decision Template: status decided, decided by Alex Example and Sam Example on 2026-11-10, source said in chat. One line under Decisions in [[Checkout Migration]]. |
| checkout-api gotcha: make test hangs instead of failing ... | [[checkout-api]], Gotchas | Add "2026-11-10: `make test` hangs instead of failing when the payments sandbox is down. Check the sandbox first. Source: said in chat, 2026-11-10." |
| idea: Checkout Error Budget Dashboard ... | `Notes/2026-11-10 Checkout Error Budget Dashboard.md` | Create from Note Template, `up` [[Home]], tag `idea`, your line as the body. |
| stop reading the board during standup, listen first | stays | None. |

Alex answered "yes, skip the board item". The markers were appended, `AI: closed 17:40` ended the section, the command did not run, and the summary listed one promise: cut-over options to the Director of Platform by 2026-11-12.

## 3. The check-in log entry that resulted

Appended to `Teams/Team Alpha/2026-11-05 Team Alpha Log.md`, in the one entry shape every log uses, in Alex's words.

```markdown
## 2026-11-10
- What happened: standup. 412 merged, Sam's flag PR 421 is up and wants my review, 418 still stuck on the payments sandbox, Sam wants a cut-over date before planning Thursday.
- Decided: nothing in standup. Later that day: 418 waits for the real sandbox, no local mocks, in [[2026-11-10 Wait For Payments Sandbox Decision]].
- Next: Alex sends cut-over options to the Director of Platform by 2026-11-12, before planning, so Sam has a date.
- Waiting on: the Platform manager, payments sandbox access for issue 418, since 2026-10-28.
- Links: https://github.com/example-org/checkout-api/issues/412, https://github.com/example-org/checkout-api/pull/421, https://github.com/example-org/checkout-api/issues/418.
- Source: said in chat, 2026-11-10.
```

## 4. "Where did we leave off on checkout-api?"

Asked at 10:05 on 2026-11-10. The AI read the hub and the last three log entries, ran git and gh in the repo, read the linked tracker item, refreshed Current state, and answered in ten lines.

```text
1. Left off Monday 2026-11-09, end of session: Sam Example opened PR 421, the feature flag plumbing, and asked for your review; 418 was waiting on the sandbox. Source: [[2026-11-05 Checkout Migration Log#2026-11-09]].
2. The hub was read at commit 8e0f4a1 on 2026-11-06; main is now at 9c1e2f4, so I re-read it first. Local: branch fix/address-validation, clean, one commit ahead of origin. Source: git status and git log, 2026-11-10.
3. Moved since: PR 421's checks pass, 2 of 2, and nobody has reviewed it yet. Source: https://github.com/example-org/checkout-api/pull/421; gh pr status, 2026-11-10.
4. Moved since: your PR 423, address validation for issue 415, failed its integration check overnight with a timeout. Source: https://github.com/example-org/checkout-api/pull/423; gh pr checks, 2026-11-10.
5. Tracker: issue 418 is In progress on the board, owner Sam Example, no change since 2026-11-06; the hub has it waiting on sandbox access since 2026-10-28. Source: https://github.com/example-org/checkout-api/issues/418.
6. Next: review PR 421 today, as your Plan says. Source: [[2026-11-10]], Plan.
7. Next: find why PR 423's integration check timed out, then re-run it. Source: [[Checkout Migration]], Next steps.
8. Next, by the deploy order: checkout-api deploys first, then web-storefront, so PR 233 waits for PR 421 to deploy. Source: [[Checkout Migration]], Repos and deploy order.
9. Waiting: sandbox access from the Platform manager, 13 days. Source: [[Team Alpha]], Waiting on.
10. Waiting: the cut-over window, with the Director of Platform, no date yet. Current state in [[checkout-api]] is refreshed as of 2026-11-10 at commit 9c1e2f4. Source: [[Checkout Migration]], Open questions.
```

## 5. The weekly status report for Team Alpha

`Teams/Team Alpha/2026-11-13 Team Alpha Status Report.md`, drafted by "Status report for Team Alpha for this week" from project 7 through the three named queries, the check-in entries since 2026-11-06, the hub, and last week's report, and saved after a yes.

```markdown
---
type: report
summary: "Weekly status of Team Alpha for the Director of Platform: done, in progress, blocked, decisions needed, next, every line with its source."
up:
  - "[[Team Alpha]]"
created: 2026-11-13
created_by: ai
tags:
  - checkout
---

# 2026-11-13 Team Alpha Status Report
- Delta since last week: last week's Next listed 412, 415, and the flag plumbing; all three are Done. 418 went from In progress to Blocked on 2026-11-10. Source: [[2026-11-06 Team Alpha Status Report]], Next.
- Tracker and vault disagree on 418: the board says In progress, last changed 2026-11-06; the check-in of 2026-11-10 says blocked. The vault is newer, so 418 is under Blocked below, and the board edit was offered in chat. Source: [[2026-11-05 Team Alpha Log#2026-11-10]].

## Done
- Order service client, issue 412, closed 2026-11-06 by PR 419. Source: https://github.com/example-org/checkout-api/issues/412
- Feature flag plumbing, PR 421, merged 2026-11-11. Source: https://github.com/example-org/checkout-api/pull/421
- Address validation on the new service, issue 415, Done on the board 2026-11-12. Source: https://github.com/example-org/checkout-api/issues/415
- Checkout ships behind a feature flag, default off, until Team Beta is trained. Source: [[2026-11-11 Feature Flag Until Beta Is Trained Decision]]

## In progress
- Storefront reads the checkout flag, PR 233, checks passing, held until checkout-api deploys first. Source: https://github.com/example-org/web-storefront/pull/233

## Blocked or at risk
- Payments capture, issue 418, blocked on sandbox access from the Platform manager since 2026-10-28, 16 days, asked again 2026-11-06; no local mock, by decision. Source: https://github.com/example-org/checkout-api/issues/418
- The end-of-quarter milestone depends on Team Beta's training date, which has none yet. Source: [[Checkout Migration]], Risks, raised 2026-11-11

## Decisions needed
- Cut-over window: a two-hour window in the week of 2026-11-30, as proposed in the options sent on 2026-11-12; the Director of Platform decides, by 2026-11-20. Source: said in chat, 2026-11-12

## Next
- Deploy checkout-api with the flag off on 2026-11-17, then merge and deploy PR 233, in that order. Source: [[Checkout Migration]], Repos and deploy order
- Training plan for Team Beta drafted with Team Beta's tech lead by 2026-11-18, owner Alex Example. Source: [[Checkout Migration]], Next steps
```

The paste-ready copy that came with it, for Teams:

```text
Team Alpha status, week of 2026-11-09 to 2026-11-13
Delta since last week: 412, 415, and the flag plumbing were Next and are Done. 418 went from In progress to Blocked on 2026-11-10.
Done
- Order service client, issue 412, closed 2026-11-06 by PR 419. https://github.com/example-org/checkout-api/issues/412
- Feature flag plumbing, PR 421, merged 2026-11-11. https://github.com/example-org/checkout-api/pull/421
- Address validation on the new service, issue 415, done 2026-11-12. https://github.com/example-org/checkout-api/issues/415
- Checkout ships behind a feature flag, default off, until Team Beta is trained (decision note of 2026-11-11).
In progress
- Storefront reads the checkout flag, PR 233, checks passing, held until checkout-api deploys first. https://github.com/example-org/web-storefront/pull/233
Blocked or at risk
- Payments capture, issue 418, blocked on sandbox access from the Platform manager since 2026-10-28, 16 days. https://github.com/example-org/checkout-api/issues/418
- The end-of-quarter milestone depends on Team Beta's training date, which has none yet.
Decisions needed
- Cut-over window: a two-hour window in the week of 2026-11-30; the Director of Platform decides, by 2026-11-20.
Next
- Deploy checkout-api with the flag off on 2026-11-17, then merge and deploy PR 233, in that order.
- Training plan for Team Beta drafted by 2026-11-18.
Sources: GitHub project 7 (issues 412, 415, 418; pull requests 421 and 233); Team Alpha check-ins of 2026-11-09, 2026-11-10, and 2026-11-12; the decision note "2026-11-11 Feature Flag Until Beta Is Trained Decision"; the Checkout Migration hub; the Team Alpha status report of 2026-11-06; said in chat on 2026-11-12.
```

## 6. The leadership roll-up

`Reports/2026-11-13 Weekly Roll-Up.md`, from "Roll up this week for leadership", after both team reports existed. Properties as in the status report, with `up` [[Reports]] and the tag `rollup`. The same run refreshed Open asks of leadership in the Reports hub with the two decisions below.

```markdown
# 2026-11-13 Weekly Roll-Up

## Headline
- Checkout Migration moved: the flag plumbing merged, and checkout ships behind a flag until Team Beta is trained. Source: [[2026-11-13 Team Alpha Status Report]].
- One blocker is older than two weeks: payments sandbox access for Team Alpha, with the Platform manager. Source: [[Team Alpha]], Waiting on.
- Two decisions wait on leadership, the cut-over window and the sandbox access, both due by 2026-11-20. Source: [[Reports]], Open asks of leadership.

## By team

### Team Alpha
- Delta since last week: 412, 415, and the flag plumbing are Done; 418 went from In progress to Blocked. Source: [[2026-11-13 Team Alpha Status Report]]; [[2026-11-06 Weekly Roll-Up]].
- Traffic state (proposed): amber, because 418 is blocked and the cut-over window is undecided.

### Team Beta
- Delta since last week: alert routing for the checkout dashboards, OBS-141, moved to In review; the three Jira filters are saved and recorded in the hub. Source: [[2026-11-13 Team Beta Status Report]]; https://example.atlassian.net/browse/OBS-141.
- Traffic state (proposed): green, with the training date for the new checkout service as the one open item.

## Risks new or changed
- Payments sandbox access for issue 418, owner the Platform manager, 16 days, unchanged since last week. Source: [[Team Alpha]], Risks.
- Team Beta's training has no date, which keeps the flag off; owner Alex Example, new, raised 2026-11-11. Source: [[Checkout Migration]], Risks.

## Decisions needed
- Cut-over window for checkout: a two-hour window in the week of 2026-11-30; the Director of Platform decides, by 2026-11-20. Source: [[2026-11-13 Team Alpha Status Report]].
- Sandbox access for Team Alpha: the Platform manager decides, by 2026-11-17; raised here after no answer since 2026-11-06. Source: [[Team Alpha]], Waiting on.

## Milestones in the next 30 days
- 2026-11-25: Team Beta trained on the new checkout service. Source: [[Checkout Migration]], Milestones.
- 2026-12-02: checkout flag on for internal traffic. Source: [[Checkout Migration]], Milestones.

## Team reports
- [[2026-11-13 Team Alpha Status Report]]
- [[2026-11-13 Team Beta Status Report]]
```

## 7. The weekly review

`Notes/2026-11-13 Weekly Review.md`, from "Write this week's review" at the end of "Close the week". Properties as in the status report, with `type` note, `up` [[Home]], and the tag `review`.

```markdown
# 2026-11-13 Weekly Review

## What moved
- Checkout Migration: 412, 415, and the flag plumbing merged, and checkout ships behind a flag until Team Beta is trained. Source: [[2026-11-13 Team Alpha Status Report]].
- Shipped by me: PR 423 merged in checkout-api; PR 233 open in web-storefront, held by the deploy order in the hub, not by memory. Source: "What did I ship this week?", gh, 2026-11-13; [[Checkout Migration]], Repos and deploy order.

## What stalled
- 418 has waited 16 days on sandbox access and stopped on 2026-11-10 rather than mock it. Source: [[Team Alpha]], Waiting on; [[2026-11-10 Wait For Payments Sandbox Decision]].
- Observability Rollout had no session this week; its Current state is still the build line. Source: [[Observability Rollout]].

## Promises kept and not kept
- Kept: cut-over options to the Director of Platform by Thursday, sent 2026-11-12. Source: [[2026-11-10]] and [[2026-11-12]], Log.
- Not kept: the training plan with Team Beta's tech lead, promised for this week, now due 2026-11-18. Source: [[2026-11-05 Team Beta Log#2026-11-12]].

## What to drop
- The Plan line about the Jira filters: saved and recorded on 2026-11-12, so it leaves the morning list. Source: [[Team Beta]], Tracker and queries.

## Next week's three
1. Deploy checkout-api with the flag off, then merge and deploy PR 233, in that order.
2. Get the sandbox answer from the Platform manager, or escalate through the Director of Platform on 2026-11-17.
3. Draft the Team Beta training plan with Team Beta's tech lead by 2026-11-18.

## Update for my team
Checkout moved this week: the order service client, address validation, and the feature flag plumbing all merged, and we decided checkout ships behind a flag, default off, until Team Beta is trained on the new service. The storefront change waits for the checkout-api deploy, in that order. Payments capture is still blocked on sandbox access, which is now with the Director of Platform. Next week: the checkout-api deploy, the storefront merge, and the training plan with Team Beta.
```

With the review, the AI proposed new Current focus lines for `Home.md`. They are a proposal; nothing in `Home.md` changes until Alex says yes:

- Checkout Migration: flag plumbing merged; checkout behind a flag until Team Beta is trained; cut-over window with the Director of Platform by 2026-11-20. As of 2026-11-13. Source: [[2026-11-13 Team Alpha Status Report]].
- Observability Rollout: ongoing; alert routing for the checkout dashboards in review, OBS-141; Team Beta's training date open. As of 2026-11-13. Source: [[2026-11-13 Team Beta Status Report]].

## 8. A decision note

`Projects/Checkout Migration/2026-11-11 Feature Flag Until Beta Is Trained Decision.md`, from "Write a decision note: we decided X because Y; the alternatives were Z", linked from the Checkout Migration hub under Decisions. Properties as in the status report, with `type` decision and `up` [[Checkout Migration]].

```markdown
# 2026-11-11 Feature Flag Until Beta Is Trained Decision

## Context
- The flag plumbing, PR 421, merged on 2026-11-11, so checkout can run on the new service for any share of traffic. Source: https://github.com/example-org/checkout-api/pull/421.
- Team Beta owns the dashboards and alerts for checkout and has not been trained on the new service. The Platform manager asked in the staff meeting of 2026-11-09 that checkout not switch before that. Source: said in chat, 2026-11-11.

## Decision
- Checkout ships behind the feature flag, default off, in every environment. The flag turns on for internal traffic after Team Beta's training, and for customers only after the cut-over window is decided.

## Alternatives
- Switch a share of traffic to the new service now and train Team Beta in parallel. Rejected: an alert on the new service would page a team that cannot read it.
- Hold PR 421 unmerged until the training. Rejected: the branch would drift for two weeks, and 415 and 418 build on it.

## Consequences
- The end-of-quarter milestone depends on the training date, recorded as a risk in [[Checkout Migration]] on 2026-11-11, owner Alex Example.
- Two new milestones in [[Checkout Migration]]: Team Beta trained, 2026-11-25; flag on for internal traffic, 2026-12-02.

## Decided by and when
- Alex Example, engineering manager, with Sam Example, tech lead of Team Alpha, 2026-11-11.

## Status
- decided

Source: said in chat, 2026-11-11: "Write a decision note: we decided checkout ships behind a flag, default off, until Team Beta is trained, because an alert on the new service would page a team that cannot read it; the alternatives were switching a share of traffic now or holding PR 421 unmerged."
```

Next: [the build prompt](../prompts/build-work-vault.md), or the [sample vault](sample-vault/) for the hubs and templates these notes were made from.
