# 12 — Response to the red-team findings (file 11)

- **Written:** 2026-10-26T17:43:38Z (`date -u`) by Claude.
- **Inputs:**
  - file 11 (40 findings);
  - ChatGPT's review of the Codex prompt (user message, 2026-10-26);
  - the user's answers "codex can commit", "claude can read only" and "you may install".
- **Verdicts:**
  - ACCEPT;
  - PARTIAL: accepted, with a correction backed by evidence;
  - DISPUTE.
- **Check status:**
  - **RE-CHECKED** means I fetched or opened the primary source myself in this session.
  - **On 11's evidence** means I accepted the red team's evidence without re-fetching it.

## 1. What changes

1. **The C4 lean is withdrawn.** Re-scored against the official rubric wording (§3), C3 is at 8.23 and C4 at 8.10. That is a tie inside ±1, so the scores do not decide.
2. **The spikes become feasibility probes for blocking failures** (§4). They run on Day 1 and do not rank the candidates.
3. **The decision rule is symmetric.**
   - "Desk favourite C4" is gone.
   - Missing evidence leads to INSUFFICIENT EVIDENCE plus the cheapest test that would settle it, not to a commitment. This also answers ChatGPT's point 5.
4. **C4 gets safety constraints:**
   - It never outputs clue text, timestamps or a location guess.
   - It shows only the redacted video and counts per category.
   - All fixtures use staged props.
5. **My own error (RT07):** Day 1 is **2026-10-27**. The guide says "Building period: Oct 27 – Nov 4" (p4, RE-CHECKED).
   - At 17:14 UTC I changed file 10 from Oct 27 to Oct 28 to match 07 §5, but 07 was the wrong one.
   - Build time is **144 h** (2 developers × 9 days × 8 h), not 128 h.
6. **Governance enforcement must be a hook, not the sandbox.**
   - Claude Code's sandbox does not run on native Windows (S-CC-SANDBOX).
   - Read-only git is now allowed (D15). A blanket `git *` deny would block it, because deny always beats allow.

## 2. Responses

