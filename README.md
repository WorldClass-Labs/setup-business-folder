# setup-business-folder

A Claude Code skill that sets up a business folder so every AI session in it files work the same way: a file plan, tickets grouped by workstream with statuses and blocking edges, a glossary, a table of current facts with sources, and a decision log.

## Credit

This skill is built on [Matt Pocock's skills](https://github.com/mattpocock/skills) (MIT licence — his copyright notice is kept in [LICENSE](LICENSE)). It draws on five of them:

| Matt's skill | What this skill takes from it |
|---|---|
| [setup-matt-pocock-skills](https://github.com/mattpocock/skills/tree/main/skills/engineering/setup-matt-pocock-skills) | The setup flow: explore, present findings and ask, confirm, write, done |
| [domain-modeling](https://github.com/mattpocock/skills/tree/main/skills/engineering/domain-modeling) | The glossary format, challenging and sharpening terms as you talk, and decision records with the three tests for when to write one |
| [to-tickets](https://github.com/mattpocock/skills/tree/main/skills/engineering/to-tickets) | Splitting a plan into tickets with blocking edges, and quizzing the user on the breakdown |
| [triage](https://github.com/mattpocock/skills/tree/main/skills/engineering/triage) | The status vocabulary: `needs-triage`, `needs-info`, `ready-for-agent`, `wontfix` |
| [wayfinder](https://github.com/mattpocock/skills/tree/main/skills/engineering/wayfinder) | The map for an effort too big for one session, and the frontier of unblocked tickets |

### What was changed

Matt's skills are written for software repos and an issue tracker such as GitHub. This skill adapts them for a business folder of documents:

- Tickets are plain files in the folder, grouped into workstreams, each with a short brief, instead of issues on a tracker.
- `ready-for-human` becomes `ready-for-<name>`: a named teammate, or an outside party such as a supplier, so the status always says whose move it is.
- His file names are redirected to this folder's: `GLOSSARY.md` (or the older `CONTEXT.md`) → `glossary.md`, `docs/adr/` → `decisions/`, `.scratch/` → `work/`.

### What was added

- **A file plan** (`folder-layout.md`) — where every kind of item goes and how it is named.
- **Current facts** (`state.md`) — a table of facts, each with its source and the date it was last checked.
- **Finished records** (`finished-records/`) — signed, filed and final documents, named by date and party.
- **The filing check** — the list a ticket must pass before it can close.

## Before you start

You need:

- **Claude Code**, or another AI coding agent that can run skills, on a paid plan that includes it.
- **Matt Pocock's skills**, installed as below. This skill sets up the folder; his skills (`/grilling`, `/research`, `/handoff`, `/wayfinder` and others) do much of the work inside it.

## Install

Claude Code can install both for you. Paste this into Claude Code:

> Install Matt Pocock's skills by running `claude plugin install mattpocock-skills@claude-plugins-official`. Then install the skill at https://github.com/WorldClass-Labs/setup-business-folder into `~/.claude/skills/setup-business-folder`.

Claude asks your permission before it downloads anything — allow it. Then start a new Claude Code session in the folder you want to set up and run `/setup-business-folder`. It runs only when you call it.

### Installing by hand

1. Install Matt Pocock's skills. In Claude Code, his README gives:

   ```bash
   claude plugin install mattpocock-skills@claude-plugins-official
   ```

   For other agents, follow [the install steps in his README](https://github.com/mattpocock/skills#installation-30-second-setup).

2. Copy this repo into your Claude skills folder. With git:

   ```bash
   git clone https://github.com/WorldClass-Labs/setup-business-folder.git ~/.claude/skills/setup-business-folder
   ```

   Without git, click **Code → Download ZIP** on this page, unzip it, and move the folder (it unzips as `setup-business-folder-main`) to `~/.claude/skills/setup-business-folder`.

## What it writes

- `AGENTS.md` — a short block pointing to the rules (`CLAUDE.md` just imports it)
- `how-this-folder-works/folder-layout.md` — where every kind of item goes and how it is named
- `how-this-folder-works/tickets.md` — workstreams, tickets, statuses, triage and the filing check
- `how-this-folder-works/knowledge.md` — glossary, current facts and decision records

Everything else is created only when its first real item arrives.
