# Governance proposals — NOT INSTALLED

Drafts for the build repository. Nothing here is active. Each file is copied into the repo root only after the user approves it (MCQ). The research folder stays a read-only reference.

Revised 2026-10-26T17:20Z after the audit (research file 09) and the user's message-3 rules: Claude never commits or accesses GitHub; approvals by usefulness, not count; official skills pre-approved; plans detailed enough to switch agents without drift.

Revised again 2026-10-26T18:36Z after the red team (research files 11 and 12) and the user's answers: Codex may commit when told (D14); Claude may run local read-only git (D15); the Security Guidance plugin is installed at local scope (D16).

Revised again 2026-10-26T18:51Z after the user's MCQ answers: AGENTS line 9 reworded (D19: Codex commits when told; push, merge, tag, release and deploy are the user's only); Claude may read public GitHub pages through WebFetch (D20).

## Install map (on approval)

| Draft | Goes to (repo root) | Read by | Size (`wc`, 18:36Z) |
|---|---|---|---|
| `AGENTS.md` | `AGENTS.md` | Codex natively; Claude through the import in CLAUDE.md | 97 lines / 6,651 bytes at 18:51Z (Codex cap 32 KiB) |
| `CLAUDE.md` | `CLAUDE.md` | Claude Code | 13 lines + imported AGENTS.md |
| `docs/governance/PROTOCOLS.md` | same path | Both, on demand by § | 166 lines, §1–§12 |
| `docs/ledger/*` | same paths | Both | templates: STATE, PLAN, DECISIONS, QUESTIONS, FEATURES, PROVENANCE |
| `docs/CODEMAP.md` | same path | Both, before opening source | template |
| `.claude/settings.json` + `.claude/hooks/session_start.py` | same paths | Claude Code | 94 deny / 31 ask rules at 18:51Z (Bash and PowerShell mirrored); hook prints STATE.md + the last 20 log lines |
| `.codex/config.toml` | same path | Codex (trusted projects only) | — |
| `.gitignore` | `.gitignore` | git | `.env`, `.env.*`, local settings, caches. **The repo has none today** (12 §2) |
| `.gitattributes` | `.gitattributes` | git | `merge=union` for LOG and COSTS (12 RT39) |
| `TOOLING_PROPOSAL.md` | not installed | the user, for decisions | — |

## Why this shape (sources in `../sources.jsonl`)

- **AGENTS.md is the single source of rules.**
  - When both files exist, Claude Code reads only CLAUDE.md. CLAUDE.md therefore imports AGENTS.md instead of copying it, so the two never drift (S-CC-MEMORY).
  - Codex concatenates AGENTS.md from the root down to the working directory, with a 32 KiB cap (S-CODEX).
- **Short always-loaded files, detail on demand.** Imports do not reduce context cost (S-CC-MEMORY). PROTOCOLS.md is therefore read by section only when needed, not imported.
- **Enforcement lives in settings.** Must-happen rules are permission rules, because instruction files are only context (S-CC-MEMORY, S-CC-HOOKS). Deny beats allow and ask (S-CC-PERMS).
  - Claude: git writes (commit, push, merge, rebase, tag, reset, revert, cherry-pick, am, clean, restore, rm, config and others), clone/fetch/pull, `gh`, GitHub installs, GitHub WebFetch domains and GitHub MCP are **denied**. Branch and worktree creation, and edits to PLAN, FEATURES and DECISIONS, **ask**.
  - Local read-only git stays allowed (D15). A blanket `git *` deny would block it, because deny beats allow.
  - Known gaps: rules miss full-path and `sh -c` invocations (S-CC-PERMS), and the sandbox does not run on native Windows (S-CC-SANDBOX). A PreToolUse hook that allows only read-only git is drafted at install, with tests. The AGENTS rule still binds meanwhile.
- **No-drift handoff.** `PLAN.md` holds each approved spec verbatim, `CODEMAP.md` says where code lives, and the `STATE.md` handoff block lists uncommitted files and a proposed commit message (PROTOCOLS §12). A new chat, or a switch to Codex, starts from these, not from the chat or the codebase.
- **Ledger and feature list.** These follow Anthropic's long-running-agent harness: a progress file, a JSON feature list with `passes`, one feature at a time, and a clean state at session end (S-ANTH-HARNESS).

## What changes with each MCQ answer

- **Product (D13) is C3 or C4, not Parity:**
  - `FEATURES.json` is replaced with that product's acceptance tests; `PLAN.md` gets its kill criteria.
  - The AGPL/PyMuPDF line is revisited. The Wonder VM rule stays for C3 (it drives a browser).
- **Approval granularity (07 D5):**
  - The drafts assume *per-task spec approval plus hard gates*.
  - If *per-change* approval is chosen, AGENTS.md gains: "show each diff hunk for approval before writing", and the cadence slows.
- **Q8 and Q9 are answered** (D14, D15).
- **Q11 is answered (D19):** AGENTS line 9 now says Codex commits when told; push, merge, tag, release and deploy are the user's only. The earlier wording is kept verbatim in LEDGER D19.
- **Q12 is answered (D20):** the WebFetch GitHub denies are narrowed to `api.github.com`, `uploads.github.com` and `*.github.io`. Shell fetches of GitHub, `gh` and the GitHub MCP stay denied.
- **Track:** Indie is confirmed (D4), so the Startup production-evidence additions are dropped.

## Checks run on these drafts (18:36Z; settings re-checked 18:51:40Z)

- 18:51:40Z, after D20: `settings.json` parses; 94 deny / 31 ask / 0 allow; 0 duplicates.

- `settings.json` and `FEATURES.json` parse (`python -I` json.load); 0 duplicate rules. `config.toml` is unchanged since its last parse.
- The hook script prints STATE.md when `CLAUDE_PROJECT_DIR` points at this folder.
- All source IDs cited in the drafts exist in `sources.jsonl` (`python -I` scan: none missing).
- **Not checked:** the hook inside a live Claude Code session; the deny rules inside a live session; Codex loading the config. All are checked at install time.