| ID | Verdict | Check | Response and fix | Applied in |
|---|---|---|---|---|
| RT01 | ACCEPT | RE-CHECKED | The media-segmentation page says "To segment several object types, send several requests." The pricing page gives $0.20 per 1,000 frames, with a 50-frame minimum per request.<br>Cost = clue types × fps × seconds × $0.0002. For a 60 s clip with 6 types that is $2.16 at 30 fps, $0.72 at 10 fps and $0.36 at 5 fps (`python -I`).<br>New gate: the billed cost of a 30 s clip is ≤ $1.00 at a tracking fps stated before the run. Subsampled tracking must still pass a native-fps leak check. | 10 §3, 10 §5, PLAN |
| RT02 | PARTIAL | RE-CHECKED | **Overstated on one point.** The page documents instance prompts: "When you already know where an object is, from a user's click or an earlier box, mark it with box and point prompts instead." So a path to "this sign, not that one" exists.<br>**Confirmed:**<br>• the video-understanding page states no timestamps, boxes, fps or billing for Spark;<br>• SAM returns "one box and one mask per match", with no track IDs stated;<br>• "a reflection" and "a landmark" are not valid SAM prompts.<br>Fix: probes V1 (instance restriction, three routes) and V2 (Spark timestamps). C4's clues narrow to concrete objects. This blocks the spike as written, not the concept. | 10 §3, 10 §5 |
| RT03 | ACCEPT | — | New bar: **0 readable planted clues** in a native-fps full-frame check after redaction, confirmed by the other developer. Coverage is reported per clue. | 10 §5, PLAN |
| RT04 | ACCEPT | — | New hard gates:<br>• W1: NVDA + Guidepup speech capture;<br>• W2: at least one interaction-only barrier that axe-core misses. | 10 §5, PLAN |
| RT05 | ACCEPT | RE-CHECKED | My own Wilson intervals match (14/18 is 0.548–0.910; 8/10 is 0.490–0.943).<br>The probes only answer go/no-go on blocking failures and report their CIs. The other developer writes the held-out fixture. | 10 §5 |
| RT06 | ACCEPT | — | The rule is now symmetric with no lean written in advance, and the no-credits case is INSUFFICIENT EVIDENCE (§4). | 10 §5, PLAN |
| RT07 | ACCEPT | RE-CHECKED | The guide (p4) says "Building period: Oct 27 – Nov 4", so Day 1 is Oct 27.<br>Probes are time-boxed at ≤ 5 h per developer, fixtures included: ≤ 10 h of 144 (6.9%, `python -I`).<br>Any code written before Oct 27 is throwaway and is not shipped (new-work rule, p4). | 07, 09, 10, PLAN, LEDGER |
| RT08 | PARTIAL | RE-CHECKED | Agreed that C4's Impact of 8.0 is unsupported.<br>**Correction:** file 05 §1's definition (buyer, dated trigger) is narrower than the official one. Guide p8: "What's the real-world potential here? Who be[nefits] … Could this actually bec[ome something] people use? Does it fit into one of the problem [statements]".<br>Against that wording, C4 Impact is 7.5 (broad audience, no usage evidence) and C3 is 8.0. Aligning 05 §1 is a follow-up. | 10 §4 |
| RT09 | ACCEPT | On 11's evidence | C4's Meta score drops from 9.0 to 8.0. The headline must be cross-frame inference (clue A + clue B → address), not the blur, which SAM tutorials already show. | 10 §4 |
| RT10 | ACCEPT | RE-CHECKED | Lookr "detects faces, plates, signs, logos, and content-policy risks automatically". It handles photos only, $4.99/mo. Imago Obscura (arXiv 2505.20916) handles images only.<br>The gap narrows to video, tracking, a full-frame leak check and cross-frame inference. Lookr's subscription is weak evidence that people pay for pre-share privacy; it publishes no usage numbers. | 10 §3 |
| RT11 | ACCEPT | RE-CHECKED | Stage One is pass/fail (p8), and the anti-list includes "Simple Image Analyzers" (p4).<br>F-anti for C4 becomes **risk**. A 3-outsider read test is added (V4). The demo's first 10 s must show the cross-frame inference. | 10 §2, 10 §5 |
| RT12 | ACCEPT | — | **Design constraint:**<br>• output is the redacted video plus counts per category ("3 location clues blurred");<br>• no clue text, no timestamps, no location guess.<br>**Residual risk:** comparing the output with the original shows where the blur went. That is a small uplift, because the attacker already has the original. It is added to the falsifier. | 10 §3 |
| RT13 | ACCEPT | — | Staged props only (fake house numbers and plates, a fictional crest), filmed in a neutral place, with no bystanders and a consent log. Whether DPDP-Act exposure remains is INFERENCE and was not researched; staged props keep it minimal. | 10 §3, 10 §5 |
| RT14 | ACCEPT | On 11's evidence | C3's novelty rests on three things together: the real NVDA log, the sighted/blind gap and the fix loop. If W1 fails, C3 is dropped. | 10 §3, 10 §5 |
| RT15 | PARTIAL | — | It is true that Windows Home has no Hyper-V (INFERENCE, not re-fetched).<br>**Correction:** the VM rule covers Wonder computer use (AGENTS security). NVDA + Guidepup can run on the host against our own local page, so W1 runs on the host. The GitHub Action claim is dropped until tested. | 10 §3, 10 §5 |
| RT16 | PARTIAL | RE-CHECKED | The gaps are confirmed. **Two of the fixes don't apply:**<br>• "Enable the sandbox": the docs say "On native Windows, Claude Code runs commands unsandboxed" (S-CC-SANDBOX).<br>• A blanket `git *` deny: it would now block D15's read-only git, because deny beats allow.<br>**Fix:**<br>• a PreToolUse hook allowing only read-only git subcommands and rejecting `-c`, `--git-dir` and aliases, drafted at governance install because it is code and needs tests;<br>• now: the deny list is extended with revert, cherry-pick, am, commit-tree, update-ref, notes, reset, clean, restore, `checkout --`, `branch -D`, stash drop/clear, rm and config. | settings.json |
| RT17 | ACCEPT | — | The destructive commands are added to the deny list now. | settings.json |
| RT18 | PARTIAL | RE-CHECKED | Confirmed open, and the sandbox is unavailable (RT16). The sandbox would not cover MCP tools anyway: "Other processes Claude Code starts… run with your full access" (S-CC-SANDBOX).<br>**Fix:**<br>• the same hook rejects GitHub hosts in browser-navigate tool inputs;<br>• now: deny `*git+https://github*` and `*github:*` installs. | settings.json |
| RT19 | ACCEPT | — | Ask rules added for `docs/ledger/PLAN.md`, `FEATURES.json` and `DECISIONS.md`. PROTOCOLS now logs a SHA-256 of the gates table at pre-registration. | settings.json, PROTOCOLS §6 |
| RT20 | ACCEPT | — | Q8 is answered ("codex can commit", D14). Line 9 is the user's own wording, so I propose a rewrite by MCQ instead of editing it.<br>Two things are left for Codex to check:<br>• config.toml cannot express "commit only when told", so that rule stays in AGENTS;<br>• whether `workspace-write` keeps `.git` writable. | AGENTS, QUESTIONS |
| RT21 | PARTIAL | — | The exception is the user's own instruction ("install the required skills you need from official sources"), so I keep it but define it:<br>• **official** means published by Anthropic, either in the `claude-plugins-official` marketplace or as Anthropic's skills;<br>• each install is logged with name, version and scope. The first is D16. | AGENTS, LEDGER |
| RT22 | ACCEPT | — | Resolved by D15. The handoff now lists `git status --short`, and the reviewer reads `git diff`. | PROTOCOLS §12 |
| RT23 | ACCEPT | — | Staged props in a neutral place remove most unplanted clues. Any that remain are judged by the other developer before scoring and count as true if confirmed. | 10 §5 |
| RT24 | ACCEPT | On 11's evidence | Cite SEBI's circular before using it. Reframe the claim as "entities that missed 31 Oct now need evidence fast". | 10 §2 note |
| RT25 | ACCEPT | — | Read the *Amar Jain* judgment and quote it with a paragraph number before it goes in the demo. | 10 §3 |
| RT26 | ACCEPT | RE-CHECKED | `wc -l sources.jsonl` returns 107. | 00, 08 |
| RT27 | ACCEPT | — | Register range updated to F1–F58. | 00 |
| RT28 | ACCEPT | — | S-CC-PERMS and S-CC-SANDBOX added to 00. | 00, sources |
| RT29 | ACCEPT | — | $120 marked as superseded by $100 (09 §3.4). | 01, 04, 07 |
| RT30 | ACCEPT | — | Recomputed from the guide: 9 days and 144 h. The estimated "~22:00 IST" is labelled an estimate. | 01, 10 |
| RT31 | ACCEPT | — | "Revised" line added to 10. | 10 |
| RT32 | ACCEPT | RE-CHECKED | The verbatim quote is "currently not fully supported". | LEDGER F45 |
| RT33 | ACCEPT | — | Relabelled THIRD-PARTY. | 10 §3 |
| RT34 | ACCEPT | RE-CHECKED | The API docs state no track schema. The claim is relabelled as third-party for the API. | 10 §3 |
| RT35 | ACCEPT | — | "Proof" becomes "evidence report". | 01 |
| RT36 | ACCEPT | — | Left for Codex: the changelog is on GitHub. | Codex prompt |
| RT37 | ACCEPT | — | The hook now prints 20 log lines, and the AGENTS step says the hook does it. | session_start.py, AGENTS |
| RT38 | ACCEPT | — | PowerShell rules now mirror Bash. | settings.json |
| RT39 | ACCEPT | — | New draft `.gitattributes` with `merge=union` for LOG and COSTS. STATE.md gets one section per developer. | proposals |
| RT40 | ACCEPT | — | The demo clip is costed separately with the RT01 formula. | 10 §3 |

