# 11 — Red-team findings on the pivot (10) and governance drafts

- **Started:** 2026-10-26T17:22:39Z (`date -u`)
- **Ended:** 2026-10-26T17:35:14Z (`date -u`, taken immediately before writing this file)
- **Reviewer:** independent red team, read-only; this file is the only write.
- **Scope:** `10_PIVOT_BRAINSTORM.md` (primary), LEDGER, 00–09, `proposals/**`, `resources/guide_p*.png`, `sources.jsonl`; Meta and Claude Code docs on the open web. No GitHub access of any kind.
- **Labels:** VERIFIED (I checked the primary source), THIRD-PARTY, INFERENCE (my reasoning), UNVERIFIED.

## 1. Verdict

1. The pivot away from Parity-PDF is defensible. The specific "lean C4" does not survive: C4's cost model is about 6× too low, and its key step (Spark picks out a clue, SAM tracks that one instance) has no documented API path.
2. S-V's own cost criterion (c) fails for arithmetic reasons at 30 fps. Pre-registered as written, the spike rejects C4 on bookkeeping, not on product merit.
3. S-W tests only C3's least novel part, the accessibility-tree proxy. S-V's 95% coverage bar contradicts the product's "0 visible" promise. All of the spikes' sample sizes sit inside noise.
4. The C4 score lead (0.15) comes from an Impact 8.0 that file 05's own definition does not support. Setting Impact to 7 drops C4 to 8.20, below C3's 8.35, and the decision rule still defaults to C4 twice.
5. Governance is broadly valid in syntax but leaks in four places:
   - commit-creating and destructive git subcommands are not covered;
   - browser MCP tools can still reach GitHub;
   - the thresholds in PLAN.md can be edited without a prompt;
   - there is no sandbox network denylist.

**Counts:** 4 BLOCKER · 21 MAJOR · 15 MINOR (40 findings).

## 2. Findings

