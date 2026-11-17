# Tickets

Work is split into **workstreams** — one folder per piece of work with its own goal — so an agent working a ticket loads one workstream and nothing else.

## Workstreams

A workstream is `work/<workstream>/`: a brief, its tickets, and its working files. Open a new workstream with its brief:

```
# <workstream name>

Goal: what is true when this workstream is finished — one or two sentences
Why now: the trigger, and the cost of delay
Out of scope: what this workstream deliberately does not cover
Sources: the documents, laws, emails this work starts from
Decisions: links to decision records this workstream produced or relies on
```

A workstream is finished when every ticket is `done` or `wontfix`. Add `Finished: YYYY-MM-DD` under the brief's title and leave the workstream where it is.

## Tickets

One file per ticket at `work/<workstream>/tickets/NN-slug.md`. **Ticket numbers are unique across the whole folder, not per workstream**: scan every `work/*/tickets/` directory for the highest existing number and increment by one. Numbers are permanent; dependency order lives on the `Blocked by:` line.

A ticket's **name is its number** — `04`, never `gst-registration/04`. Because numbers are unique across the folder, the number alone identifies a ticket, and a ticket that moves workstream keeps its number and its name. Use the bare number everywhere — `Blocked by:` lines, logs, briefs, chat. Name the workstream alongside it only as context for a reader, never as part of the identifier.

```
# <NN> — <title>

Status: <status>
Blocked by: <ticket numbers>, or "None — can start immediately"

What this delivers: the outcome, from the user's side — not a list of steps
Done when:
- [ ] checkable criterion
Result goes to: <each exact path, plus the row's Item label from how-this-folder-works/folder-layout.md, separated by semicolons — e.g. finished-records/contracts/ (Finished document); state.md (Current fact)>

## Log
```

A `needs-triage` item carries only its title line, Status, a `Raw:` line quoting the item as it arrived, and `## Log`; triage fills in the rest and keeps the `Raw:` line.

The log takes dated entries, appended to the bottom: status changes, what was done, where things were filed.

## Statuses

| Status | Meaning |
|---|---|
| `needs-triage` | Captured, not yet scoped. Lives in `work/unsorted/`. |
| `needs-info` | Can't be scoped until someone answers. The log names who, and the question. |
| `ready-for-agent` | Fully specified; Claude can finish it alone — research, drafting, analysis. |
| `ready-for-<name>` | The next move is that person's. For the team ({{TEAM}}): a decision, signature, filing, payment or call. For an outside party, named by who they are (`ready-for-harlow-ltd`): the ball is with them, and the log gives a date to chase. While the party is still unknown, finding them is the next move — the ticket is ready for the teammate or the agent doing that. |
| `done` | Finished, and passed the filing check. |
| `wontfix` | Dropped. The log gives the reason in one line. |

Every ticket carries exactly one status.

The status always names whoever makes the next move, so it changes hands as the ticket does — log each hand-off.

State transitions: a new item goes to `needs-triage` first; triage moves it to `needs-info`, a `ready-for-` status, or `wontfix`. `needs-info` returns to `needs-triage` once the answer arrives. When the next move passes to someone else — an outside party, a teammate, back to us — the status moves with it; when nothing is left to do, the ticket goes straight to the filing check. Tickets split from a plan are already scoped — they start at a `ready-for-` status. The user can override any status at any time; flag transitions that look unusual and ask before proceeding.

## Blocking and the frontier

A ticket is **blocked** while any ticket on its `Blocked by:` line is not `done`. Blocked is worked out fresh from that line each time, so it is not one of the statuses.

The **frontier** is every open ticket whose blockers are all done. "What's next" means the frontier, first by number within a workstream.

No ticket may be blocked by a ticket in `work/unsorted/` — an unscoped ticket cannot gate scoped work, so triage it first.

## Triage

Triage moves an item out of `work/unsorted/`. Read it, then recommend a workstream (existing or new) and a status, with reasoning. Wait for the user. On their yes, move the file into the workstream's `tickets/`, keeping its number and file name, and record the move in its log. A new workstream opens with its brief, written at triage.

## Splitting work into tickets

1. **Gather context.** Work from the workstream's brief and the conversation. A ticket triaged into the workstream becomes one of the split tickets, keeping its number and log.
2. **Draft.** Each ticket delivers one checkable outcome and fits a single fresh session. Create blockers first where you can, and give each its blocking edges: the tickets that must be `done` before it can start. A ticket with no blockers can start immediately.
3. **Quiz the user.** Present the breakdown as a numbered list — title, status, blocked by, what it delivers — and ask:
   - Does the granularity feel right? (too coarse / too fine)
   - Are the blocking edges correct — does each ticket only depend on tickets that genuinely gate it?
   - Should any tickets be merged or split further?

   Iterate until the user approves the breakdown.
4. **Write** one file per approved ticket.

## Closing a ticket — the filing check

Set `Status: done` only when every line holds:

- [ ] every ticket on its `Blocked by:` line is `done`
- [ ] every `Done when` box is ticked
- [ ] any decision the ticket settled is recorded first, per `how-this-folder-works/knowledge.md`
- [ ] every path on `Result goes to:` exists and matches a row in `how-this-folder-works/folder-layout.md`
- [ ] new facts are in `state.md`, per `how-this-folder-works/knowledge.md`
- [ ] every finished document the ticket produced sits in `finished-records/`, named to the pattern
- [ ] the log's closing entry lists where each item was filed

When an item fits no row in the file plan, stop and ask the user. Add the agreed row first, then file it.