**Also found while responding (not in 11):**
- **No `.gitignore` in the repo.** `.env` would be committed by `git add -A`. A draft `proposals/.gitignore` is added; installing it is part of the governance MCQ.
- **C5 shares C4's SAM engine.**
  - If V1 or V3 fails, C5 fails too, so it is not a clean fallback.
  - If only V2 (Spark grounding) fails, C5 survives: policy-based class redaction needs no Spark instance reasoning.

## 3. Re-score (official rubric wording; INFERENCE ±1 per criterion; `python -I`)

| Candidate | Impact 30 | Meta 25 | Depth 20 | Demo 25 | Weighted | Change vs 10 §4 |
|---|---|---|---|---|---|---|
| C3 Blindfolded agent | 8.0 | 8.0 | 8.5 | 8.5 | **8.23** | Demo −0.5: a fictional eKYC site has less mass appeal than a reel (11 §4) |
| C4 Privacy guard | 7.5 | 8.0 | 8.0 | 9.0 | **8.10** | Impact −0.5 (RT08), Meta −1.0 (RT09) |
| C5 Redaction, B2G | 7.0 | 8.5 | 7.5 | 9.0 | 7.98 | none |
| C1 Parity-PDF rescoped | 7.5 | 7.0 | 8.0 | 7.5 | 7.48 | none |

