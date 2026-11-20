---
name: setup-business-folder
description: Set up a business folder — its file plan, tickets with blocking edges and statuses, glossary, current-state facts and decision log. Run once per folder.
disable-model-invocation: true
---

# Setup Business Folder

Scaffold the rules a business folder runs on:

- **File plan** — where every kind of item lives and how it is named
- **Tickets** — one file per ticket, grouped by workstream, with statuses and blocking edges
- **Knowledge** — the glossary (`glossary.md`), current facts (`state.md`) and decision records (`decisions/`)

This is a prompt-driven skill, not a deterministic script. Explore, present what you found, confirm with the user, then write.

Setup writes `AGENTS.md`, `CLAUDE.md`, the three rules files, and any unsorted tickets Section C approves. Every other file and folder is created lazily, at the path the file plan gives it, when its first real item arrives.

## Process

### 1. Explore

Look at the folder to understand its starting state. Read whatever exists; don't assume:

- `AGENTS.md` and `CLAUDE.md` — does either exist, and what is in it? Is there already a `## Business folder` section? Does `CLAUDE.md` already contain the line `@AGENTS.md`?
- `how-this-folder-works/` — does this skill's prior output already exist? If so, this is a re-run: see step 4.
- `glossary.md`, `state.md`, `decisions/`, `work/`, `finished-records/`
- Every other file and folder at the top level — these are the existing items step 2 has to place on the file plan.

**Done when** you can list every top-level item and say whether the file plan already covers it.

### 2. Present findings and ask

Summarise what's present and what's missing. Then take the sections in order — one section, one answer, then the next. Lead each with your recommended answer so the user can accept it in a word. Skip a section when exploration already settled it.

**Section A — What this project is.** One or two sentences. They open the `AGENTS.md` block. Propose a draft from what exploration found.

**Section B — The team.** The fixed list of people inside the business a ticket can be ready for — for example the user and named collaborators. Claude is always `ready-for-agent`. Record each as the single lowercase name the status will carry (`joe`, giving `ready-for-joe` — not `Joe (accountant)`), and mark which one is the user — the folder's owner, who triages and approves. A fixed list keeps one person from appearing under three spellings.

**Section C — Existing items.** Only when step 1 found files or folders beyond this skill's own. For each, propose where it sits on the file plan (see [folder-layout.md](folder-layout.md)). Moving is the user's call: list the proposed moves, and move nothing without their yes. An item that fits no row gets a new row in the "What goes where" table, agreed with the user. A loose note — a fact or a task — becomes a ticket in `work/unsorted/`, quoting the note under `Raw:` — triage and closing then carry the fact into `state.md` with its provenance. Remove the original note only with the user's yes.

If `CLAUDE.md` already holds instructions of its own, propose moving them into `AGENTS.md`, under a `## Standing instructions` heading above the `## Business folder` block.

### 3. Confirm

Show the user a draft of:

- the `## Business folder` block for `AGENTS.md`:

  ```markdown
  ## Business folder

  {Section A}

  Before acting, read the rules file for what you are about to do:

  - **Creating, moving or naming any file** → `how-this-folder-works/folder-layout.md`. It is the file plan; file only where it says.
  - **Opening, triaging, splitting, working or closing a ticket** → `how-this-folder-works/tickets.md`.
  - **Adding a term, a fact or a decision** → `how-this-folder-works/knowledge.md`.

  Read `state.md` before answering anything fact-dependent. When grilling, apply `how-this-folder-works/knowledge.md` as you go.

  These paths override any skill's own: `GLOSSARY.md` or the older `CONTEXT.md` → `glossary.md`; an ADR or `docs/adr/` → `decisions/`, numbered on from the highest there, in the format of `how-this-folder-works/knowledge.md`; `.scratch/<feature>/` → `work/<workstream>/`.
  ```

- `how-this-folder-works/folder-layout.md`, `how-this-folder-works/tickets.md`, `how-this-folder-works/knowledge.md` (templates: [folder-layout.md](folder-layout.md), [tickets.md](tickets.md), [knowledge.md](knowledge.md)), with `{{TEAM}}` in `tickets.md` filled in from Section B as a comma-separated list, the user's name first and marked `— the user`

Let them edit before writing.

### 4. Write

`AGENTS.md` is the source of truth; `CLAUDE.md` only imports it.

- Write the block into `AGENTS.md`, creating the file if needed. If a `## Business folder` block already exists, update its contents in place rather than appending a duplicate. Leave the surrounding sections exactly as the user wrote them.
- Make sure `CLAUDE.md` contains the line `@AGENTS.md`, creating the file if needed. Move any other content of `CLAUDE.md` into `AGENTS.md` only if the user approved it in step 2.
- Write the three rules files to `how-this-folder-works/`.
- Carry out only the moves the user approved in step 2.

On a re-run, update the block and the rules files in place and touch nothing else: tickets, records, decisions, `glossary.md` and `state.md` are the user's.

### 5. Done

Tell the user setup is complete and what now reads these files: every session started in this folder, through `CLAUDE.md` → `AGENTS.md`. Mention they can edit `how-this-folder-works/*.md` directly later — re-running this skill is only needed to restart from scratch.

Name the reused skills that fit this layout: `/grilling` or `/grill-me` to sharpen a plan, `/research` for sourced reading, `/handoff` to carry a thread into a fresh session, `/wayfinder` for an effort too big for one session.
