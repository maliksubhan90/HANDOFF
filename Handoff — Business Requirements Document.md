# Handoff — Business Requirements Document

Oct 26, 2026 · @Subhan Abdullah

## Document control

| Field | Value |
| --- | --- |
| Product | Handoff (Meeting Action Items to Slack) |
| Document | Business Requirements Document (BRD) |
| Version | 1.0 |
| Status | Draft for client review |
| Author | Subhan Abdullah, Project Manager |
| Client sponsor | Head of Operations (client) |
| Course context | M2 Digital Project Management, Week 1: Build First Project Tool |
| Related documents | Handoff PRD v1.0, README, Brand kit |

## Executive summary

Handoff cuts the time to send a meeting's action items to Slack from about 15 minutes to about 3, without building a new platform.

Today someone reads each transcript, copies out who agreed to do what, and types a Slack recap by hand. The client asked for a simple tool that does four things: take a transcript, find action items and owners, let a person review them, and post the final update to Slack.

Handoff is a single web page with no accounts and no database. It extracts action items in the browser, shows them in an editable list, and posts the approved recap through a Slack incoming webhook. The client's instruction to keep it lean is treated as a requirement, not a preference: every feature request is tested against the four jobs above.

## Business problem and current process

The team loses time and follow-through because action items are pulled out of meeting notes by hand.

**Client statement:** "We're wasting time manually pulling action items from meeting notes and sending Slack recaps."

### Current process (as-is)

1. The meeting ends and the notetaker exports or opens the transcript.
2. The notetaker reads the full transcript to find commitments and requests.
3. They work out who owns each item and any due date mentioned.
4. They type a recap message in Slack, formatting it by hand.
5. Owners reply in thread when something is wrong or missing.

### Pain points

- **Time:** about 10–20 minutes per meeting is spent on a clerical task (to be confirmed with the client).
- **Missed items:** commitments made in passing ("I can take that") are easy to overlook.
- **Unclear ownership:** items like "we need someone to…" go out with no owner.
- **Delay:** recaps are often sent hours later, after the team has moved on.
- **Inconsistency:** each notetaker formats the recap differently, so owners scan for their name.

## Business objectives and success metrics

Success means recaps go out faster, with owners on every item, and the team keeps using the tool after the first month.

Objectives follow the SMART format. Baselines are estimates until measured in week 1 of the pilot.

| # | Objective (SMART) | Metric | Baseline | Target | Measured by |
| --- | --- | --- | --- | --- | --- |
| O1 | Cut the time to produce a meeting recap within 4 weeks of launch | Minutes from transcript in hand to recap posted | \~15 min | ≤ 3 min | Timed sample of 10 meetings |
| O2 | Every posted action item has a named owner by week 4 | % of posted items with an owner | Unknown | ≥ 95% | Count in posted recaps |
| O3 | Recaps go out the same day as the meeting | % of meetings recapped within 1 hour | Unknown | ≥ 80% | Slack post time vs meeting end |
| O4 | Extraction is good enough that review stays quick | % of extracted items kept without rewriting | n/a | ≥ 70% | Pilot review log |
| O5 | The team adopts it | Meetings recapped with Handoff ÷ recurring meetings | 0% | ≥ 75% by week 6 | Weekly count |

## Stakeholders and RACI

The client sponsor approves scope; the notetaker is the primary user; owners only read the Slack post.

| Stakeholder | Role | Interest |
| --- | --- | --- |
| Client sponsor (Head of Operations) | Requested the tool, approves scope and budget | Time saved, follow-through |
| Meeting notetaker | Primary user: pastes transcript, reviews, posts | Speed, accuracy, little setup |
| Action item owners | Receive the Slack recap | Clear task, owner, due date |
| Slack workspace admin | Approves the incoming webhook | Security, channel hygiene |
| Project manager (Subhan Abdullah) | Delivers the tool and documents | Scope, quality, schedule |

**RACI** (R = Responsible, A = Accountable, C = Consulted, I = Informed)

| Activity | Sponsor | PM | Notetaker | Slack admin | Owners |
| --- | --- | --- | --- | --- | --- |
| Approve scope (BRD/PRD) | A | R | C | I | I |
| Build and test the tool | I | A/R | C | I | – |
| Set up the Slack webhook | I | C | I | A/R | – |
| Pilot (4 weeks) | A | R | R | I | C |
| Measure success metrics | A | R | C | – | I |
| Go / no-go after pilot | A/R | C | C | I | I |

## Scope

Version 1 does the four jobs the client named and nothing else; everything else waits for evidence from the pilot.

