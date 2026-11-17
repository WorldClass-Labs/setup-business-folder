# setup-business-folder

A Claude Code skill that sets up a business folder so every AI session in it files work the same way: a file plan, tickets grouped by workstream with statuses and blocking edges, a glossary, a table of current facts with sources, and a decision log.

Adapted from the setup skill in [mattpocock/skills](https://github.com/mattpocock/skills) (MIT).

## Install

Clone this repo into your Claude skills folder:

```bash
git clone https://github.com/WorldClass-Labs/setup-business-folder.git ~/.claude/skills/setup-business-folder
```

Then, in Claude Code, open the folder you want to set up and run `/setup-business-folder`. It runs only when you call it.

## What it writes

- `AGENTS.md` — a short block pointing to the rules (`CLAUDE.md` just imports it)
- `how-this-folder-works/folder-layout.md` — where every kind of item goes and how it is named
- `how-this-folder-works/tickets.md` — workstreams, tickets, statuses, triage and the filing check
- `how-this-folder-works/knowledge.md` — glossary, current facts and decision records

Everything else is created only when its first real item arrives.
