# Handoff — Product Requirements Document

Oct 26, 2026 · @Subhan Abdullah

## Overview

Handoff v1 turns a pasted meeting transcript into a reviewed list of action items and posts it to Slack in under 3 minutes.

|  |  |
| --- | --- |
| Problem | Notetakers spend about 15 minutes per meeting copying action items out of transcripts and formatting Slack recaps by hand. |
| Goal | One screen: paste, review, post. No accounts, no database, no new platform. |
| Primary user | The meeting notetaker |
| Version | 1.0 (MVP) |
| Business case | [Handoff — Business Requirements Document](https://claude.ai/artifact/7uEWDV3RLPbFc6aaqybw8L) |
| Working prototype | [Handoff tool](https://claude.ai/artifact/RM2hkJaMhLTeXoYfqdyPPe) |

**Product principle:** the tool drafts, the person decides. Nothing is posted without a human review, so extraction can be fast and simple rather than perfect.

## Personas

Two people matter in v1: the one who sends the recap and the ones who receive it.

| Persona | Who they are | Needs | Frustration today |
| --- | --- | --- | --- |
| **Nadia, the notetaker** | Operations coordinator; runs notes for 6–10 meetings a week | Get a correct recap out fast; avoid chasing people later | Rereads every transcript; misses items said in passing; formats by hand |
| **Omar, the action owner** | Team member who attends the meeting | See his tasks and dates at a glance in Slack | Recaps arrive late, in a different format each time, sometimes without his item |

## User stories and acceptance criteria

Six stories cover v1. Acceptance criteria use Given / When / Then.

| ID | User story | Acceptance criteria | Priority |
| --- | --- | --- | --- |
| US-1 | As a notetaker, I want to paste a transcript so I don't have to retype anything. | Given a transcript with "Name: text" lines (timestamps optional), when I paste it and choose Find action items, then the tool reads every line and shows the line and speaker count. | Must |
| US-2 | As a notetaker, I want action items found with owners and due dates so I only check, not search. | Given commitments ("I'll…"), requests ("Dev, can you…"), assignments ("Lena will…") and "Action item:" lines, then each becomes an item with task, owner and due date if one was said. | Must |
| US-3 | As a notetaker, I want to fix the list quickly so the recap is right. | When I edit a task, change an owner, set a due date, untick, delete or add an item, then the Slack preview updates immediately. | Must |
| US-4 | As a notetaker, I want to see items without an owner so nobody's task gets lost. | Given an included item has no owner, then it is outlined and the summary shows "N need owners" before I post. | Must |
| US-5 | As a notetaker, I want to post to Slack in one click so the team sees it right away. | Given a valid webhook URL and at least one item, when I choose Post to Slack, then the recap is sent to that channel and a confirmation appears. Invalid URL or no items shows a clear error. | Must |
| US-6 | As an owner, I want my tasks grouped under my name so I can find them at a glance. | Given grouping is on, then the message lists owners alphabetically with Unassigned last, each with their tasks and due dates. | Should |

## Functional requirements (MoSCoW)

Every Must is built in the prototype; Could and Won't items are deliberately held back to keep v1 lean.

| ID | Requirement | MoSCoW | Status in prototype |
| --- | --- | --- | --- |
| FR-1 | Paste transcript into a text box; load sample; clear | Must | Built |
| FR-2 | Parse "Name: text" lines with optional \[hh:mm:ss\] timestamps; join wrapped lines to the previous speaker | Must | Built |
| FR-3 | Read an "Attendees:" line and match first-name speakers to full names | Should | Built |
| FR-4 | Detect action items, owners and due dates (rules in the next section) | Must | Built |
| FR-5 | Show each item with include checkbox, editable task, owner dropdown, due date, confidence and source quote | Must | Built |
| FR-6 | Add and remove items by hand | Must | Built |
| FR-7 | Flag included items with no owner | Must | Built |
| FR-8 | Live Slack preview; meeting name, date and channel label | Must | Built |
| FR-9 | Group by owner toggle | Should | Built |
| FR-10 | Post via Slack incoming webhook with URL validation | Must | Built |
| FR-11 | Copy message to clipboard as a fallback | Must | Built |
| FR-12 | Upload .txt or .vtt transcript files | Could | Not built |
| FR-13 | AI-assisted extraction for free-form notes | Could | Not built (v1.1 candidate) |
| FR-14 | Real Slack @mentions that notify owners | Won't (v1) | Needs a Slack app and user ID mapping |
| FR-15 | Save history of past recaps | Won't (v1) | Conflicts with "no database" |

## Extraction rules

Extraction is rule-based and runs in the browser, so it is instant, free and private. Rules are checked per sentence in this order; the first match wins.

| Order | Pattern | Example | Owner | Confidence |
| --- | --- | --- | --- | --- |
| 1 | Explicit marker | "Action item: Dev to check with legal…" | Name after the marker | High |
| 2 | Request to "someone" | "Can someone fix that link?" | Unassigned until someone accepts | Low |
| 3 | Request to a named person | "Dev, can you put together a summary by Thursday?" | The named person | High |
| 4 | Assignment | "Lena will extend the test" | The named person | High |
| 5 | Commitment | "I'll pause the broad-match keywords today" | The speaker | High |
| 6 | Open need | "We still need someone to draft the newsletter" | Unassigned until someone accepts | Low |

**Follow-up handling.** When the next speaker accepts an open item ("I can take that", "Yep, on it"), the item is assigned to them with medium confidence. When the owner confirms their own item ("I'll have it by Thursday"), it is merged, not duplicated, and any new due date is added.

**Due dates** recognised: today, tomorrow, EOD/EOW, this/next week, weekdays ("next Monday"), and dates like "Oct 30" or "30/10". The date phrase is removed from the task text.

**Cleaning.** Fillers such as "also", "just", "please" and trailing reasons ("so that…", "because…") are removed so tasks start with a verb.

**Measured on the sample meeting:** 8 of 8 action items found with the correct owner; 1 task ("Fix that link") needs a clearer wording during review, which is what the review step is for.

## Screens and UX

Handoff is one screen with three numbered steps visible at once, so the notetaker never navigates. See the [working prototype](https://claude.ai/artifact/RM2hkJaMhLTeXoYfqdyPPe).

1. **Paste the transcript** (left panel): large monospace text box, Load sample, Clear, and Find action items. A line under the button reports lines read, speakers and items found.
2. **Review action items** (right panel): one card per item with an include checkbox, editable task, owner dropdown (speakers + Unassigned), due date, confidence label and a collapsible quote from the transcript. A summary row shows "6 of 8 selected" and "1 needs an owner" in amber. + Add item opens a blank card.
3. **Post the recap to Slack** (full-width panel): meeting name, date, channel label, group-by-owner toggle and webhook URL on the left; a live message preview on the right; Post to Slack and Copy message buttons with a status line.

**UX rules**

- The screen opens with a realistic sample already processed, so a first-time user sees the result before pasting anything.
- Every edit updates the preview instantly; there is no Save button.
- Errors say what to do: "Add a Slack webhook URL that starts with https://hooks.slack.com/".
- Works at phone width; panels stack into one column below 920 px.
- Light and dark themes follow the system setting.

## Slack message specification

The recap is plain Slack mrkdwn sent as one message, so it renders in every Slack client and can be copied anywhere.

**Structure:** bold title with meeting name and date → item and owner count → one block per owner (bold name, then bullets with task and italic due date) → Unassigned last → a closing line asking owners to reply in thread.

**Payload:** `POST` to the incoming webhook URL, body `payload={"text": "<message>", "mrkdwn": true}` form-encoded.

**Example** (from the sample meeting, grouped by owner):

```markdown
*Action items: Weekly Growth Sync* (Mon 26 Oct)
8 items · 4 owners

*Dev Patel*
• Put together a one-page summary of the campaign results _(due Thursday)_
• Check with legal whether we can use the customer quotes in email three

*Lena Fischer*
• Extend the test for another two weeks
• Share the interim numbers in the channel _(due Friday)_
• Fix the welcome email link to the new help center

*Maria Chen*
• Send the recap after this call

*Sam Okafor*
• Pause the broad-match keywords and move that budget to the retargeting set _(due Today)_
• Draft the November newsletter _(due Next Monday)_

_Reply in thread if anything is missing or wrong._
```

## Non-functional requirements

| ID | Area | Requirement | Target |
| --- | --- | --- | --- |
| NFR-1 | Speed | Extraction of a 60-minute transcript | < 1 second in the browser |
| NFR-2 | Usability | First-time user posts a recap without instructions | ≤ 3 minutes |
| NFR-3 | Privacy | Transcript never leaves the browser; nothing stored | Only the final message is sent, to Slack |
| NFR-4 | Security | Webhook URL kept in the open tab only | Not saved, logged or sent elsewhere |
| NFR-5 | Simplicity | Deployment footprint | One static HTML file; no server, no database, no build step |
| NFR-6 | Accessibility | Keyboard use, labels, contrast | Every control labelled; visible focus; WCAG AA contrast in light and dark |
| NFR-7 | Compatibility | Browsers and screen sizes | Current Chrome, Edge, Firefox, Safari; 360 px and up |
| NFR-8 | Cost | Running cost | €0 |

## Architecture

Handoff is a single static HTML file: all logic runs in the browser and the only network call is one POST to Slack.

&#91;embedded content: architecture · one static page, one outbound call\]

There is no backend to host, patch or secure. The page can be opened from a file, a shared drive or any static host. The webhook call uses form-encoded `no-cors` mode, which Slack accepts from browsers; Slack does not return a delivery receipt to the page, so the status line asks the user to check the channel.

| Layer | Choice | Why |
| --- | --- | --- |
| UI | Plain HTML, CSS, JavaScript | No build step; any course reviewer can open it |
| Extraction | Rule-based parser (\~150 lines) | Instant, free, private, explainable |
| Delivery | Slack incoming webhook | Free, admin-approved, one channel per URL |
| Hosting | Any static host or local file | €0 running cost |

## Release plan

v1 ships at the end of week 1; whether anything more is built depends on a 4-week pilot measured against the BRD objectives.

&#91;embedded content: release plan · 4 phases, 2 gates (not to scale)\]

The go / no-go rule: continue to v1.1 if at least 4 of the 5 BRD objectives (O1–O5) are met. If not, fix the weakest point or stop; either outcome is a valid result of a lean pilot.

## Future versions and open questions

Anything below ships only if pilot data shows the notetaker needs it.

**Candidates for v1.1** (each must pass the scope guardrail)

- AI-assisted extraction for free-form notes without speaker names, behind an on/off switch and a privacy review.
- Upload .txt / .vtt files exported from Zoom or Teams.
- Owner-to-Slack-user mapping so names become real @mentions.
- Remember the last-used channel label and meeting name per browser.

**Open questions for the client**

- [ ] Which meeting tool produces most transcripts, and can we get 5 real (anonymised) samples?
- [ ] One channel per meeting, or one shared #action-items channel?
- [ ] Is sending meeting content to an AI service acceptable for v1.1, or must it stay on-device?
- [ ] Who in the client team is the Slack admin who will create the webhook?
