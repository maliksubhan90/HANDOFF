# Handoff

Handoff turns meeting transcripts into reviewed action items and posts them to Slack. The brand is a working tool's brand: calm navy for structure, one warm amber for the moment something is handed on, and nothing that slows the user down.

## Brand idea

**A recap, approved and passed on.** The mark is a speech bubble (the meeting) carrying a check that turns into an arrow (approved, then sent). Every visual choice serves the same job as the product: make the next step obvious.

Personality: clear, quick, dependable. Not playful, not corporate.

## Logo

| File | Use |
| --- | --- |
| `handoff-logo-horizontal.svg` | Default lockup on light backgrounds: docs, slides, README headers |
| `handoff-logo-horizontal-reverse.svg` | Lockup on navy or dark backgrounds |
| `handoff-mark.svg` | App icon, favicon, Slack app avatar, social avatar |
| `handoff-mark-flat.svg` | The bubble alone, where a square would crowd the layout |
| `handoff-mark-mono.svg` | One-colour print, stamps, embossing |
| `handoff-wordmark.svg` | Text-only placements next to other logos |

**Rules**

- Clear space around the logo: at least the height of the bubble's tail (one quarter of the mark's height) on every side.
- Minimum size: mark 16 px; horizontal lockup 96 px wide.
- The wordmark is always lowercase "handoff" and drawn as artwork. In running text, write the name as **Handoff**.
- Don't recolour the bubble, rotate the mark, add shadows or gradients, or set the wordmark in another typeface.
- On photos, place the mark (with its navy square), never the bare wordmark.

## Colour

Two fixed brand colours, used in the logo in every theme:

- **Brand ink** `brand-ink` #16202E: the logo square and the app's text colour in light mode.
- **Brand amber** `brand-amber` #E8920C: the bubble and the one primary action on any screen.

UI colours come in light and dark pairs (`bg`, `surface`, `soft`, `line`, `ink`, `muted`, `accent`). Status colours (`ok`, `warn`, `danger`) only describe state and are never decoration.

**Rules**

- One amber element per view: the primary button. Amber is a fill, never text on light grounds (2.6:1). Text on amber uses `accent-ink`.
- Items that need attention get a `warn` border and a `warn-bg` pill, not red. Red (`danger`) is only for errors.
- Neutrals lean slightly blue toward the navy; never pure grey.

## Typography

| Role | Face | Where |
| --- | --- | --- |
| Display | Bricolage Grotesque 600–700 | Step headings, product name, slide titles |
| Body | IBM Plex Sans 400–600 | Everything users read and type |
| Mono | IBM Plex Mono 400–500 | Transcripts, quotes from the transcript, raw Slack text, labels |

All three are free on Google Fonts. Display is for short headings only; never set paragraphs in it. Headings use sentence case.

## Layout

- Panels on a quiet `bg`, `radius-lg` corners, 1px `line` border, no shadows.
- Spacing steps of 4: `space-2` (8) inside rows, `space-4` (16) inside panels and as the minimum page gutter, `space-5` (20) between panels.
- Numbered step badges (1, 2, 3) only where the order is real: paste, review, post.

## Iconography

Handoff uses almost no icons. Where one is needed, draw it as a 2px rounded stroke in `ink` or `muted`, matching the check-arrow in the mark. No emoji in the product UI.

## Voice and writing

Write the way a good operations colleague talks: short, specific, active.

| Do | Don't |
| --- | --- |
| Find action items | Analyze transcript with AI |
| 1 needs an owner | Warning: incomplete data detected |
| Sent to Slack. Check #growth-team to confirm. | Success! 🎉 |
| Add a Slack webhook URL that starts with https://hooks.slack.com/ | Invalid input |

- Buttons say exactly what happens: **Post to Slack**, **Copy message**.
- Tasks in the recap start with a verb: "Draft the November newsletter".
- Dates are written as people say them: "Thursday", "Next Monday", "Oct 30".

## The Slack recap

The recap is the product's most-seen surface, so it follows the brand voice too: bold title with the meeting name and date, a count line, owners in bold with their tasks under them, due dates in italics, Unassigned last, and one closing line inviting corrections in thread.
