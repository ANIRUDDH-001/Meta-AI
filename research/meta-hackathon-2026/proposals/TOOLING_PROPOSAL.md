# Tooling proposal: skills, plugins, practices (UNAPPROVED)

Each item needs a yes or no. The reasons are given so that each one can be challenged.

- **Skills from official sources are pre-approved** (user, message 3: "install the required skills you need from official sources"). Agents use whichever installed skill the situation needs without being asked. AGENTS.md does not list them (a list goes stale).

## A. Skills already available in this Claude Code install (₹0, no install)

| Use? | Skill | When | Why |
|---|---|---|---|
| **Yes (rec)** | `superpowers:verification-before-completion` | Before any "done" | Enforces PROTOCOLS §5. The most common agent failure is declaring done early (S-ANTH-HARNESS). |
| **Yes (rec)** | `superpowers:test-driven-development` | Contracts, verifiers, budget guard | These are the parts where a silent bug costs credits or credibility |
| **Yes (rec)** | `superpowers:requesting-code-review` / `receiving-code-review` | Each task, before the commit MCQ | Structures the cross-tool review in PROTOCOLS §4 |
| **Yes (rec)** | `superpowers:systematic-debugging` | Any failing test or K-gate miss | Stops guess-and-patch loops |
| **Yes (rec)** | `superpowers:using-git-worktrees` | One worktree per agent | Two agents and two developers in parallel without collisions |
| **Yes (rec)** | `playwright-cli` | End-to-end checks of the review UI; AT9 replay | Anthropic found unit tests alone missed failures that browser end-to-end tests caught (S-ANTH-HARNESS) |
| **Yes (rec)** | `frontend-design` | Review UI and demo screens | The demo is 25% of the score, and the UI is on screen for about 2 minutes |
| **Yes (rec)** | `security-review` | Day 6 and before submission | A public repo, API keys, and computer use |
| Optional | `grilling` | Storyboard and pitch, Day 4 | Stress-tests the 3-minute story before recording |
| Optional | `dataviz` | Cost and accuracy charts in the demo | Consistent, honest charts |
| **No (rec)** | `openspec-*` | — | Duplicates the spec → FEATURES.json flow. Two planning systems would cost tokens and cause drift. |
| **Used** | `superpowers:brainstorming` | Product or scope pivots only | Used for the pivot brainstorm (research file 10). Use again only when a gate fails or the user reopens scope. |

## B. Connections that need the user (₹0)

| Item | State | Action |
|---|---|---|
| context7 docs MCP | Needs OAuth | The user runs `/mcp` in an interactive `claude` terminal. A second docs server already works in this session. |
| GitHub MCP (`plugin:github:github`) | Failed to connect: authorization header badly formatted | **Claude: denied** (`mcp__github__*`, `mcp__plugin_github_github__*` in settings; verify the tool names at install). Recommend the user disables the plugin for Claude sessions. The user or Codex uses `gh`. |

## C. Free OSS to add at scaffold time (each is a dependency approval)

| Tool | Purpose | Why |
|---|---|---|
| `gitleaks` pre-commit | Secret scan on every commit | A public repo is required (F5), and a leaked key is the highest-impact risk (file 07) |
| `pytest` + `ruff` | Tests and lint, file-scoped | Fast commands for each file keep token use low |
| veraPDF (Docker) | PDF/UA conformance gate | Required for any conformance claim (F30) |
| pikepdf, pypdfium2 | PDF read/write | MPL-2.0 / Apache-2.0-compatible. No AGPL (D9). |

## D. Practices (already in the drafts; listed here for approval)

1. **JSON feature list with `passes`.** Agents only flip the flag (S-ANTH-HARNESS).
2. **STATE.md handoff and clear between tasks.** Carries context across sessions without re-reading history (S-ANTH-HARNESS, S-CC-BP).
3. **Cross-tool writer/reviewer.** Claude writes and Codex reviews, or the reverse.
   - The benefit of different model blind spots is INFERENCE, not measured.
   - Claude Code's docs recommend a fresh-context reviewer (S-CC-BP).
4. **Hard gates as permission rules, not prose.** Instruction files are context, not enforcement (S-CC-MEMORY), and hooks are not hard enforcement (S-CC-HOOKS). That is why `.claude/settings.json` uses `deny` / `ask` rules.
   - **Limit:** a `Read(.env)` deny covers built-in file tools, not a shell `cat`. Keeping keys out of the shell environment is the real protection.
   - **Limit:** Bash and PowerShell rules match the command text after compound commands are split. They miss the same program called by full path or inside `sh -c` (S-CC-PERMS). The drafts add `git -C *` variants; the AGENTS rule still binds where a pattern misses.
   - **Choice for Q9:** if Claude gets no local git at all, replace the git deny list with one `Bash(git *)` / `PowerShell(git *)` deny. That is simpler and closes the `-C` and `-c` gaps.
5. **Pre-registered thresholds** (file 06). A failed gate triggers its stated action. It is never renegotiated.
6. **Rough-cut demo recorded by Day 6.** A fallback always exists (S-HACK-TIPS).
7. **`/doctor prompt-audit`** after each governance change. It checks the instruction files for stale paths and contradictions (S-CC-MEMORY; needs v2.1.283+).

## E. Not proposed, with reasons

- **A Stop hook that runs the full test suite.** It is slow, can loop, and spends tokens on every turn. The definition of done already requires verification.
- **A PostToolUse hook that logs every tool call.** It produces a noisy trail nobody reads. Agent-written milestone lines are cheaper and more useful.
- **Codex `notify`.** It cannot be set per project (S-CODEX-CONFIG), and it is a personal preference.

## F. Plugin directory search (2026-10-26 17:21 UTC by `date -u`; SearchPlugins, official sources only)

| Use? | Plugin | Source | Why |
|---|---|---|---|
| **Yes, at scaffold (rec)** | Security Guidance | Anthropic tier; `anthropics/claude-plugins-official` `plugins/security-guidance` | Warns on edits and reviews diffs for injection, SSRF and hard-coded secrets. Our highest-impact risk is a leaked key (07). **Cost:** its Stop hook runs a model diff review each turn, which uses Claude usage (not Meta credit) and adds latency. The install card was shown to the user; the user enables it. |
| **No (rec)** | playwright (MCP) | Microsoft, listed in the official directory | The installed `playwright-cli` skill already covers browser checks. A second browser driver duplicates it and costs more context (INFERENCE). |
| Not proposed | DemoDay, devrunway, securitymaxxing, E2E Test Generator | Community tier | Not official sources. DemoDay is also macOS-only and uses paid fal.ai. |

A standalone-skill search (accessibility, WCAG, video, ffmpeg, demo script, screen reader) returned nothing new.
