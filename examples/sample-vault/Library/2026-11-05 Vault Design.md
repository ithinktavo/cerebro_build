---
type: note
summary: "Why this vault is shaped the way it is: modules on and off with reasons, the mapping table, the defaults Alex accepted, alternatives not chosen, and what to revisit after the first month."
up:
  - "[[Home]]"
created: 2026-11-05
created_by: ai
tags:
  - vault
  - design
---

Built on 2026-11-05 from Alex's profile, after the design pass was approved with "yes" in chat. Every fact below comes from the profile or from a design default Alex accepted.

## Modules

- Developer: on. Two repositories are named, and the roles include developer.
- Teams: on. Team Alpha and Team Beta are named, and two tech leads report to Alex. One-on-one logs: off, as the profile says.
- Reports: on. A weekly status is owed across two teams, and the roles include manager.
- Specs: off. Specs for my stories was left blank.

## Mapping table

| Item | Module | Links |
| --- | --- | --- |
| [[Checkout Migration]] | Project | [[Team Alpha]] works it; repos [[checkout-api]] and [[web-storefront]]; record: GitHub Projects, owner example-org, project 7, shared with Team Alpha |
| [[Observability Rollout]] | Project, Goal says ongoing | [[Team Beta]] works it; record: Jira at example.atlassian.net through acli, shared with Team Beta |
| [[checkout-api]] | Repo | /Users/alex/code/checkout-api; serves Checkout Migration; which part and its place in the deploy order live in the project hub |
| [[web-storefront]] | Repo | /Users/alex/code/web-storefront; serves Checkout Migration; same |
| [[Team Alpha]] | Team | reports through the Director of Platform; works Checkout Migration; GitHub Projects project 7 |
| [[Team Beta]] | Team | reports through the Director of Platform; works Observability Rollout; Jira |
| Weekly status | Report, recipe in [[Reports]] | to the Director of Platform, Fridays, posted in Teams; one report per team, then one roll-up, because leadership reads by team |

## Defaults Alex accepted in the design pass

1. The fact Alex is tired of re-explaining, which repository serves which part of checkout and the deploy order, lives in [[Checkout Migration]]; each repo hub points to it.
2. Team Beta and Observability Rollout share one Jira project; the key is left blank.
3. GitHub project 7 holds all of Team Alpha's work; the Checkout Migration hub filters it by a field left blank.
4. On Fridays Alex posts the roll-up, built from the two team reports.

## Alternatives not chosen

- Observability Rollout as a section of the Team Beta hub instead of a project: a standing responsibility is a project whose Goal says ongoing, and it needs its own log.
- One combined weekly status instead of one per team plus a roll-up: leadership reads by team.
- A One-on-One Log template built in case: 1:1 logs are off, and nothing is built in case. It is added if Alex turns them on.
- Repo logs created at build: a repo log is created on first need.
- Team logs named "Check-In Log": the one naming pattern is `YYYY-MM-DD <Name> Log.md`, and the hub calls it the check-in log.
- A People or Areas folder for the tech leads or the Director of Platform: no other folder kinds exist; names and roles live in the team hubs.
- Reading the repositories or the trackers during the build: the prompt forbids it, so every value that needs a tool is a marked blank.

## Revisit after 30 days, from 2026-12-05

- Is Observability Rollout still its own project, or has it folded into Team Beta's routine?
- Do the three named queries per team exist, and are they recorded in [[Team Alpha]] and [[Team Beta]]?
- Were [[checkout-api]] and [[web-storefront]] filled in, and have their commits moved since?
- Has any topic piled up three notes in `Notes/`, asking for a folder?
- Are the Friday reports written from sources, and is the roll-up still the right thing to post?
- Is anything in `Home.md` Current focus older than 30 days?