| In scope (v1) | Out of scope (v1) |
| --- | --- |
| Paste a text transcript (Zoom, Meet, Teams or typed notes) | Joining or recording meetings, audio transcription |
| Find action items, owners and due dates automatically | Task tracking after posting (status, reminders, completion) |
| Review screen: edit, add, remove, reassign items | User accounts, logins, team workspaces |
| Preview the Slack message before posting | Storing transcripts or history in a database |
| Post to one Slack channel via incoming webhook; copy as fallback | Real @mentions that notify users (needs a Slack app and user IDs) |
| Runs in a browser with no install | Integrations with Jira, Asana, email or calendars |
|  | Analytics dashboards |

**Scope guardrail:** a new feature enters v1 only if the notetaker cannot complete one of the four jobs without it.

## Future process (to-be)

The notetaker spends their time on judgment (is this right, who owns it) instead of copying and formatting.

&#91;embedded content: to-be process · 3 lanes, 7 steps, 1 decision\]

Handoff does the reading and formatting; the person keeps the decision. Nothing posts until the notetaker has reviewed the list, and an item without an owner is flagged before posting.

## High-level business requirements

Eight requirements cover the client's four jobs plus the constraints that keep the tool lean and safe. Detailed functional requirements and acceptance criteria are in the PRD.

| ID | Requirement | Client job it serves | Priority |
| --- | --- | --- | --- |
| BR-1 | Accept a meeting transcript as pasted text from common tools | Take a transcript | Must |
| BR-2 | Identify action items, their owners and any stated due dates | Identify items and owners | Must |
| BR-3 | Let a person edit, add, remove and reassign items before sending | Quick review | Must |
| BR-4 | Post the approved recap to a chosen Slack channel | Post to Slack | Must |
| BR-5 | Show exactly what will be posted before posting | Quick review | Must |
| BR-6 | Complete a typical recap (30–60 min meeting) in under 3 minutes | All | Must |
| BR-7 | Need no accounts, installs or new systems to adopt | Keep it lean | Must |
| BR-8 | Keep meeting content private: nothing stored, only the final recap leaves the browser | Keep it lean / trust | Must |

## Assumptions, constraints and dependencies

**Assumptions**

- The team already gets text transcripts from its meeting tool or writes notes with speaker names.
- Transcripts are in English for v1.
- One Slack channel per recurring meeting is enough; the notetaker picks the webhook for that channel.
- A person always reviews before posting; the tool is never expected to be 100% accurate.

**Constraints**

- Client instruction: "Keep it lean. Don't let this turn into a massive platform."
- Course timebox: one week to build and document.
- Budget: no paid services required to run v1.

**Dependencies**

- A Slack workspace admin creates an incoming webhook for the target channel.
- A modern browser (Chrome, Edge, Firefox or Safari, current versions).

## Risks and mitigations

The biggest risk is scope creep, which the client named directly; the second is extraction misses, which the review step contains.

| ID | Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- | --- |
| R1 | Scope creep turns the tool into a task-management platform | High | High | Scope guardrail; change requests need sponsor approval; out-of-scope list in this BRD | PM |
| R2 | Extraction misses items or picks the wrong owner | Medium | Medium | Mandatory human review; source quote shown per item; "needs owner" flag | PM |
| R3 | Transcripts in unusual formats are not parsed | Medium | Medium | Support the common "Name: text" format; manual add; collect samples in pilot | PM |
| R4 | Webhook URL is leaked and someone posts to the channel | Low | Medium | Kept in the browser tab only; never stored or logged; admin can rotate it | Slack admin |
| R5 | Low adoption: notetakers keep the old habit | Medium | High | 3-minute demo; pilot with 2 recurring meetings first; measure O5 weekly | Sponsor |
| R6 | Sensitive meeting content leaves the company | Low | High | Processing runs in the browser; no server, no third-party AI in v1 | PM |

## Cost-benefit estimate

On the working assumptions below, Handoff pays back its build cost in about 13 weeks and returns roughly €5,500 of time per year.

| Item | Assumption | Value |
| --- | --- | --- |
| Recurring meetings recapped | 15 per week | – |
| Time saved per recap | 15 min → 3 min | 12 min |
| Time saved per week | 15 × 12 min | 3 hours |
| Time saved per year | 46 working weeks | 138 hours |
| Loaded cost of staff time | Estimate | €40 / hour |
| Annual benefit | 138 h × €40 | €5,520 |
| One-off build cost | \~40 hours × €40 | €1,600 |
| Running cost | Static page, Slack webhook is free | €0 / year |
| Payback period | €1,600 ÷ €120 per week | \~13 weeks |
| Year-1 ROI | (€5,520 − €1,600) ÷ €1,600 | \~245% |

Not counted: fewer dropped commitments and faster follow-through, which are likely the larger benefit but hard to price. All figures are to be replaced with pilot measurements in week 4.

## Approval

Signing below approves the v1 scope above and the 4-week pilot.

| Role | Name | Decision | Date |
| --- | --- | --- | --- |
| Client sponsor |  |  |  |
| Project manager | Subhan Abdullah |  |  |
| Slack workspace admin |  |  |  |
