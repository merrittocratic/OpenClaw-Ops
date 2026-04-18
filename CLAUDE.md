# OpenClaw Ops

## Project Summary
Operational workspace for self-hosted OpenClaw agents running on the Mac Mini.
Home for the OpenClaw Security Checklist, the security journal, skill-vetting
notes, sanitized configs, and any other artifacts that document how agents on
the Mac Mini are configured, permissioned, and maintained.

This repo is **ops documentation and doctrine**, not application code. Agents
themselves run on the Mac Mini; the repo just tracks their configuration and
change history.

## Who You're Working With
Merrittocracy is run by a director-level data scientist and former Navy
helicopter pilot (20 years, ~4,500 hours). Aviation safety culture shapes this
project more than any other — layered defense, written checklists, and
"show your work" as a discipline, not a slogan. Preferences:
- Concise, direct responses — no fluff
- When in doubt on architecture: **ask before proceeding**
- When in doubt on implementation details: **make reasonable assumptions, note
  them, keep moving**
- If you disagree with a locked-in decision below: **flag and pause** — do not
  silently proceed or unilaterally change direction

---

## Architecture Decisions (Locked In)

### Mac Mini is the Factory Floor, Laptop is the Workshop
Always-on scheduled agent work runs on the Mac Mini via OpenClaw. Interactive
iteration, doc editing, and skill vetting happen on the laptop via Claude Code.
Git is the bridge between them — laptop pushes, Mac Mini pulls. Do NOT propose
always-on agent work on the laptop, and do NOT propose iterative doc editing
directly on the Mac Mini.

### OpenClaw Security Checklist is Operational Doctrine
`OpenClaw_Security_Checklist.docx` is the standing doctrine for any agent
configuration, credential, skill install, or permission change. Ten sections,
checkbox format. Do NOT propose alternative security frameworks or compete with
this document — amend it when it needs amending, and log the amendment to the
journal.

### Journal Entries Precede Actions
Every significant change — skill install, permission grant, credential rotation,
config change, scheduled task addition, model tier change — gets a journal entry
**before** the action is taken, not after. The log is the preflight checklist.
Entries live in `journal/` using the template. Filename pattern:
`YYYY-MM-DD_short-description.md`. Do NOT retroactively edit old journal entries
to reflect new knowledge — append a new entry that references the old one.

### Single-Operator Trust Model
One human, one gateway, one trust boundary. No multi-tenant, no shared agents,
no "run this for a friend." This is a personal-hardware, personal-brand
workspace. Do NOT propose architectures that share agent access across
identities.

### Hard Wall — Florida Blue
Nothing related to the user's day job at Florida Blue belongs in this workspace
or any agent configured from it. No employer data, credentials, VPN, networks,
tokens, or artifacts of any kind. Mac Mini runs on personal network with
personal credentials only. If a task, config, or prompt looks like it could
pull in employer context — stop and flag it.

---

## Repo Structure
```
OpenClaw-Ops/
├── CLAUDE.md                          # This file
├── OpenClaw_Security_Checklist.docx   # Operational doctrine (tracked)
├── journal/
│   ├── TEMPLATE.md                    # Entry template (tracked)
│   └── YYYY-MM-DD_*.md                # Entries (gitignore-consider, see below)
├── configs/                           # Sanitized configs only, tracked
├── skills-reviewed/                   # Notes on vetted skills/MCP servers
└── .gitignore
```

### What Goes in Git, What Doesn't
- **Tracked:** the checklist, TEMPLATE.md, sanitized configs, skill review notes,
  CLAUDE.md
- **Gitignore candidates:** journal entries containing sensitive operational
  details (tokens, hostnames, exact paths), raw configs with any secrets
- **Never tracked:** `.env` files, real credentials, any file with a secret in it

If a journal entry needs to reference sensitive values, reference them by
**name** (e.g., "rotated the X API write token") not by **value**. That keeps
the entry safe to track and preserves the audit trail.

---

## Known Issues / TODOs

1. **Mac Mini not yet delivered.** OpenClaw itself is not running. This repo is
   currently documentation-only. Do NOT build any scripts that assume the Mini
   is present.
2. **Laptop ↔ Mac Mini sync mechanism.** Planned: git as the bridge. When Mini
   arrives: clone this repo to Mini, establish pull cadence, document in a
   journal entry.
3. **Break-glass SSH path not yet established.** Checklist Section 3 calls for
   an independent SSH path to the Mini that doesn't depend on agent
   infrastructure. Configure when Mini arrives. Document the path in a journal
   entry (by description, not by credentials).
4. **No scheduled tasks yet.** The first scheduled task — likely an `openclaw
   security audit` weekly cron — becomes the first real test of the journal
   pattern.

---

## Code Style (When Code Lands Here)
This repo is primarily markdown and configs. If scripts arrive:
- Shell: `bash`, not `zsh`-specific. `set -euo pipefail` at the top.
- R: tidyverse style, base R `|>` pipe (consistent with other Merrittocracy
  repos).
- Paths via `$HOME` or `here::here()` — never hardcoded absolute paths.
- Comments explain *why*, not *what*.

---

## Do NOT
- Propose always-on agent work on the laptop (that's Mac Mini territory)
- Propose iterative doc editing on the Mac Mini (that's laptop territory)
- Retroactively edit journal entries — append new ones that reference old
- Add alternative security frameworks that compete with the Checklist
- Track real credentials, `.env` files, or any file with a secret
- Propose multi-operator or shared-agent architectures
- Build automation infrastructure that assumes the Mac Mini is present before
  it actually is
- Silently change a locked-in decision — flag and pause instead

---

## Building in Public Log
**Ask at the end of EVERY session, not just when something feels notable.**
Log lives at `/Users/stephenmerritt/content/draft/building_in_public_log.md`
(cross-repo reference — in the content repo).

Proactive prompt at natural stopping points:

> "Any candidates for the building in public log?"

Good OpenClaw-Ops candidates: the aviation-safety-to-agent-ops mental model,
layered-defense decisions, surprising failure modes discovered during setup,
the break-glass SSH story, the journal-precedes-action discipline as an
anti-pattern-prevention tool. Not routine: doc typo fixes, README tweaks.
