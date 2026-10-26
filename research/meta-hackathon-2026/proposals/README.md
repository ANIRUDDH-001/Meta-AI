# Governance proposals — NOT INSTALLED

Drafts for the build repository. Nothing here is active. Each file is copied into the repo root only after the user approves it (MCQ). The research folder stays a read-only reference.

## Install map (on approval)

| Draft | Goes to (repo root) | Read by | Size |
|---|---|---|---|
| `AGENTS.md` | `AGENTS.md` | Codex natively; Claude through the import in CLAUDE.md | 89 lines / 4.8 KB (Codex cap 32 KiB) |
| `CLAUDE.md` | `CLAUDE.md` | Claude Code | 10 lines + imported AGENTS.md |
| `docs/governance/PROTOCOLS.md` | same path | Both, on demand | 111 lines |
| `docs/ledger/*` | same paths | Both | templates |
| `.claude/settings.json` + `.claude/hooks/session_start.py` | same paths | Claude Code | hook tested locally against these templates |
| `.codex/config.toml` | same path | Codex (trusted projects only) | — |
| `TOOLING_PROPOSAL.md` | not installed | the user, for decisions | — |

## Why this shape (sources in `../sources.jsonl`)

- **AGENTS.md is the single source of rules.**
  - When both files exist, Claude Code reads only CLAUDE.md. CLAUDE.md therefore imports AGENTS.md instead of copying it, so the two never drift (S-CC-MEMORY).
  - Codex concatenates AGENTS.md from the root down to the working directory, with a 32 KiB cap (S-CODEX).
- **Short always-loaded files, detail on demand.** Imports do not reduce context cost (S-CC-MEMORY). PROTOCOLS.md is therefore read by section only when needed, not imported.
- **Enforcement lives in settings.** Must-happen rules are permission rules, because instruction files are only context (S-CC-MEMORY, S-CC-HOOKS).
- **Ledger and feature list.** These follow Anthropic's long-running-agent harness: a progress file, a JSON feature list with `passes`, one feature at a time, and a clean state at session end (S-ANTH-HARNESS).

## What changes with each MCQ answer

- **Product is not Parity:**
  - `FEATURES.json` is replaced with that product's acceptance tests.
  - The AGENTS.md Wonder line and the AGPL line are revisited.
  - Nothing else changes.
- **Approval granularity:**
  - The drafts assume *per-task spec approval plus hard gates*.
  - If *per-change* approval is chosen, AGENTS.md gains: "show each diff hunk for approval before writing", and the cadence slows (see the MCQ).
- **Track = Startup:** PROTOCOLS §7 adds production-evidence items (hosted URL, uptime, tests shown).

## Checks run on these drafts

- `settings.json`, `FEATURES.json` and `config.toml` parse.
- The hook script prints STATE.md when `CLAUDE_PROJECT_DIR` points at this folder.
- All source IDs cited exist in `sources.jsonl`.
- **Not checked:** the hook running inside a live Claude Code session; Codex loading the config. Both are checked at install time.
