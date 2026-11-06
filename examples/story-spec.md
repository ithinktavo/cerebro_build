# Example: a story spec and the week around it

Everything on this page is an illustration with placeholder data, written by hand to show the shapes one story leaves behind when the Specs switch is on: Jordan Example as the product owner for checkout, Alex Example as the tech lead on Team Alpha who reviews specs and builds the story, Checkout Migration, example-org/checkout-api, and Jira project ALPHA at example.atlassian.net through acli.
No tracker or repository was read to write it. The story keys, pull request numbers, commits, test runs, and tool output are made up, and the AI replies are what the rituals in [the build prompt](../prompts/build-work-vault.md) describe, not a transcript. The profile and the design this vault came from are in [product-owner-design-pass.md](product-owner-design-pass.md).

## 1. Monday: the morning names the story

`Daily/2026-11-09.md`, from "Start my day". Among the Plan lines, the Specs switch added this one for Checkout Migration. The second line it can add, developer questions on delivered stories, had nothing to say, so it did not print.

```markdown
- AI: ALPHA-123 Retry on timeout and ALPHA-124 Save card for later are next up with no spec. Source: Jira filter "Checkout Migration next up"; git ls-tree --name-only origin/main -- specs/ at 8e0f4a1, 2026-11-09.
```

## 2. "Spec for ALPHA-123"

The AI read the story in full through acli, description and comments, and pasted none of it; the Checkout Migration hub with its Priorities and Decisions; the checkout-api hub; and the clone after `git -C /Users/jordan/code/checkout-api switch main` and `git -C /Users/jordan/code/checkout-api pull --ff-only`, at commit 8e0f4a1. Then it showed this draft for `Projects/Checkout Migration/2026-11-09 ALPHA-123 Retry On Timeout Spec.md`, with the hub line, and waited. Every line it proposed starts with `AI:`; a line read from the repository ends with its path and commit; the rest is Jordan's, from the story or from chat. The reply also named what it left out: a comment on the story quoted a production order number and a customer's email address, and both became `order 1234` and `customer-0001`.

