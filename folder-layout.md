# Folder layout

This folder's file plan: where every kind of item goes. Read it before creating, moving or naming any file. Create a folder only where the file plan puts it, and only when its first real item arrives.

## The file plan

```
AGENTS.md                             ← pointers to these rules — the source of truth
CLAUDE.md                             ← one line, @AGENTS.md
glossary.md                           ← glossary
state.md                              ← current facts
how-this-folder-works/                ← rules for how this folder works
decisions/NNNN-slug.md                ← decision records, project-wide
finished-records/<type>/              ← signed, filed, final and received documents
work/<workstream>/brief.md            ← one workstream per piece of work
work/<workstream>/tickets/NN-slug.md
work/<workstream>/<working files>     ← drafts, research notes, analysis
work/unsorted/tickets/NN-slug.md
```

Everything at the top level outlasts the work. `work/` holds the work in progress, and a workstream stays where it is after its last ticket closes.

## What goes where

| Item | Path | Name |
|---|---|---|
| Term and its meaning | `glossary.md` | — |
| Current fact | `state.md` | — |
| Decision, including a rejected idea | `decisions/` | `NNNN-slug.md` |
| Workstream brief | `work/<workstream>/` | `brief.md` (`map.md` for a `/wayfinder` workstream) |
| Ticket | `work/<workstream>/tickets/` | `NN-slug.md` |
| New item not yet sorted | `work/unsorted/tickets/` | `NN-slug.md` |
| Working file, including a document received but not yet through the filing check | `work/<workstream>/` | `slug.ext` |
| Finished document | `finished-records/<type>/` | `YYYY-MM-DD-<party>-<document>.ext`, dated by the document's own date — signed, issued or filed |

`<type>` is a plain category, such as `contracts` or `filings`. The subfolders already in `finished-records/` are the list of types: file into one that fits. A new type is agreed with the user when a ticket's `Result goes to:` line first names it; that line is its record until the first document arrives.

## Naming

- Dates in file names, status lines and table cells are `YYYY-MM-DD`, so they sort. Prose and logs follow any standing instruction on date format.

- Lowercase words joined by hyphens, for every folder and file. `AGENTS.md` and `CLAUDE.md` keep the capitals other tools look for.
- Workstream names are permanent, and so are ticket and decision numbers. A retired ticket or decision keeps its number, and the next one takes the next number.
- Numbering: ticket numbers are unique across the whole folder — scan every `work/*/tickets/` directory for the highest number and increment by one. Decision numbers are scanned the same way across `decisions/`.

## When an item fits no row

Stop and ask the user where it belongs. Add the agreed row to the table above first, then file the item.

## Other skills' names for these

Some reused skills name their own paths. This translation overrides them, and is repeated in `AGENTS.md` so every session has it:

- `CONTEXT.md` → `glossary.md`
- "ADR", or `docs/adr/` → a decision record in `decisions/`, numbered on from the highest there, in the format and under the three tests of `how-this-folder-works/knowledge.md`
- "issue", "spec" or "PRD" → a ticket, or a workstream's brief, per `how-this-folder-works/tickets.md`
- `.scratch/<feature>/` → `work/<workstream>/`

## Wayfinding operations

Used by `/wayfinder`. A wayfinder effort is a workstream whose `map.md` stands in for `brief.md`.

- **Map**: `work/<workstream>/map.md` — the Destination / Notes / Decisions so far / Not yet specified / Out of scope body.
- **Child ticket**: `work/<workstream>/tickets/NN-slug.md`, with the question in the body and a `Type:` line (`research` / `prototype` / `grilling` / `task`). Otherwise the ticket rules apply as written.
- **Blocking**: the ticket's `Blocked by:` line, in ticket numbers. A ticket is unblocked when every ticket it lists is `done`.
- **Frontier**: scan `work/<workstream>/tickets/` for tickets that are open and unblocked; first by number wins.
- **Claim**: this folder has no claim status. Work one map at a time, in one session.
- **Grilling**: where `/wayfinder` calls `/grilling` with `/domain-modeling`, run `/grilling` alone and record terms and decisions per `how-this-folder-works/knowledge.md`.
- **Resolve**: append the answer under an `## Answer` heading, set `Status: done`, then append a context pointer (gist + link) to the map's Decisions so far.
