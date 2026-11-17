# Knowledge

Three files outlast the work: the glossary (`glossary.md`), current facts (`state.md`) and decision records (`decisions/`).

**Every entry has provenance**: a closed ticket, an agreed decision, a term the user settled in conversation, or a team member's own statement of a choice the business makes. Each file starts with its first entry that has one.

## glossary.md — glossary

```md
# {Project name}

{One or two sentences: what this project is.}

## Language

**Client**:
The organisation paying for the work under a signed agreement.
_Avoid_: customer, buyer

**Engagement**:
One statement of work under that agreement.
_Avoid_: project, job
```

It is a glossary and nothing else — facts go to `state.md`, reasoning to `decisions/`.

Use the glossary's vocabulary in tickets, briefs and records. In any conversation — above all while grilling, where these writes are the record of the conversation and so happen as it goes rather than waiting for the shared understanding:

- **Challenge against the glossary.** When the user uses a term that conflicts with it, call it out immediately: "Your glossary defines X as …, but you seem to mean … — which is it?"
- **Sharpen fuzzy language.** When the user uses a vague or overloaded term, propose a precise canonical one: "You're saying 'account' — do you mean the client or the bank account? Those are different things."
- **Discuss concrete scenarios.** When the relationships between terms are being discussed, stress-test them with specific scenarios. Invent scenarios that probe edge cases and force the user to be precise about the boundaries between concepts.
- **Update inline.** When a term is resolved, update `glossary.md` right there — capture terms as they are settled, one at a time.

## state.md — current facts

```md
# State

| Fact | Current | Source | Last verified |
|---|---|---|---|
| Fiscal year end | 31 December | decisions/0003 | 2026-08-04 |
```

- Every fact carries a source and the date it was last checked against that source. The source is the ticket's number plus the document path — or, for a choice the business makes (a price, a term, a policy, who does what), the statement of the team member who made it: `<name>, stated YYYY-MM-DD`, with the name as it appears in the team list. A fact about the outside world always needs a document. When two team members' statements conflict, flag it — the user decides.
- A closing ticket writes its facts here. Change the row in place; the ticket's log keeps the history.
- `state.md` is the single source of truth for facts: where any other document in the folder disagrees, `state.md` wins.
- When a fact is added or changes, scan `decisions/` for records whose `Rests on:` line cites it or is waiting on it. Update the line to cite a newly added fact; flag to the user each record whose basis changed.

## Decision records

`decisions/NNNN-slug.md`.

```md
# {NNNN} — {Short title of the decision}

{1-3 sentences: what's the context, what did we decide, and why.}

Rests on: {facts in state.md, and sources, this depends on}
Reopen if: {the tripwire — the event that sends us back to this decision}
```

That's it. The value is in recording *that* a decision was made and *why* — not in filling out sections. Add `Superseded by: NNNN` when a later record replaces one.

**When to record one** — all three must be true:

1. **Hard to reverse** — the cost of changing your mind later is meaningful
2. **Surprising without context** — a future reader will wonder "why did they do it this way?"
3. **The result of a real trade-off** — there were genuine alternatives and you picked one for specific reasons

While grilling, offer a record the moment a decision passes all three — sparingly, and as it lands. If any one is missing, skip the record. A decision recorded outside a ticket also goes on its workstream brief's `Decisions:` line. A rejected idea that passes all three is recorded the same way — its tripwire says what would bring it back. A minor "no" needs no record; if it came from a ticket, close that ticket as `wontfix` with the reason in its log.

**Flag conflicts.** If your output contradicts an existing record, surface it explicitly rather than silently overriding:

> _Contradicts decision 0007 (no paid Substack tier) — but worth reopening because…_