```markdown
---
type: plan
summary: "Spec for ALPHA-123, one retry of a capture call on a gateway timeout: scope, criteria, data, where in the code, open questions."
up:
  - "[[Checkout Migration]]"
created: 2026-11-09
created_by: ai
tags:
  - spec
  - checkout
---

# ALPHA-123: Retry on timeout

## Story
- Story: https://example.atlassian.net/browse/ALPHA-123, To Do as of 2026-11-09, owner Jordan Example, read with acli.
- Epic: https://example.atlassian.net/browse/ALPHA-100, Checkout Migration.
- Repository: example-org/checkout-api. Reviewer: Alex Example, tech lead.
- Version: r0, draft.

## Why
- A gateway timeout on capture fails the order today, and the customer pays again by hand or leaves.
- One retry turns most of those timeouts into completed orders without a second charge.
- Serves the Checkout Migration priority "fewer failed captures before the cut-over", Checkout Migration hub, Priorities, as of 2026-11-06.

## Scope
- In: one retry of a capture call when the payment gateway times out.
- Out: retries on a declined card, which is ALPHA-131, and retries from the storefront; web-storefront is untouched.

## Acceptance criteria
Verify lines are proposed from example-org/checkout-api at commit 8e0f4a1; the developer may replace them in the pull request.

### AC1 Retry once on timeout
- Given a capture call that times out after 5 seconds
- When the client has not retried this capture yet
- Then it retries once with the same idempotency key
- Verify: a unit test in `tests/payments/test_retry.py`, named `test_alpha_123_ac1_retries_once`
- Blocked by: Q1

### AC2 No second retry
- Given a capture call that was retried once
- When the retry times out after 5 seconds too
- Then the order fails with the existing error code `GATEWAY_TIMEOUT` after exactly 2 calls
- Verify: a unit test named `test_alpha_123_ac2_no_second_retry`

### AC3 One log per attempt
- Given a capture call that is retried
- When each attempt ends
- Then one log line is written per attempt with the order id, and the line carries no card data
- Verify: a unit test in `tests/payments/test_retry.py`, named `test_alpha_123_ac3_logs_each_attempt`
- Blocked by: Q2

### AC4 Late answer changes nothing
- AI: Given a capture call that timed out at 5 seconds and was retried
- AI: When the first call answers after the retry was sent
- AI: Then the order state comes from the retry only
- AI: Verify: a unit test in `tests/payments/test_retry.py`, named `test_alpha_123_ac4_late_answer_ignored`

## Data and interfaces
Sample values only.
- Setting `payment_timeout_ms`, today 5000, `src/payments/client.py at 8e0f4a1`.
- AI: Setting `payment_retry_delay_ms`, new, value from Q1.
- Event `payment.retried`, defined and never emitted today, `src/payments/client.py at 8e0f4a1`.
- Idempotency key: the first call's key is reused, sample `cap-0001`; order 1234; customer `customer-0001`.

## Where in the code (AI proposal, read at commit 8e0f4a1 on 2026-11-09)
- `src/payments/client.py`: `capture()` and its timeout; the retry goes around it.
- `src/checkout/handlers.py`: maps a gateway error to the order state.
- `tests/payments/test_retry.py`: the retry tests to extend.
- Similar merged pull request: https://github.com/example-org/checkout-api/pull/402, the timeout setting.

## Non-functional needs
- Request validation stays under 50 ms with the retry in place, as the existing latency test checks, `tests/checkout/test_latency.py at 8e0f4a1`.

## Rollout
- Behind the existing flag `payments.retry`, default off, `src/payments/flags.py at 8e0f4a1`; staging first, then production with the flag off; the flag is the rollback.
- checkout-api only, no migration. Jordan Example switches it on after Alex Example confirms the staging run.

## Open questions
- Q1: What is the delay before the retry? Owner Jordan Example, product owner, asked 2026-11-09. Blocks AC1.
- Q2: Does support need the retry logged, and where? Owner Jordan Example, product owner, asked 2026-11-09. Blocks AC3.

## Sources
- https://example.atlassian.net/browse/ALPHA-123, description and 3 comments, and its epic https://example.atlassian.net/browse/ALPHA-100, read 2026-11-09.
- example-org/checkout-api at 8e0f4a1, read 2026-11-09.
- Checkout Migration hub, Priorities and Decisions, as of 2026-11-06.
- Jordan Example in chat, 2026-11-09.

## Revisions
- none
```

Jordan answered in chat: "Q1: 2 seconds. Keep AC4. Yes." The AI applied the answer to Q1 and Sources, showed the two other lines it changed, AC1's Then and the new setting's value, as before and after, and created the note on that yes. AC1's Then now reads "retries once, after 2 seconds, with the same idempotency key" and its Blocked by line went; Q1 kept its line and its id under Open questions and gained "Answered 2026-11-09: 2 seconds"; Q2 and the Blocked by line on AC3 stay, since Jordan did not answer Q2; the `AI:` prefix came off the four AC4 lines and off the new setting, which now reads `payment_retry_delay_ms`, new, 2000. The Checkout Migration hub got its Specs line and its Notes in this folder line, Q2 went under the hub's Open questions with owner and date, and the project log got an entry. Nothing was written to the repository or to Jira.

## 3. Tuesday: review, then deliver

"Review the spec for ALPHA-123" re-read the note, the story's title and state, and the clone at HEAD, and printed the table:

| Check | Result |
| --- | --- |
| Every Then names one exact value | fail: AC3 joins two results with "and" |
| Every criterion has a Verify line naming a test path, steps, or a metric | fail: AC2 names a test and no path |
| Every criterion heading is AC plus at most four words | pass |
| Out has at least one line | pass |
| Every path exists at the current commit | pass: 5 paths, all present at HEAD |
| Every open question has an owner and a date, and a blocked criterion says so | pass: Q1 answered; Q2 open and AC3 says Blocked by: Q2 |
| No `AI:` line remains outside Where in the code | pass |
| Nothing looks like customer data, a record, a secret, a hostname, or an id | pass |
| Three to seven criteria and under 80 lines | pass: 4 criteria, 76 lines |
| The story link resolves and its title matches | pass |

Then the fixes, before and after, applied to the note on Jordan's yes. The card-data rule left AC3 and became a non-functional need, so AC3 keeps one result.

```diff
 ### AC2 No second retry
-- Verify: a unit test named `test_alpha_123_ac2_no_second_retry`
+- Verify: a unit test in `tests/payments/test_retry.py`, named `test_alpha_123_ac2_no_second_retry`
 ### AC3 One log per attempt
-- Then one log line is written per attempt with the order id, and the line carries no card data
+- Then one log line is written per attempt with the order id and the attempt number, 1 or 2
 ## Non-functional needs
+- Security: a log line or an event about a capture carries no card data, so no card number, expiry, or security code.
```

"Deliver the spec for ALPHA-123" ran the review again, and it passed. `gh repo view example-org/checkout-api --json viewerPermission` returned WRITE, `git -C /Users/jordan/code/checkout-api status --short` printed nothing, `git branch --list spec/ALPHA-123` and `git ls-remote --heads origin spec/ALPHA-123` printed nothing too, and the checkout-api hub's Specs section said the repository keeps no specs folder yet, so `specs/` is proposed in this pull request. Alex Example's GitHub handle had been a marked blank in that hub until Jordan said "My reviewer's handle for checkout-api is [handle]; update its hub" that morning, so the set carries `--reviewer`; it stands as `<handle>` below. The AI also said who can read the story, the organization, from the Specs section of the checkout-api hub, and that acli has no internal-comment option. The story comment ends after "the criterion id", because the repo hub's Rulebook line says the repository's rulebook does not name specs yet. Then it showed the file as it will be committed, the note's body with the properties block dropped and the version line now `r1, 2026-11-10`, then this set, and waited for one yes. Each command then ran behind the tool's own prompt.

```sh
git -C /Users/jordan/code/checkout-api switch main     # go to the team's main copy
git -C /Users/jordan/code/checkout-api pull --ff-only     # bring it up to date; refuses if the clone was touched
git -C /Users/jordan/code/checkout-api ls-files specs/ALPHA-123.md     # must print nothing; never overwrite
git -C /Users/jordan/code/checkout-api switch -c spec/ALPHA-123     # make the spec branch
# write specs/ALPHA-123.md: the note's body, properties block dropped
git -C /Users/jordan/code/checkout-api add specs/ALPHA-123.md     # stage the one file
git -C /Users/jordan/code/checkout-api commit -m "ALPHA-123: add spec"     # record it with that message
git -C /Users/jordan/code/checkout-api push -u origin spec/ALPHA-123     # upload the branch to GitHub
gh pr create -R example-org/checkout-api --head spec/ALPHA-123 --title "Spec ALPHA-123: Retry on timeout" --body "Spec r1 for https://example.atlassian.net/browse/ALPHA-123. Review the criteria; the code comes later. Open: Q2." --reviewer <handle>     # open the pull request
acli jira workitem comment create --key "ALPHA-123" --body "Spec r1 for review: <pull request URL>. After the merge: specs/ALPHA-123.md on main. Questions here as comments that open with the criterion id."     # post the comment on the story; the URL comes from gh pr create; comment create: check your version
git -C /Users/jordan/code/checkout-api switch main     # leave the clone on main
```

