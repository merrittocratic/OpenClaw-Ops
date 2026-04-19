# OpenClaw Ops

Operational documentation for self-hosted OpenClaw agents running on the Mac Mini.

This is a documentation and doctrine repo, not application code. Agents 
themselves run on the Mac Mini; this repo tracks configuration, change 
history, and the standing operational rules.

## Entry Points

- **`OpenClaw_Security_Checklist.docx`** — operational doctrine, ten-section 
  pre-launch checklist
- **`CLAUDE.md`** — agent and Claude Code context when editing this repo
- **`journal/`** — change history, journal-precedes-action discipline
- **`journal/TEMPLATE.md`** — template for new entries
- **`configs/`** — sanitized agent and infrastructure configs *(tracked, no secrets)*
- **`skills-reviewed/`** — notes on vetted skills and MCP servers

## Secrets Management

Secrets never touch this repo. All credentials live in 1Password and are
injected at runtime via the 1Password CLI:

```bash
op run --env-file=.env.template -- your-command-here
```

Each pipeline repo owns its own `.env.template` — a mapping of environment
variable names to `op://` vault references. No actual values, safe to track.

- `autopilot/.env.template` — secrets for the Substack → X distribution pipeline

To add a new secret:
1. Add the credential to 1Password as an API Credential item
2. Add the `op://` reference line to `.env.template` in the relevant pipeline repo
3. Push — Mac Mini picks it up on next pull

`.env.template` (per pipeline) is the canonical list of what secrets that
pipeline needs. 1Password is the canonical store of their values.

## Mac Mini Setup Sequence

*Mac Mini not yet delivered. This section is a stub — flesh out and convert 
to a journal entry when setup begins.*

High-level sequence when Mini arrives:
1. Create dedicated OS user for OpenClaw (never primary account)
2. Install Homebrew, Node, OpenClaw
3. Install 1Password CLI, authenticate, verify `op vault list`
4. Clone this repo and each pipeline repo (e.g. `autopilot`)
5. Run `op run --env-file=.env.template` in each pipeline repo to verify secret injection
6. Establish break-glass SSH path (document in journal by description, not credentials)
7. Run `openclaw security audit --deep`
8. First scheduled task: weekly `openclaw security audit` cron

## Conventions

- Private repo. Personal hardware, personal credentials only.
- No employer context, credentials, or data anywhere in this workspace.
- Journal entries reference sensitive values by **name**, not by **value**.
- Journal entry precedes every significant action — skill install, permission 
  grant, credential rotation, config change.
- Laptop is the workshop for editing this repo; Mac Mini is the factory floor 
  for running agents. Git is the bridge.