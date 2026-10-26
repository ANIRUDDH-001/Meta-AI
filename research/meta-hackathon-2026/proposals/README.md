# Governance proposals — NOT INSTALLED

Drafts for the build repository. Nothing here is active. Each file is copied into the repo root only after the user approves it (MCQ). The research folder stays a read-only reference.

Revised 2026-10-26T17:20Z after the audit (research file 09) and the user's message-3 rules: Claude never commits or accesses GitHub; approvals by usefulness, not count; official skills pre-approved; plans detailed enough to switch agents without drift.

## Install map (on approval)

| Draft | Goes to (repo root) | Read by | Size (`wc`, 17:20Z) |
|---|---|---|---|
| `AGENTS.md` | `AGENTS.md` | Codex natively; Claude through the import in CLAUDE.md | 98 lines / 6,292 bytes (Codex cap 32 KiB) |
| `CLAUDE.md` | `CLAUDE.md` | Claude Code | 11 lines + imported AGENTS.md |
| `docs/governance/PROTOCOLS.md` | same path | Both, on demand by § | 162 lines, §1–§12 |
| `docs/ledger/*` | same paths | Both | templates: STATE, PLAN, DECISIONS, QUESTIONS, FEATURES, PROVENANCE |
| `docs/CODEMAP.md` | same path | Both, before opening source | template |
| `.claude/settings.json` + `.claude/hooks/session_start.py` | same paths | Claude Code | 49 deny / 24 ask rules; hook prints STATE.md + log tail |
| `.codex/config.toml` | same path | Codex (trusted projects only) | — |
| `TOOLING_PROPOSAL.md` | not installed | the user, for decisions | — |

## Why this shape (sources in `../sources.jsonl`)

- **AGENTS.md is the single source of rules.**
  - When both files exist, Claude Code reads only CLAUDE.md. CLAUDE.md therefore imports AGENTS.md instead of copying it, so the two never drift (S-CC-MEMORY).
  - Codex concatenates AGENTS.md from the root down to the working directory, with a 32 KiB cap (S-CODEX).
- **Short always-loaded files, detail on demand.** Imports do not reduce context cost (S-CC-MEMORY). PROTOCOLS.md is therefore read by section only when needed, not imported.
- **Enforcement lives in settings.** Must-happen rules are permission rules, because instruction files are only context (S-CC-MEMORY, S-CC-HOOKS). Deny beats allow and ask (S-CC-PERMS).
  - Claude: git commit/push/merge/rebase/tag, clone/fetch/pull, `gh`, GitHub WebFetch domains and GitHub MCP are **denied**; branch and worktree creation **ask**.
  - Known gap: rules miss full-path and `sh -c` invocations (S-CC-PERMS). The AGENTS rule still binds there.
- **No-drift handoff.** `PLAN.md` holds each approved spec verbatim, `CODEMAP.md` says where code lives, and the `STATE.md` handoff block lists uncommitted files and a proposed commit message (PROTOCOLS §12). A new chat, or a switch to Codex, starts from these, not from the chat or the codebase.
- **Ledger and feature list.** These follow Anthropic's long-running-agent harness: a progress file, a JSON feature list with `passes`, one feature at a time, and a clean state at session end (S-ANTH-HARNESS).

## What changes with each MCQ answer

- **Product (D13) is C3 or C4, not Parity:**
  - `FEATURES.json` is replaced with that product's acceptance tests; `PLAN.md` gets its kill criteria.
  - The AGPL/PyMuPDF line is revisited. The Wonder VM rule stays for C3 (it drives a browser).
- **Approval granularity (07 D5):**
  - The drafts assume *per-task spec approval plus hard gates*.
  - If *per-change* approval is chosen, AGENTS.md gains: "show each diff hunk for approval before writing", and the cadence slows.
- **Q8 (Codex commits):** if "user only" stands, the Codex sub-bullet in AGENTS.md is deleted.
- **Q9 (Claude local read-only git):** if no, the git deny list becomes one `git *` deny (TOOLING §D4).
- **Track:** Indie is confirmed (D4), so the Startup production-evidence additions are dropped.

## Checks run on these drafts (17:20Z)

- `settings.json` and `FEATURES.json` parse (`python -I` json.load). `config.toml` is unchanged since its last parse.
- The hook script prints STATE.md when `CLAUDE_PROJECT_DIR` points at this folder (re-run after this revision).
- All source IDs cited exist in `sources.jsonl` (re-run after this revision).
- **Not checked:** the hook inside a live Claude Code session; the deny rules inside a live session; Codex loading the config. All are checked at install time.