Jordan said yes. Pull request 456 opened, the comment landed on the story with its URL, and the clone was back on main. Then, reported and not asked for: the note's new first line, above its title, `Delivered 2026-11-10: https://github.com/example-org/checkout-api/pull/456, specs/ALPHA-123.md. The repository file is what developers follow.`; the hub's Specs line; the version line in the file now reads `r1, 2026-11-10` and its Revisions section's `none` became `r1, 2026-11-10: delivered for review`, and the note mirrors the file from here; the log entry; one `AI:` pointer line in the day's Log; `AI-Memory.md` and `AI-Log.md`; and the paste-ready copy of the spec as plain text, Where in the code dropped, for a Teams post or a Word page.

The Specs line in the Checkout Migration hub:

```markdown
- ALPHA-123 Retry on timeout (https://example.atlassian.net/browse/ALPHA-123): delivered r1 2026-11-10, https://github.com/example-org/checkout-api/pull/456; story To Do as of 2026-11-10; note [[2026-11-09 ALPHA-123 Retry On Timeout Spec]]. Source: gh and acli, 2026-11-10.
```

The entry appended to `Projects/Checkout Migration/2026-11-05 Checkout Migration Log.md`:

```markdown
## 2026-11-10
- What happened: delivered the spec for ALPHA-123, r1, as pull request 456 in checkout-api, reviewer Alex Example; one comment on the story points at it.
- Decided: nothing.
- Next: Alex Example reviews and merges 456; the code starts after the merge.
- Waiting on: Alex Example, the review of 456, since 2026-11-10.
- Links: https://github.com/example-org/checkout-api/pull/456, https://example.atlassian.net/browse/ALPHA-123.
- Source: gh and acli, 2026-11-10.
```

## 4. Wednesday: the developer starts

Alex Example reviewed and merged pull request 456 on 2026-11-11, under the repository's branch protection; the product owner never merges. Then, in a session opened on the clone with Alex's own vault added, Alex said "Start on ALPHA-123". The AI ran `git fetch origin` and read the spec first with `git show origin/main:specs/ALPHA-123.md`, with no switch and no pull, since a developer's own clone is never switched; then the story and the comments newer than the spec's version line, 2026-11-10, the project and repo hubs and the last three log entries, `git status --short`, `git branch --show-current`, `git log --oneline -10`, and `gh pr status`, and printed the plan:

```text
1. Spec: specs/ALPHA-123.md r1, pull request 456 merged 2026-11-11, owner Jordan Example. Story: In Progress, assignee Alex Example. Source: specs/ALPHA-123.md; acli, 2026-11-11.
2. The spec read the repository at 8e0f4a1; origin/main is at 9c1e2f4, 14 commits later. src/payments/client.py changed in pull request 451, logging, so I re-read it. Source: git log 8e0f4a1..origin/main, 2026-11-11.
3. AC3 is blocked by Q2, so the question goes on the story and AC3 waits.
4. Branch: alpha-123-retry-on-timeout from origin/main at 9c1e2f4, after your yes.
5. AC1: src/payments/client.py, a retry loop around capture() with the 2 second delay; tests/payments/test_retry.py::test_alpha_123_ac1_retries_once.
6. AC2: the same file; tests/payments/test_retry.py::test_alpha_123_ac2_no_second_retry.
7. AC3: blocked by Q2, skipped until the answer; then the same file and src/logging/fields.py; tests/payments/test_retry.py::test_alpha_123_ac3_logs_each_attempt.
8. AC4: the same file; tests/payments/test_retry.py::test_alpha_123_ac4_late_answer_ignored.
9. Out: declined cards and the storefront, untouched. src/checkout/handlers.py stays untouched too, because the client owns the timeout; this differs from the spec's Where in the code and goes in the pull request.
10. "Draft the PR for this branch" will list AC1, AC2, and AC4 as met and AC3 as not met until Q2 is answered. Reply yes to create the branch, or tell me what to change.
```

Alex said yes. The branch was created with `git switch -c alpha-123-retry-on-timeout origin/main`, and the question was shown and sent on a second yes:

```sh
acli jira workitem comment create --key "ALPHA-123" --body "Spec question, AC3: does support need the retry logged, and where? It decides the log shape."     # check your version
```

