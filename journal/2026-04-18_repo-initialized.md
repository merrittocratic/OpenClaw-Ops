# Journal Entry — 2026-04-18

## Type
- [ ] Skill / plugin installed
- [ ] Permission granted (new folder, new connector, new credential, new scope)
- [x] Configuration change
- [ ] Credential rotation or access change
- [ ] Incident or near-miss
- [ ] Scheduled task added or modified
- [ ] Model tier change
- [ ] Other: ___

## Summary
OpenClaw-Ops repo initialized on GitHub (private) and initial documentation committed.

## Details
Created private GitHub repo `OpenClaw-Ops` and cloned to `~/OpenClaw-Ops/` on the laptop. Initial commit contains:

- `OpenClaw_Security_Checklist.docx` — ten-section operational doctrine, with Section 8 expanded to cover Opus / Sonnet / Haiku tier selection and routing patterns
- `CLAUDE.md` — agent-facing operating instructions, written in the nfl-draft-model style (locked-in architecture decisions, Do NOT list, Building in Public prompt)
- `journal/TEMPLATE.md` — journal entry template
- `journal/2026-04-18_repo-initialized.md` — this entry
- `README.md` — orientation and entry points
- `.gitignore` — macOS/editor artifacts, credentials, forward-compatible OpenClaw runtime patterns

Mac Mini M4 not yet delivered. Repo is documentation-only at this stage.

## Why
Establishes the laptop side of the eventual laptop ↔ Mac Mini git bridge, and captures the current state of operational doctrine before any real agents are configured. Also establishes the journal-precedes-action discipline at zero stakes — the first entry is about the workspace itself, not about a change to a running system.

## Verification
Repo exists on GitHub (private). Local clone at `~/OpenClaw-Ops/` is clean (`git status` shows no uncommitted changes after the initial push). All files listed above are present and tracked. No `.env` files, credentials, or employer-related content in the repo or staged.

## Rollback / Kill Switch
Delete the GitHub repo (no external dependencies at this stage). Remove the local clone. Rollback cost is effectively zero right now — this entry exists primarily to establish the journal pattern.

## Follow-ups
- [ ] Clone this repo to the Mac Mini when it arrives
- [ ] Decide pull cadence for Mac Mini-side sync (git hook, cron, or manual) and log that decision as a separate entry
- [ ] Establish break-glass SSH path to Mac Mini, log as separate entry
- [ ] First scheduled OpenClaw task (likely weekly `security audit` cron) becomes the first real state-change journal entry