**Reading:**
- C3 and C4 are 0.13 apart, inside the noise.
- The scores don't capture two risks:
  - C4's Stage One all-or-nothing misread risk (RT11);
  - C3's NVDA dependency (RT14).
- The probes in §4 test those two risks directly.

## 4. Revised probes and decision rule (replaces 10 §5's spike table; pre-registered; UNAPPROVED)

| Probe | Owner | Setup (time-box) | Blocking pass criteria | Cap |
|---|---|---|---|---|
| **V1** instance (C4) | Dev A | One staged 30 s clip with two fake house-number plates; one is marked sensitive (≤ 2 h, filming included) | SAM masks the marked plate and never the other one, in all 30 human-checked frames where either is visible, by at least one route:<br>(a) a box from a user tap;<br>(b) a box from Spark on one frame;<br>(c) a class prompt plus a Spark crop filter | $1 |
| **V2** grounding (C4) | Dev A | One staged 30 s clip with 6 concrete props, in a neutral place | Spark lists ≥ 5 of the 6 with a time within ±1 s of the truth, in 2 of 3 runs, and with ≤ 1 non-clue listed per run | $1 |
| **V3** cost and leak (C4) | Dev A | V2's clip through the whole pipeline, at a tracking fps stated before the run | Billed cost ≤ $1.00 per 30 s clip, from the usage record. A native-fps full-frame check finds 0 readable planted props, confirmed by Dev B | $1 |
| V4 read test (C4) | Dev B | 3 people outside the team hear the one-sentence pitch | Reported, not blocking: how many call it an image analyzer | $0 |
| **W1** NVDA capture (C3) | Dev B | NVDA + Guidepup on the Windows 11 Home host, against our local page, on a 10-step keyboard task (≤ 2 h) | A complete speech log is captured in 3 of 3 attempts | $0 |
| **W2** blind finding (C3) | Dev B | An accessible control page and a seeded page with 3 interaction-only barriers, written by Dev A. Run axe-core first. | Control: the task completes in ≥ 4 of 5 runs.<br>Seeded: at least 1 barrier that axe-core misses is found and located in ≥ 2 of 3 runs | $2 |
| W3 fix loop (C3) | Dev B | Spark patches one W2 barrier | Reported, not blocking: whether the blind re-run succeeds | in W2 |

**Decision rule.** A candidate passes when all of its bold (blocking) probes pass.

| Outcome | Then |
|---|---|
| Only C3 passes | Build C3. |
| Only C4 passes | Build C4. |
| Both pass | The user chooses from the probe results. No lean is written in advance. |
| Neither passes | If V1 and V3 passed and only V2 failed: C5 is open. Otherwise: C1 audit-only. |
| **INSUFFICIENT EVIDENCE** (credits not posted, or a probe could not run) | No default candidate. See below. |

**When evidence is insufficient:**
- Run every $0 part: W1, the axe-core baseline and the fixture filming.
- V1 can run on SAM 3 open weights if a GPU is available (Q5) or partner GPU credits arrive (guide p6–p7).
- Hard stop at the end of 2026-10-28 IST. The user then decides, and it is logged as "decided on insufficient evidence", naming the untested risk and adding a kill check on 2026-10-30.

**Time:** each developer spends ≤ 5 h on 2026-10-27, so ≤ 10 h of 144 (6.9%).

## 5. What this response did not check
- Rows marked "On 11's evidence" (RT09, RT14, RT24). The search results behind RT14 and the DataCamp, Playground and SEBI sources were not re-fetched.
- GitHub-only checks: these go to the Codex prompt (11 §6 plus ChatGPT's points).
- Whether Hyper-V is missing on Windows 11 Home (INFERENCE).