With the vault present, the question also landed under Waiting on in Alex's Checkout Migration hub, with Jordan Example's name and the date.

## 5. Thursday: the question comes back as a revision

Jordan's "Start my day" on 2026-11-12 carried the second Specs line:

```markdown
- AI: Spec question on ALPHA-123, AC3, from Alex Example, 2026-11-11. Say "Revise the spec for ALPHA-123: [answer]". Source: Jira filter "Checkout Migration spec question", 2026-11-12.
```

Jordan said "Revise the spec for ALPHA-123: yes, log the retry as a payment.retried event with the order id, no card data". The AI read `specs/ALPHA-123.md` on main after a fast-forward, since pull request 456 was merged, never the note, found Alex's comment by URL, and showed the diff: the answer under Open questions in Jordan's words with Alex's comment linked, AC3 reworded with its Blocked by line removed, and the version line bumped. Criteria keep their ids; the file's Revisions line carries the date and the change, because the pull request number is not known when the file is committed, and the note's line, written after the pull request opens, carries the URL as well.

```diff
-- Version: r1, 2026-11-10.
+- Version: r2, 2026-11-12.
 ...
-### AC3 One log per attempt
+### AC3 One event per attempt
 - Given a capture call that is retried
 - When each attempt ends
-- Then one log line is written per attempt with the order id and the attempt number, 1 or 2
+- Then one `payment.retried` event is emitted per attempt, with the fields under Data and interfaces
 - Verify: a unit test in `tests/payments/test_retry.py`, named `test_alpha_123_ac3_logs_each_attempt`
-- Blocked by: Q2
 ...
-- Event `payment.retried`, defined and never emitted today, `src/payments/client.py at 8e0f4a1`.
+- Event `payment.retried`, defined and never emitted today, `src/payments/client.py at 8e0f4a1`; fields `order_id` 1234, `attempt` 1 or 2, `reason` "timeout"; no card field. Support reads it in the log search.
 ...
-- Q2: Does support need the retry logged, and where? Owner Jordan Example, product owner, asked 2026-11-09. Blocks AC3.
+- Q2: Does support need the retry logged, and where? Owner Jordan Example, product owner, asked 2026-11-09. Blocks AC3. Answered 2026-11-12: yes, as a payment.retried event with the order id, no card data. Asked by Alex Example on the story, https://example.atlassian.net/browse/ALPHA-123?focusedCommentId=10001.
 ...
 ## Revisions
 - r1, 2026-11-10: delivered for review
+- r2, 2026-11-12: AC3 reworded, answers Q2
```

Then the set, shown first and run only after one yes, as for a delivery; the request was not the yes. The AI said again who can read the story before the comment, and each command ran behind the tool's own prompt:

```sh
git -C /Users/jordan/code/checkout-api switch main     # go to the team's main copy
git -C /Users/jordan/code/checkout-api pull --ff-only     # bring it up to date; refuses if the clone was touched
git -C /Users/jordan/code/checkout-api switch -c spec/ALPHA-123-r2     # make the revision branch
# apply the diff to specs/ALPHA-123.md
git -C /Users/jordan/code/checkout-api add specs/ALPHA-123.md     # stage the one file
git -C /Users/jordan/code/checkout-api commit -m "ALPHA-123: revise spec (r2)"     # record it with that message
git -C /Users/jordan/code/checkout-api push -u origin spec/ALPHA-123-r2     # upload the branch to GitHub
gh pr create -R example-org/checkout-api --head spec/ALPHA-123-r2 --title "Spec ALPHA-123: Retry on timeout, r2" --body "Spec r2 for https://example.atlassian.net/browse/ALPHA-123: AC3 reworded, answers Q2. AC1, AC2, and AC4 are unchanged." --reviewer <handle>     # open the pull request
acli jira workitem comment create --key "ALPHA-123" --body "Spec answer, AC3: log it as a payment.retried event with the order id, no card data, revised in <pull request URL>."     # post the answer on the story; the URL comes from gh pr create; comment create: check your version
git -C /Users/jordan/code/checkout-api switch main     # leave the clone on main
```