| ID | Sev | File:line | Claim | What is wrong | Evidence | Fix |
|---|---|---|---|---|---|---|
| RT01 | BLOCKER | 10:124, 10:200 (S-V c), PLAN.md:9 | "a 60-second clip at 30 fps costs about $0.36"; pass requires "Each clip costs ≤ $0.50", spike cap $3 | **Costs are wrong.** SAM segments **one object type per request**, so cost scales with the number of clues:<br>• 6 clues × 1,800 frames = 10,800 frames = **$2.16 per 60 s clip**, and $1.08 per 30 s clip, for SAM alone;<br>• Spark video tokens and the full-frame leak check (09 A16) come on top;<br>• the 3-clip spike is $3.24–$6.48 for SAM alone, which breaks both the $0.50/clip and the $3 caps.<br>AGENTS:38 and TOOLING:52 say a gate is "never renegotiated", so as written C4 fails on arithmetic. | VERIFIED dev.meta.ai/docs/media-segmentation: "To segment several object types, send several requests." VERIFIED dev.meta.ai/docs/pricing-rate-limits: $0.20 per 1K frames, minimum 50 frames. Computed with `python -I`: 60 s / 6 clues → $2.16; 60 s / 7 clues → $2.52; 30 s / 6 clues → $1.08. | Before Day 1:<br>• re-derive cost/clip = clues × frames × $0.20/1K + Spark video + leak check;<br>• pre-register the tracking fps;<br>• set the cap from that formula.<br>If subsampling (e.g. 5 fps), say how the full-frame leak check is still met. |
| RT02 | BLOCKER | 10:115–118, 10:138, 10:140 | Spark "lists every clue… a reflection, a landmark"; "SAM 3.1 tracks each clue through the video by text prompt" | **The Spark→SAM handoff is undocumented.**<br>• SAM's API takes "a short noun phrase that names one concrete object" and returns **every** match. You cannot point it at *this* sign out of all signs, so the app either blurs every "sign" or none.<br>• "A reflection", "a landmark" and "a screen showing a name" are not concrete-object noun phrases.<br>• The Spark video docs give no fps sampling, timestamps, spatial grounding, billing basis or maximum duration. Spark therefore cannot tell SAM *where* or *when* a clue is.<br>• The API docs describe no track ID or format.<br>This handoff is C4's whole novelty claim (10:135). | VERIFIED dev.meta.ai/docs/media-segmentation (prompt rule; one box and mask per match; no track schema). VERIFIED dev.meta.ai/docs/video-understanding (mp4 accepted; fps, billing and grounding not stated). | Make "Spark → instance-level SAM prompt" the **first hour** of S-V. Test it on 1 clip with 2 same-class objects (2 signs, only 1 sensitive).<br>Fail fast if SAM cannot be restricted to one instance (box prompt, frame index, or post-filter by Spark crop check). |
| RT03 | BLOCKER | 10:200 (S-V b) vs 10:153; 04:209; PLAN.md:9 | Pass if "SAM masks cover the clue in ≥ 95% of hand-checked frames"; demo says "0 visible" | **The pass bar contradicts the product.**<br>• 95% coverage allows 5 leaked frames per 100. One readable frame of a house number defeats a privacy guard.<br>• File 04's own redaction acceptance was "0 unredacted target frames… (blocking)". 09 A16 accepted that 5 fps interpolation "cannot claim zero exposed frames".<br>• PLAN.md:9 drops "where it is visible", so 95% of *all* frames is ambiguous, and it is unclear whether coverage is per clue or pooled. | Quotes above; `sed -n 9p PLAN.md`. | Pre-register: **0 readable leaks** for planted clues in the full-frame check (human-confirmed). Report coverage per clue. Restore "where it is visible" in PLAN.md. |
| RT04 | BLOCKER | 10:199 (S-W), 10:83–85, 10:94 | S-W fixture: "Proxy speech only"; pass (b) "≥ 3 of the 5 seeded barriers" | **S-W does not test C3's thesis.**<br>• NVDA/Guidepup (differentiator 1, Windows-only, riskiest) is untested.<br>• The sighted Wonder agent and the "differential gap" (differentiator 2) are untested.<br>• The fix loop (3) is untested.<br>• (b) can pass on the 2 static barriers, which axe-core already finds, plus 1 of 3 interaction-only barriers. axe-core is listed for evaluation (10:99) but is not in the spike.<br>A pass shows only "an LLM can tab an AX-tree dump of our own page". | 10:199 text; Guidepup ships a virtual screen reader for tests, so the proxy is not new (guidepup.dev, THIRD-PARTY). | Change (b) to "≥ 2 of 3 interaction-only barriers in ≥ 2 of 3 runs, and ≥ 1 barrier axe-core misses". Add a ≤ 2 h NVDA+Guidepup smoke test that captures one real speech log, as a hard pass criterion. |
| RT05 | MAJOR | 10:199–200 | 14/18 recall; 8/10 control; 2 of 3 runs; 3 of 5 barriers | **Samples are too small to discriminate.** Wilson 95% intervals:<br>• 14/18 = 0.55–0.91;<br>• 8/10 = 0.49–0.94;<br>• 2/3 = 0.21–0.94;<br>• 3/5 = 0.23–0.88.<br>Pass or fail sits inside noise. The fixtures are made by the same people who tune the prompts, with no held-out set, and planted clues are salient by design. 09 A04 / §1.1 already rejects bars "unsupportable at n ≈ 125"; here n = 18. | `python -I` Wilson computation (this review). | Call the spikes **feasibility smoke tests**: go/no-go on blocking failures (RT02, NVDA capture), not ranking. Report CIs. Hold out 1 clip and 1 page written by the other developer. |
| RT06 | MAJOR | 10:184 vs 10:204, 10:206 | "0.15 apart, well inside the noise"; both pass → "My lean is C4"; no credits → "Desk favourite: C4" | **The decision rule is asymmetric.** C4 wins unless it actively fails, yet the text says scores should not decide. Combined with RT04, where C3's spike proves little, the spike cannot move the decision towards C3. | 10:184, 10:204, 10:206. | Pre-register a symmetric tie-break that does not reuse the scores, e.g. "the candidate whose top un-retired risk is smaller after the spike". Desk decision without credits: state it as a tie and let the user choose. |
| RT07 | MAJOR | 10:207 | Day 1 = 6–8 h per developer | **Fixture building is unbudgeted.**<br>• S-W needs a two-version eKYC site, a harness, and 10+10+15 runs.<br>• S-V needs 3 clips filmed with 18 planted props, Spark prompts, SAM integration and mask rendering. It also needs hand-labelling 300 frames for up to 6 clues each (≤ 1,800 judgements).<br>• Credits and API approval arrive on an unknown day.<br>The building period starts **Oct 27** (guide p4), but the plan's Day 1 is Oct 28, so a day is idle. | guide_p4.png "Building period: Oct 27 – Nov 4"; 10:195. | Time-box each sub-task. Use Oct 27 for fixtures, after checking whether the rules allow prep before the period. Cut the frame labelling to frames flagged by the leak check plus a random 30. |
| RT08 | MAJOR | 10:178 vs 05 §1, 10:163 | C4 Impact 8.0 | **Score inflation.** File 05 §1 defines Impact as "demand evidence, buyer reachability, dated trigger, commercial scale". C4 has:<br>• no demand evidence;<br>• no buyer;<br>• "No regulatory deadline" (10:163).<br>C5, the same engine with a B2G buyer and measured costs, gets 7.0. 10:188 concedes C3's Impact "could be higher". With `python -I`: C4 Impact 7 → **8.20 < C3 8.35**; Impact 7 and Meta 8 → 7.95. | 05 §1; 10:163, 10:178–188; recomputation. | Re-score Impact against 05 §1 with one evidence line per sub-criterion. Present C3 ≥ C4 unless demand evidence exists (e.g. a 20-person poll on whether people would run it before posting). |
| RT09 | MAJOR | 10:138, 10:178 | Meta 9.0; "highest Meta-tooling fit of any candidate" | **The SAM half of C4 is Meta's own showcase.**<br>• The Segment Anything Playground already offers pixelate/blur effects on text-prompted objects.<br>• Meta says SAM 3 is coming to Instagram Edits.<br>• DataCamp (2025-11-27) has a "SAM3 Tutorial: Build a Privacy Filter" that blurs faces, plates and screens in images and MP4.<br>The rubric asks "beyond a basic integration… surprised even us" (guide p8). | ai.meta.com/sam3 (THIRD-PARTY via heise for Playground effects); datacamp.com SAM3 privacy-filter tutorial; guide_p8.png. | Meta ≤ 8 until the Spark cross-frame reasoning (the non-tutorial part) is shown working. Make that, not the blur, the headline. |
| RT10 | MAJOR | 10:125–132, 10:135 | "No consumer video defence found"; novelty = "open-vocabulary, reasoning-based clue detection" | **Prior art is missed (§3).**<br>• Lookr (iOS, $4.99/mo) already scans photos before sharing for faces, plates, signs and logos, and inpaints them.<br>• Imago Obscura (arXiv 2505.20916) is a pre-share privacy co-pilot that finds *context-relevant* risks and blurs or inpaints them.<br>The claim is only true for video. | Lookr App Store page; arXiv 2505.20916. | Add both to prior art. Narrow the claimed gap to "video + temporal tracking + full-frame leak check + cross-frame inference". |
| RT11 | MAJOR | 10:37, 10:160; guide p4, p8 | F-anti = "pass" | **The "Simple image analyzer" risk is under-weighted.** Stage One is pass/fail on theme fit (p8), so a misread costs everything, not points. The one-sentence pitch ("AI looks at your video and blurs private stuff") *is* the anti-project. 10:160's answer is an assertion with no evidence. | guide_p4.png anti-list "Simple Image Analyzers"; guide_p8.png Stage One. | Mark F-anti as **risk**. The first 10 s of the demo must show the inference no image analyzer can do (clue A in frame 40 + clue B in frame 300 = address). Run a 3-outsider one-sentence read test. |
| RT12 | MAJOR | 10:116, 10:137, 10:37 (F-AUP) | "It never outputs a location guess, so it cannot be turned into a stalking tool" | **The clue list is itself the doxxing output.** Upload someone else's reel and you get "house number at 0:07, school crest at 0:12, street sign at 0:21". The falsifier tests only location extraction. GeoSpy (10:121) is exactly this abuse pattern. | 10:116, 10:137. INFERENCE. | Output only the blurred video plus generic categories; never clue text with timestamps. Or restrict uploads to the device camera roll. Add "clue list used against a third party" to the red-team falsifier. |
| RT13 | MAJOR | 10:142, 10:151–153, 10:156 | "Self-filmed clips with planted clues"; morning-routine reel | **Legal and consent exposure.**<br>• Self-filmed clips at home show the developers' real address, plates and bystanders.<br>• They are uploaded to a cloud model and then published in a public demo.<br>• India's DPDP Act 2023 is not considered (INFERENCE).<br>• Rules ban data "you do not have the rights to" (p4). | guide_p4.png; 10:156 admits the irony. | Use staged props only: fake house numbers and plates, a fictional school crest. No bystanders. Film in a neutral location. Record consent for anyone shown. |
| RT14 | MAJOR | 10:72–81, 10:83, 10:94 | C3 prior art is 5 works; the proxy is "fast" and NVDA is "evidence" | **C3 prior art is also missed:**<br>• ScreenAudit (recall 69.2%, precision 71.3% vs a checker's 31.3%);<br>• "Are We There Yet?" (arXiv 2609.00524): computer-use agents for 8 blind users were unreliable;<br>• UXAgent (2502.12561); the MCP accessibility-tree paper (2608.24898);<br>• Scott Logic 2024 (LLM driving a screen reader);<br>• Assistiv Labs (cloud assistive tech with screen-reader automation); the W3C AT Driver spec;<br>• Guidepup's own virtual screen reader.<br>With proxy only, C3 ≈ "an LLM agent reading the AX tree", which is common. | Search results (§3). | Add them. State that novelty depends on the real-NVDA log + gap + fix loop. If NVDA fails, C3's novelty mostly falls with it. |
| RT15 | MAJOR | 10:83, 10:94, 10:108 | "Guidepup cannot capture NVDA speech reliably in our VM" | **The VM is unspecified.** This machine is Windows 11 Home Single Language (environment). Hyper-V is not available on Home (INFERENCE), so the VM means VirtualBox or similar, with audio and speech hooks unverified. The "GitHub Action" interface (10:95) also needs a Windows runner. | Session environment OS string. | Name the VM route now. Make the NVDA capture a Day-1 hard gate (RT04). Drop the CI claim unless it is tested. |
| RT16 | MAJOR | settings.json:3–53 | Claude git writes are denied | **Commit-creating and history-rewriting subcommands are not denied:**<br>• `git revert`, `cherry-pick`, `am`, `commit-tree`, `update-ref`, `notes`;<br>• `git reset --soft/--mixed HEAD~`;<br>• `git config alias.p push` then `git p`;<br>• `git 'push'`; `git --git-dir=.git push`.<br>The docs say rules match command text and recommend sandboxing for real enforcement. | `grep revert\|cherry\|clean\|restore` in settings.json → no matches. code.claude.com/docs/en/permissions ("A push written another way… isn't matched"; sandboxing). | Take the option TOOLING:50 already names: one `Bash(git *)` / `PowerShell(git *)` deny until Q9 is answered. Later, allowlist read-only subcommands explicitly. Enable the sandbox. |
| RT17 | MAJOR | settings.json:54–79 (ask) | Uncommitted work is the handoff (PROTOCOLS §12) | **Destructive commands are ungated:** `git clean -fdx`, `git checkout -- .`, `git restore .`, `git branch -D`, `git stash drop`, `git rm`. Because "Claude never commits", uncommitted files are the only copy, and one command erases them. | Same grep; ask list lines 54–79. | Deny these (covered automatically by RT16's `git *` deny). |
| RT18 | MAJOR | settings.json:3–53; AGENTS:11 | "Claude never accesses GitHub (web, API, `gh`, MCP)" | **Only WebFetch, curl/wget/iwr and two MCP names are blocked.** Still open:<br>• browser MCP tools (`mcp__claude-in-chrome__navigate`, `mcp__Claude_Browser__navigate`, `rea` web-capture tools), all present in this session's tool list;<br>• `python -c urllib…`;<br>• `pip install git+https://github…` and `npm i github:` (only "ask").<br>There is no sandbox network denylist. | Session deferred-tool list; settings.json lines 25–43. | Add deny rules for the browser MCP navigate tools, or a sandbox `network` denylist for the GitHub domains, which is the only real enforcement. Deny `*git+https://github*` and `*github:*` installs. |
| RT19 | MAJOR | AGENTS:38; settings.json:73–78 | "never lower a threshold… pre-registered in PLAN.md" | **Pre-registration is prose only.** `docs/ledger/PLAN.md`, `FEATURES.json` and `DECISIONS.md` are not in ask or deny, so an agent can edit a threshold without a prompt. TOOLING:46 itself says "Instruction files are context, not enforcement". | settings.json ask list has no `docs/ledger` entry. | Add `Edit(/docs/ledger/PLAN.md)`, `Edit(/docs/ledger/FEATURES.json)` and `Edit(/docs/ledger/DECISIONS.md)` to ask. Log a hash of the thresholds in LOG.jsonl when pre-registering. |
| RT20 | MAJOR | AGENTS:9 vs AGENTS:10; .codex/config.toml | "done by user only and claude is not allowed to ever access it" vs "Codex runs one only when the user tells it" | **The core rule contradicts itself** in a file loaded every session. "It" is ambiguous: git, GitHub, or releases? Q8 is pending, but the contradiction ships now.<br>config.toml (`on-request`, `workspace-write`) expresses nothing like "commit only when told". Whether workspace-write protects `.git` is unverified. | AGENTS:9–10 via `sed`; config.toml. | Rewrite line 9 now, e.g. "Commit/push/merge/tag/release/deploy: the user, or Codex when the user asks in that session. Claude: never; Claude never accesses GitHub." Verify Codex `.git` behaviour (Needs Codex). |
| RT21 | MAJOR | AGENTS:12 | "Exception: skills from official sources (user pre-approved)" | **"Official" is undefined.** Skills can carry scripts and hooks, so this is an unscoped injection channel. It conflicts with the user's memory rule that nothing enters the repo or rules without MCQ approval. | AGENTS:12; MEMORY "approval-gated MCQ workflow". | Replace with an explicit allowlist (name, publisher, version), or remove the exception. |
| RT22 | MAJOR | PROTOCOLS:155 (§12); AGENTS:64 | Handoff lists "Uncommitted… from this session's file edits"; "other agent reviews the diff" | **The handoff relies on session memory.** After `/clear` or auto-compaction (as happened in this review), the edit list is lost. Without `git status`/`git diff` (Q9) there is no diff to review, so the review step cannot run as written. | PROTOCOLS:150–158. | Grant read-only `git status`/`git diff`/`git log` (Q9), or have Claude append every edit path to LOG.jsonl at edit time. |
| RT23 | MAJOR | PLAN.md:9; 10:200 (S-V a) | "≤ 3 false clues per clip" | **"False clue" is undefined.** Self-filmed clips contain real, unplanted clues (actual signs, real reflections). If Spark finds them, is that a false positive or a success? The ground truth is incomplete by construction. | INFERENCE from the fixture design. | Pre-register that unplanted real clues are adjudicated by the other developer before scoring and count as true positives if confirmed. |
| RT24 | MAJOR | 10:50, 10:69; LEDGER:73 (F54) | SEBI "audit and remediation deadline is 2026-10-31" | **The why-now has a source problem and a timing problem.**<br>• The cited S-SEBI-A11Y (Lexplosion) headline extends only the "due date for conducting Accessibility Audit". Other secondary sources (DigitalA11Y, a dev.to post, Moneycontrol via TradingView) say audit and remediation now share Oct 31. The claim is probably right, but cited to the wrong source, and SEBI's PDF is unread.<br>• The date passes **during the build**, so by judging the why-now is "a missed deadline". | lexplosion.in SEBI page; search results (digitala11y.com, dev.to, tradingview.com). | Cite SEBI's circular directly. Reframe the pitch as "entities that missed 31 Oct now need evidence fast". |
| RT25 | MAJOR | 10:104; 10:49 | Demo opens with the *Amar Jain* blind KYC petitioner | **The pitch's lead fact is from press only** ("judgment not read"). A lawyer-judge will check it, and a misstatement in the first 10 s costs credibility. | 10:49 label. | Read the judgment and quote one line with a paragraph number before using it in the demo. |
| RT26 | MINOR | 00:3; 08:167 | "106 records by `wc -l`" | `wc -l sources.jsonl` = **107**. | Command output this review. | Update both. |
| RT27 | MINOR | 00:3 | Register covers "F1–F56" | LEDGER has F57–F58 (LEDGER:76 onward). | `grep F57` LEDGER. | Update. |
| RT28 | MINOR | 00 (source index) | Index covers all cited IDs | **S-CC-PERMS** is cited in LEDGER:145 and present in sources.jsonl (1 hit), but appears 0 times in 00. | `grep -c S-CC-PERMS` → 00: 0, sources: 1. | Add to 00. |
| RT29 | MINOR | 01:34; 04:163; 07:29 (D8) | Budget hard stop $120 | 09 §3.4, AGENTS:51 and PROTOCOLS §11 say **$100**. 07 is superseded only in its banner. | `sed` outputs above. | Edit the rows themselves, or strike them through. |
| RT30 | MINOR | 01:11, 01:13 vs 10:207; 10:29–30 | "~22:00 IST" → 144 ph; "9 days" | **Three inconsistencies:**<br>• 01:11 is an estimated timestamp, against LEDGER:15's process rule;<br>• 144 ph (01) vs 128 h (10:207);<br>• the F-9d filter says "9 days" but 10:207 says 8 build days. | `sed` outputs above. | Recompute once from the guide's building period and use one number. |
| RT31 | MINOR | 10:3 | "Written: 2026-10-26T16:58Z" | File mtime is 17:17:48Z (22:47:48 +0530) with no revision note. 00:3 says round 2 ran to 16:58. | `stat` this review. | Add a "Revised: <date -u>" line. |
| RT32 | MINOR | LEDGER:64 (F45) | Spark audio "not fully reliable" (in quotes) | Docs say audio is "currently not fully supported" and may be degraded. The quote marks wrap non-verbatim text. | dev.meta.ai/docs/video-understanding. | Quote verbatim. |
| RT33 | MINOR | 10:122 | VLM-GEOPRIVACY cited as CITED | S-VLM-GEOPRIV is an Emergent Mind aggregator page; LEDGER labels it "THIRD-PARTY / PRIMARY-SOURCE CLAIM". 10:122 drops the label. | sources.jsonl record. | Label THIRD-PARTY or cite the arXiv paper. |
| RT34 | MINOR | 10:124 | "SAM 3.1 (March 2026) added multi-object tracking (F14)" | The source is GIGAZINE (third-party), and the API docs show no tracking output schema. Mark it UNVERIFIED for the API (see RT02). | sources.jsonl S-SAM31; media-segmentation page. | Relabel. |
| RT35 | MINOR | 01:47 | "Review UI + proof report" | "Proof" was retired (09; 10:15). | `sed -n 47p`. | Rename to "evidence report". |
| RT36 | MINOR | TOOLING:53 | "`/doctor prompt-audit`… needs v2.1.283+" | Not verified in this review; no primary source fetched. | — | Verify in the Claude Code changelog (Needs Codex if only on GitHub). |
| RT37 | MINOR | session_start.py:15 vs AGENTS:22 | Agent runs `tail -n 20 LOG.jsonl` | The hook already prints the last **5** lines, so the agent reads the log twice at a different depth. | `grep` session_start.py. | Pick one depth; drop the AGENTS step or make the hook print 20. |
| RT38 | MINOR | settings.json:37–38 | PowerShell parity with Bash | PowerShell has `git -C * commit/push` but no `-C * merge/tag` and no `-c *` variants (Bash has them, lines 18–23). | `grep` settings.json. | Mirror the rules (moot if RT16's `git *` deny is adopted). |
| RT39 | MINOR | PROTOCOLS (STATE/LOG/CODEMAP) | One STATE.md, LOG.jsonl and CODEMAP.md | With 2 developers on branches or worktrees, every merge conflicts on these files. | INFERENCE. | Use a `.gitattributes` `merge=union` for LOG.jsonl and per-developer STATE sections. |
| RT40 | MINOR | 10:152 vs 10:200 | Demo "Spark lists 7 clues"; spike uses 6 per clip | The cost per clue grows with count (RT01), so the demo clip costs more than the spike measured. | 10:152, 10:200. | Use the same clue count, or cost the demo clip separately. |

## 3. Missed prior art and competitors

**C4 (privacy guard)**
- **Lookr: AI Photo Privacy** (iOS). Detects "faces, plates, signs, logos, and content-policy risks" and inpaints them; $4.99/mo; photos only. https://apps.apple.com/us/app/lookr-ai-photo-privacy/id6761846110
- **Imago Obscura** (arXiv 2505.20916, CMU/Tsinghua). Pre-share image-privacy co-pilot: finds context-relevant risks, then blurs, inpaints or generatively replaces them; 15-user study. https://arxiv.org/abs/2505.20916
- **DataCamp, "SAM3 Tutorial: Build a Privacy Filter"** (2025-11-27). A Gradio app that blurs text-prompted faces, plates and screens in images and MP4. https://www.datacamp.com/tutorial/sam3-tutorial-segment-everything-3-build-a-privacy-filter (THIRD-PARTY)
- **Meta's own SAM 3**. The Segment Anything Playground has pixelate and blackout effects on segmented objects, and SAM 3 is announced for Instagram Edits. https://ai.meta.com/sam3/
- **Threat-side sources worth citing** instead of an aggregator:
  - Privacy International, "Nowhere to Hide? Privacy Risks and Policy Implications of AI Geolocation": https://privacyinternational.org/report/5736
  - McAfee: 91% of 20,000 images held a location clue (reported by ABC7).
  - Redact.dev and Kaspersky posts on AI photo geolocation and doxing.

**C3 (blindfolded agent)**
- **ScreenAudit** (mobile; recall 69.2%, precision 71.3% vs a checker's 31.3%).
- **"Are We There Yet? … Computer-Use Agents for Blind Users"**: https://arxiv.org/abs/2609.00524
- **UXAgent**: https://arxiv.org/abs/2502.12561
- **MCP accessibility-tree agent paper**: https://arxiv.org/abs/2608.24898
- **Guidepup virtual screen reader**, which already does what the proposed "linearizer proxy" would: https://www.guidepup.dev/
- **W3C AT Driver**: https://w3c.github.io/at-driver/ (GitHub-hosted, so **not opened**; Needs Codex).
- **Assistiv Labs**, a cloud assistive-tech testing service with screen-reader automation: https://assistivlabs.com/
- **Scott Logic** (2024 blog post): LLMs navigating with a screen reader.

## 4. Strongest case against each

**Against C4**
1. The cost model is wrong by about 6× (RT01).
2. The step that makes it more than a blur tool has no documented API path. Spark cannot be shown to localise a clue in time or space, and SAM cannot be told "this sign, not that one" (RT02).
3. The part that does work is Meta's own Playground feature and a public tutorial (RT09).
4. Its one-line pitch is the anti-project, and Stage One is all-or-nothing (RT11).
5. It has no buyer and no deadline, so Impact is unsupported (RT08).
6. A privacy tool that uploads to the cloud and whose output is a doxxing map is a lawyer's dream (RT12, RT13).
7. The spike's 95% bar would certify a product that leaks (RT03).

**Against C3**
1. The spike tests only the part that is not novel (RT04).
2. The differentiators sit on unretired risks: NVDA under Guidepup in an unspecified VM on Windows 11 Home (RT15), and Wonder in preview at $4/$20.
3. The space is academically crowded: TaskAudit, ScreenAudit, AXNav, and agentic auditing at 86% recall (RT14).
4. Agents are measured as unreliable for non-visual use, which threatens the 8/10 control gate.
5. The team seeds its own barriers, so "found them" is close to self-fulfilling (RT05).
6. The Indian why-now deadline passes before judging (RT24), and the demo lead fact is unread press (RT25).
7. A fictional eKYC site is less "wow" for the mass-appeal goal than a reel.

## 5. What would change the recommendation

- **Towards C4:**
  - A 1-hour probe shows SAM can be restricted to one instance (box or frame prompt) and Spark returns usable timestamps;
  - the re-derived cost (RT01) fits ≤ $1 per 30 s clip at a fps that still passes a full-frame zero-leak check;
  - an outsider read test does not hear "image analyzer".
- **Towards C3:**
  - Impact is re-scored per 05 §1 (C3 then leads, 8.35 vs ≤ 8.20);
  - a ≤ 2 h NVDA+Guidepup capture works in a named VM;
  - the agent finds ≥ 1 interaction-only barrier that axe-core misses.
- **Towards C5 or C1:**
  - both of the above fail, or
  - a video product like Lookr is found (C4 novelty gone) and NVDA capture fails (C3 novelty gone).
- **Regardless of candidate:** fix RT01–RT06 before running any spike, or its result means little.

## 6. Needs Codex (GitHub-only checks; not attempted)

1. Guidepup repo:
   - MIT licence;
   - NVDA support on Windows, including in a VM;
   - how faithful the virtual screen reader is to NVDA.
2. SAM 3 / SAM 3.1 repos (facebookresearch): weights licence, and whether 3.1 weights are released, for the local "H2" path (10:159, Q5).
3. Open-source competitors on GitHub:
   - pre-post video privacy scanners;
   - LLM agents driven by NVDA or VoiceOver speech;
   - TaskAudit and ScreenAudit code availability.
4. W3C AT Driver spec text (w3c.github.io).
5. ASSETS'25 artifact repo licence; Matterhorn 1.1 condition split, if it is hosted on GitHub (C1).
6. wshobson/agents "screen-reader-testing" skill: existence and licence.
7. Codex docs and source: does `sandbox_mode = "workspace-write"` keep `.git` writable? (RT20)
8. Claude Code changelog: the version that introduced `/doctor prompt-audit` (RT36).

## 7. Checks performed and outcomes

| # | Check | Outcome |
|---|---|---|
| 1 | dev.meta.ai/docs/pricing-rate-limits | VERIFIED prices (Spark 1.3 $1.25/$4.25, Wonder $4/$20, SAM $0.20/1K frames with a 50-frame minimum, Voice $0.18/h). Rate limits are per team. Spark video billing not stated. |
| 2 | dev.meta.ai/docs/media-segmentation | **One object type per request**; concrete-noun-phrase prompts; one box and mask per match; no track schema (RT01, RT02). |
| 3 | dev.meta.ai/docs/video-understanding | mp4 with audio accepted. fps, billing, maximum duration and grounding not stated. Spark 1.3 audio "currently not fully supported" (RT02, RT32). |
| 4 | dev.meta.ai/docs/models | Model IDs confirmed. Wonder is in preview; Voice Transcribe is turn-level with no word timestamps; there is no TTS. |
| 5 | code.claude.com/docs/en/permissions | Settings syntax valid (`/path` anchors, `domain:*.x`, plugin MCP naming, env stripping). Text-matching limits and the sandbox recommendation confirmed (RT16–RT18). |
| 6 | resources/guide_p1, p4, p8, p9 (local PNG) | Building period Oct 27–Nov 4; the anti-list includes "Simple Image Analyzers"; Stage One is pass/fail; rubric 30/25/20/25 (RT07, RT11). |
| 7 | arXiv 2505.20916 (Imago Obscura) | Confirmed pre-share privacy co-pilot (RT10). |
| 8 | Lookr App Store page | Confirmed photo pre-share scanner for signs, plates and logos (RT10). |
| 9 | Searches: AI geolocation privacy | Privacy International report; McAfee 91% figure; Redact.dev, Kaspersky, Tom's Hardware. |
| 10 | Search: SAM 3 privacy blur / Meta Playground / Edits | Playground effects; Edits announcement; DataCamp tutorial (RT09). |
| 11 | Searches: LLM screen-reader agent prior art | ScreenAudit, "Are We There Yet?", UXAgent, MCP AX paper, Scott Logic, Guidepup virtual screen reader, Assistiv Labs, AT Driver (RT14). |
| 12 | lexplosion.in SEBI page (S-SEBI-A11Y) | Headline covers the audit only; no standards or circular number on the page (RT24). |
| 13 | Search: SEBI Oct 31 extension | Other secondary sources say audit and remediation now share Oct 31; SEBI's PDF still unread (RT24). |
| 14 | `python -I` score recomputation | 8.50 / 8.35 / 7.975 / 7.475: reproduces the table (rounded). With C4 Impact 7: 8.20 (RT08). |
| 15 | `python -I` Wilson 95% intervals | 14/18 0.55–0.91; 8/10 0.49–0.94; 2/3 0.21–0.94; 3/5 0.23–0.88 (RT05). |
| 16 | `python -I` SAM cost per clip | 60 s × 1 clue $0.36; × 6 $2.16; × 7 $2.52; 30 s × 6 $1.08 (RT01). |
| 17 | `wc -l sources.jsonl` | 107 (RT26). |
| 18 | `grep` settings.json (deny/ask contents) | No revert/cherry-pick/clean/restore, no `docs/ledger` ask, no sandbox block, no browser-MCP deny. PowerShell iwr, Invoke-WebRequest and Invoke-RestMethod `*github*` are present (RT16–RT19, RT38). |
| 19 | `stat` on 10_PIVOT_BRAINSTORM.md | mtime 17:17:48Z vs "Written 16:58Z" (RT31). |
| 20 | `grep` 00 / sources.jsonl for S-CC-PERMS | 0 vs 1 (RT28). |
| 21 | `sed` line checks in 00, 01, 04, 07, 08, 09, AGENTS, PLAN, PROTOCOLS, TOOLING, session_start.py | Line citations in this table confirmed. |
| 22 | LEDGER F1–F58, D1–D13; QUESTIONS Q1–Q10 | IDs are contiguous. Q8 (Codex commits) and Q9 (Claude read-only git) are still open and drive RT20 and RT22. |
| 23 | GitHub-hosted sources | **Not accessed** by rule; listed in §6. No bot-blocks or CAPTCHAs met. No paid calls, installs, forms or accounts. |