Jordan said yes. Pull request 470 opened, the comment on the story read "Spec answer, AC3: log it as a payment.retried event with the order id, no card data, revised in https://github.com/example-org/checkout-api/pull/470.", and Alex merged 470 that afternoon. The bookkeeping, not asked for: the note mirrored the revised file and gained the Revisions line with the URL, `r2, 2026-11-12, https://github.com/example-org/checkout-api/pull/470: AC3 reworded, answers Q2`; the hub's Specs line, now revised r2 2026-11-12; a log entry. Nobody edited the note by hand; the repository file is the spec.

## 6. Friday: the code pull request

Alex's "Start on ALPHA-123" on Friday morning read the file at r2 first and planned AC3 from it. By the afternoon the four tests passed, and "Draft the PR for this branch" read the diff, the spec at r2, the story, and the pull request template, and showed this body:

```markdown
Story: https://example.atlassian.net/browse/ALPHA-123
Spec: specs/ALPHA-123.md, r2, merged in https://github.com/example-org/checkout-api/pull/470

## What changed
- One retry of a capture call on a gateway timeout, after 2 seconds, with the same idempotency key, behind `payments.retry`, default off.
- One `payment.retried` event per attempt with `order_id`, `attempt`, and `reason`; no card field.

## Acceptance criteria
- AC1 met: tests/payments/test_retry.py::test_alpha_123_ac1_retries_once, unit, run https://github.com/example-org/checkout-api/actions/runs/123
- AC2 met: tests/payments/test_retry.py::test_alpha_123_ac2_no_second_retry, unit, run https://github.com/example-org/checkout-api/actions/runs/123
- AC3 met: tests/payments/test_retry.py::test_alpha_123_ac3_logs_each_attempt, unit, per spec r2, run https://github.com/example-org/checkout-api/actions/runs/123
- AC4 met: tests/payments/test_retry.py::test_alpha_123_ac4_late_answer_ignored, unit, run https://github.com/example-org/checkout-api/actions/runs/123

Differed from Where in the code: src/checkout/handlers.py untouched, the client owns the timeout.
```

Pull request 471 opened after Alex's yes, and its URL went into the vault log. "Close the session" wrote the log entry, linking the story, the spec at r2, and pull request 471, and offered the transition the team uses, run only on a yes:

```sh
acli jira workitem transition --key "ALPHA-123" --status "In Review"     # the status names are the team's; check your version
```

## 7. Friday: Jordan closes the week

"Close the week" gained no step. "What did I ship this week?" listed pull requests 456 and 470 under checkout-api, both merged. Jordan then said "Status report for Checkout Migration for this week", since Reports I owe is none and the report comes only on request; `Projects/Checkout Migration/2026-11-13 Checkout Migration Status Report.md` took the spec lines under its five headings; the two headings not shown had nothing from the specs.

```markdown
## Done
- Spec ALPHA-123 r2 merged. Source: https://github.com/example-org/checkout-api/pull/470

## In progress
- ALPHA-123 code in review, 4 of 4 criteria met. Source: https://github.com/example-org/checkout-api/pull/471

## Next
- ALPHA-124 Save card for later needs a spec. Source: Jira filter "Checkout Migration next up", 2026-11-13
```

"Close the week" on 2026-11-20 found pull request 471 merged on 2026-11-17 and the story Done in Jira. It added `Built by: https://github.com/example-org/checkout-api/pull/471, merged 2026-11-17` under the Delivered line of the note, set `status: done` in its properties, and refreshed the hub's Specs line. Nobody edited the note by hand.

Next: [the build prompt](../prompts/build-work-vault.md), or [the product owner's design pass](product-owner-design-pass.md) for the profile and the design this vault came from.
