# Independent counter-review: Meta hackathon 2026

## 1. Snapshot

**MEASURED — first snapshot commands (PowerShell):** `date -u +%Y-%m-%dT%H:%M:%SZ`; `git rev-parse HEAD`; `git status --short`.

```text
date: PowerShell Get-Date rejected ambiguous parameter '-u'.
HEAD: 9617c7b16977e6a450c93493e1e3e4e6c2a9ebe1
git status --short: <empty>
```

**MEASURED — timestamp correction:** `& 'C:\Program Files\Git\usr\bin\date.exe' -u +%Y-%m-%dT%H:%M:%SZ` returned `2026-10-26T18:58:33Z`. This first successful UTC timestamp is the recorded start; no timestamp was estimated. The client date is October 27 in IST. `codex --version` returned `codex-cli 0.163.0`. Session permissions supplied by the harness: `danger-full-access`, approval policy `never`, network enabled. This is an observation about this session, not a test of the proposed sandbox.

**MEASURED — method:** the tree was clean, so dirty-tree hash treatment was unnecessary. Before the Phase 1 commit, no file beneath `research/` and no repository-root Markdown content was read. Root filenames were listed; only the guide PDFs were opened. Research helpers returned read-only public-source findings without writing files. The only authored file is this report. No installs, model API calls, account actions, forms, or outbound messages to people were used. Cached Context7 was invoked with `--no-install` to reconcile the documentation instruction with the no-installs rule.

**INFERENCE — evidence convention:** CHECKED identifies an opened primary source and a quotation of at most 25 words; MEASURED identifies a command and result; INFERENCE identifies reasoning or proposed tests, not observed product performance. INACCESSIBLE means an attempted source could not be opened/read. NOT CHECKED means no adequate check was completed. Verdict words in later tables classify the claim, independently of these evidence labels. Public README assertions establish described capability, not successful execution. No legal conclusions are made.

**INFERENCE — location convention:** repository text is cited as `path:line @ SHA`, pinned to the clean starting revision unless stated otherwise. PDFs have no text lines: `meta details.pdf:1 @ 9617c7b` and `meta details 2.pdf:1 @ 9617c7b` identify their binary header; PDF page numbers are supplied separately. These are the only Phase 1 local sources. Third-party code references likewise identify a file, line and immutable commit.

**MEASURED — capture comparison:** Python/PyMuPDF, in memory, ran `ds=[fitz.open(x) for x in ['meta details.pdf','meta details 2.pdf']]`; counted pages/text and compared sorted SHA-256 hashes of every extracted page image. Output: `page counts [11,11]`; `text chars [0,0]`; identical image multisets on pages `[2,3,7,8,9,10,11]`. Second-only images: p1 `[]`; p4 `(146,147),(48,48),(3424,388)`; p5 `(2073,7),(50,7)`; p6 `(100,92),(817,7),(885,7)`. Visual inspection of these new images showed icons, an Event Details heading, and divider strips. Thus the second capture supplies no new substantive rules text on the disputed pages. This verifies the supplied image-hash account, without assuming that the captured webpage itself is complete.

### Primary evidence register for the blind review

Each quoted passage below is CHECKED; ensuing interpretations are separately labelled.

| Key | Source and short quotation | What the check establishes |
|---|---|---|
| E1 | [Event](https://cerebralvalley.ai/e/meta-ai-developer-hackathon): “Nov 4: Project submissions due by 9:00 PM ET” | Submission date; page also distinguishes Oct 26 kickoff from Oct 27–Nov 4 workshops. |
| E2 | [Captured guide origin](https://cerebralvalley.ai/e/meta-ai-developer-hackathon/details), `meta details.pdf:1 @ 9617c7b`, pp4–5: “credit card must be applied to your account” | Visually checked guide: public repo, new work, rights rule, building window, credit-card prerequisite and notification wording. Direct live details URL was INACCESSIBLE through web fetch; the local capture was readable. |
| E3 | [API Terms](https://dev.meta.ai/legal/terms-of-service), §10.1: “our Meta Model API Acceptable Use Policy” | API-specific governing terms exist, dated October 9, 2026. §1 distinguishes API use from separately licensed self-hosting. |
| E4 | [API AUP](https://dev.meta.ai/legal/acceptable-use-policy): “without a lawful basis and consent where required by applicable law” | Restrictions cover person tracking and private information; benign redaction is not categorically prohibited by the inspected wording. |
| E5 | [SAM guide](https://dev.meta.ai/docs/sam/segmenting): “One concept per request: there is no multi-concept syntax.” | Concrete-object prompts, boxes/points, source-frame tracking, limits and nondeterminism are documented. Policy interpretation is separate. |
| E6 | [Segmentation overview](https://dev.meta.ai/docs/media-segmentation): “To segment several object types, send several requests.” | Spark-to-SAM composition is explicitly described; each concept has its own request. |
| E7 | [Voice](https://dev.meta.ai/docs/speech-to-text): “Muse Voice Transcribe returns turn-level timestamps, not word-level timestamps.” | Whole-turn muting is feasible in principle; word-exact bleeps need an extra alignment step. |
| E8 | [Video](https://dev.meta.ai/docs/video-understanding): “Audio understanding in Muse Spark 1.3 is currently not fully supported” | Caveat is version-specific; the page also describes embedded audio with 1.2 examples. |
| E9 | [Computer use](https://dev.meta.ai/docs/computer-use): “There's no server-side virtual machine” | Team supplies driver/environment. Spark can run the visual loop too, allowing a same-model comparison. |
| E10 | [Prices](https://dev.meta.ai/docs/pricing-rate-limits): “Rate limits apply per team, not per API key” | Spark $1.25/$4.25 and Wonder $4/$20 per million input/output tokens; Voice $0.18/hour; SAM $0.20/1,000 frames, minimum 50/request. |
| E11 | [Spend alerts](https://dev.meta.ai/help/billing/spend-limit-alert): “doesn't currently offer a spending limit that places a hard cap on usage” | A $100 alert is not an enforced ceiling. |
| E12 | [Guidepup README](https://github.com/guidepup/guidepup): “NVDA on Windows” | Real screen-reader automation exists. Context7 `/guidepup/guidepup` errors documentation explicitly includes recent Windows 10/11; local operation remains untested. |
| E13 | [W3C evaluation guidance](https://www.w3.org/WAI/test-evaluate/tools/selecting/): “cannot check all aspects of accessibility automatically” | Automated findings do not establish whole-site accessibility. |
| E14 | [Deque plans](https://www.deque.com/axe/devtools/pricing/): “component- and user-flow analysis, CI/CD integration, and centralized reporting” | A commercial accessibility workflow category exists; this team's buyer conversion is unproved. |
| E15 | [Mathpix](https://docs.mathpix.com/guides/accessible-pdf): “Default: tagged for PDF/UA-1” | Tagged-PDF generation preserving appearance has direct commercial precedent. |
| E16 | [Axon](https://www.axon.com/products/redaction): “an agency configured exemption log is automatically generated” | Records redaction and exemption logs have existing product precedent. |
| E17 | [YouTube help](https://support.google.com/youtube/answer/9057652?hl=en): “Select Track object to make sure the blurred area moves around.” | Consumer object-blurring/tracking workflow already exists; separate willingness to pay is not established. |
| E18 | [DOJ fact sheet](https://www.ada.gov/resources/2024-03-08-web-rule/): “April 26, 2027” | Current public-entity accessibility compliance guidance has an extended date; regulatory pressure is not proof of demand for this implementation. |

**CHECKED — event details:** guide pp3–4,7–9 at E2 visibly state Oct 27–Nov 4 building, public repositories, three-minute demo, new contributions clearly identified, rights for code/data/assets, maximum team size four, and anti-project examples including basic RAG, simple image analyzers, medical advice, and political/war projects. Stage One is pass/fail on theme and Meta use; Stage Two uses Impact 30%, Meta tooling 25%, Technical Depth & Execution 20%, Demo 25%. The right side of the rubric is clipped in both captures. Visible exact fragments include “How creatively did this team use Meta's AI”, “Is the engineering sound and thoughtfully”, and “Is this a working, impressive demo?”. Full exact descriptions are **INACCESSIBLE in the capture**, and are not reconstructed from the supplied paraphrase. The impact wording is likewise incomplete. Partner resources on pp6–7 show Baseten/Modal $100 offers, selective allocation, and `meta-models/muse-spark-open-1026` for Baseten. Credit receipt was NOT CHECKED.

**MEASURED — dates and capacity:** `python -c` with `datetime(2026,11,4,21,tzinfo=ZoneInfo('America/New_York'))` converted to Asia/Kolkata returned `2026-11-05T07:30:00+05:30`, with ET offset `-05:00`. `print(2*9*8)` returned `144`. **INFERENCE:** this is nominal developer-hours, not evidence of productive capacity after setup, evaluation, approvals and demo work.

## 2. Blind findings, in priority order

### Shared gates

**INFERENCE (E1–E4):** all four can plausibly fit Build for Your World, and P1 can also fit the software frontier theme. None is automatically eligible solely from that mapping. Each must demonstrate new, nontrivial Meta-dependent execution beyond a generic analyzer. Use owned synthetic pages, documents, labels and recordings; an open repository is not permission to reuse underlying personal footage or copyrighted papers. A blank rights provenance entry is a gate, not something a judging score offsets.

**CHECKED (E3–E4):** API Terms §6.2 restrict sensitive/confidential/personal inputs to Contributor Services; §10.1 restricts products targeted at under-18 users. **INFERENCE:** select Standard models explicitly, scope P4 to adult uploaders, avoid actual minors/records in fixtures, and keep P1 on authorized sites. Do not treat removing clue text from final UI as removing private processing inside prompts, transcripts, logs and vendor storage. This corrects the supplied premise that Muse's governing policy could not be found; it does not certify any deployment.

**INFERENCE (E10–E11):** no candidate has established a real $100/account hard stop or full cost. Before future authorized calls, reserve worst-case request cost centrally, limit concurrency/retries/output, account by billing team and account, halt dispatch before the ceiling, and reconcile usage. Do not assume two keys multiply per-team quotas or credits. No paid probe was performed in this review.

### P1 — speech-only website accessibility testing

1. **INFERENCE — eligibility:** substantial Meta reasoning and a reproducible interaction/repair loop can satisfy the theme; a static report merely paraphrasing axe output would weaken it. Fixtures can be wholly authored, without third-party user data.
2. **INFERENCE — safety:** emit reproducible suspected barriers and untested items, never a global accessible verdict. A failed agent run can be a planning/driver failure; a successful run can bypass a barrier a person cannot. Fixes need semantic/keyboard review and rollback.
3. **CHECKED (E9,E12):** driver-based Wonder/Spark control and real NVDA automation are documented. **INFERENCE:** Windows 11 Home is not disproved by Server-focused examples; actual Guidepup/NVDA setup, speech completeness, focus/reset reliability, keyboard-only enforcement, latency and barrier localization are unmeasured dependencies. An accessibility-tree proxy is a distinct experiment, not evidence about real NVDA announcements. Wonder visual versus Spark speech changes model and modality simultaneously. Use the same Spark version for a control and paired healthy/broken pages before attributing divergence to accessibility.
4. **CHECKED (E14):** paying-category evidence exists. **INFERENCE:** no buyer has validated this team's specific workflow or reporting advantage.
5. **CHECKED — capability prior art:** `NewJerseyStyle/auto-a11y-test/README.md:28 @ de42111` ([README](https://github.com/NewJerseyStyle/auto-a11y-test/blob/de42111fafc4f39f4d97f7424fa14c03f2026801/README.md)) describes real NVDA/Guidepup task testing; `src/main.ts:182 @ de42111` returns `nvda.lastSpokenPhrase()`. Mouse tools mean it is not an exact keyboard-only counterpart. `marlon-sousa/screen-readers-mcp/README.md:168 @ b813e8a` ([source](https://github.com/marlon-sousa/screen-readers-mcp/blob/b813e8a2ed0de9d20fe92eedb9fb388067666a0e/README.md)) says “the task has failed” when ordinary-user focus restrictions must be exceeded. [A11y-CUA](https://arxiv.org/abs/2602.09310v1) compares default and AT-constrained agents; [A11yNavigator](https://conf.researchr.org/details/ase-2025/ase-2025-papers/192/Automated-Detection-of-Web-Application-Navigation-Barriers-for-Screen-Reader-Users) detects elements that cannot be “located” or “activated” through a screen reader. **INFERENCE:** remaining wedge is evidence-backed differential diagnosis and repair/retest on held-out barriers, not novelty of AI driving NVDA.

**INFERENCE — cheapest unresolved test:** one developer, a second developer holding out fixtures, 3 developer-hours, $0 for an already available NVDA/Guidepup deterministic speech/keyboard smoke test on one healthy and one broken page. This verifies the driver only. A subsequent budgeted same-model task probe is needed for product discrimination; do not quietly substitute canned outputs for live model evidence.

### P2 — STEM PDF remediation

1. **INFERENCE — eligibility:** a true structural transformation with human-review evidence has theme fit. A screenshot summarizer is weaker. All input figures/formulas/text need reusable rights; benchmark publication alone is insufficient.
2. **INFERENCE — safety:** wrong formulas, reading order or alt text can misteach or exclude. Mark uncertain equations and human checks; a validator pass is not semantic correctness. An HTML MathML twin needs equivalent content/navigation, not just a second file.
3. **CHECKED (E15):** automated PDF/UA-1 tagging already exists commercially. **INFERENCE:** reading a PDF with Spark does not document reliable tag writing, correct formula recognition or MathML. PDF/UA structure, font mapping, reading order, equation verification and cross-viewer behavior remain unproved. Full remediation is not yet a credible nine-day promise; audit-only remains a narrower fallback and therefore P2 is retained conditionally for provenance checks, not endorsed.
4. **CHECKED (E18):** institutional compliance pressure exists. **INFERENCE:** this does not prove purchase intent, and current deadlines must replace stale 2026 urgency claims.
5. **CHECKED — prior art:** `CUNY-AI-Lab/pdf-accessibility-app/README.md:5 @ 44374bb` ([source](https://github.com/CUNY-AI-Lab/pdf-accessibility-app/blob/44374bb60fd7a3792f9d2d9272111b2c45127066/README.md)) flags documents for “manual review” and describes semantic tags, deterministic writing, validation and fidelity checks. [iTagPDF](https://peyajm29.github.io/itagpdf.html) describes “alt texts for figures and formulas”, but uses source semantics; [scientific-PDF research](https://arxiv.org/abs/2503.22216) studies formula alternatives. **INFERENCE:** differentiation requires demonstrable STEM fidelity; tagged PDF plus HTML alone is insufficient.

**INFERENCE — cheapest unresolved test:** second developer authors a short rights-cleared equation/table PDF; first developer audits a proposed output in validator and NVDA/HTML MathML. $0 tools if already available, 4 developer-hours; API reading quality remains NOT CHECKED without separately authorized paid calls. Stop widening remediation if basic equation fidelity or tag writing fails.

### P3 — records-request video redaction

1. **INFERENCE — eligibility:** records workflow is not inherently political or war-related, so a categorical event ban would be unjustified. Use a nonpolitical, synthetic scenario and human-selected targets; no actual bodycam evidence or minor inference is needed for a demo.
2. **INFERENCE — safety:** automatic age/identity determination and legal exemption choices are high-consequence dependencies. The exemption log must be a reviewable draft. Real records raise rights, retention, bystander and cross-border processing questions not settled by redacting the output.
3. **CHECKED (E5–E8):** SAM takes concrete nouns/boxes, not arbitrary policy semantics; Voice supplies turns rather than word boundaries. **INFERENCE:** Spark policy-to-object compilation, identity selection, reliable occlusion recovery and exact audio bleeps are unproved. Human selection and whole-turn muting reduce scope but change the original promise. Do not deepen a B2G production plan until this feasibility gate passes.
4. **CHECKED (E16):** real product demand and exemption-log precedent exist. **INFERENCE:** procurement, secure storage and robust legal handling remain beyond what the described build has demonstrated.
5. **CHECKED — prior art:** Axon already combines masking and exemption logs. [CaseGuard's named agency case study](https://caseguard.com/case-studies/how-the-st-johns-county-sheriffs-office-cut-a-6-hour-body-cam-redaction-to-25-minutes-with-caseguard-ai/) reports “The AI redacted 80% of it on the first pass”. **INFERENCE:** this is vendor-reported buyer evidence, not replicated accuracy; policy-language interpretation must contribute more than existing masking/logging.

**INFERENCE — cheapest unresolved test:** 2 developer-hours, $0, manually translate a synthetic policy into target boxes and a draft exemption log, with the other developer adjudicating ambiguity. A refusal to select targets without age/legal inference kills the broad promise. Live tracking quality still requires a future paid probe.

### P4 — personal-video privacy assistance

1. **INFERENCE — eligibility:** temporal, multimodal editing is more substantial than a simple image analyzer, but the team must show real original execution. Adult-owned synthetic video, fabricated addresses/logos and no location guessing are preferable fixtures. Explicitly choose Standard model IDs.
2. **INFERENCE — safety:** category counts reduce disclosure but do not prove protection. Missed first/last frames, reflections, audio, clothing, landmarks and metadata can reveal identity/location. A same-model second pass can repeat the same miss. Never emit safe-to-post or privacy-complete; disclose scope and withhold an uncertain export. An internal clue transcript or debug preview also matters.
3. **CHECKED (E5–E10):** SAM tracking, Spark scene reasoning and turn-level transcription are documented primitives. **INFERENCE:** small text/logo discovery, translating boxes across rotation/resizing, disocclusion, end-to-end irreversible redaction, full-frame residual detection and acceptable latency remain empirical dependencies. Confidence is not a calibrated privacy-risk probability. Use whole-turn muting or manual audio review rather than assuming word timing.
4. **CHECKED (E17):** a creator blurring workflow exists. **INFERENCE:** no evidence establishes willingness to upload sensitive videos to this new service or pay for it.
5. **CHECKED — close prior art:** `jurayh/open-redactor/README.md:51 @ 572d4f0` ([source](https://github.com/jurayh/open-redactor/blob/572d4f0a8dd343661214845fd27e30ccb07d723e/README.md)) lists “Street signs, house numbers, plates, and mailboxes”; it also describes SAM 3.1, speech muting, metadata stripping, shadow checks and coverage reports. Its optional location audit differs from P4's no-clue output. `ssrajadh/sentryblur/README.md:138 @ ded52d2` ([source](https://github.com/ssrajadh/sentryblur/blob/ded52d269b6e8e19dbbaf79f353426da3a228a98/README.md)) describes “phone screens, monitors, name tags, specific people” and temporal smoothing. `Back-Road-Creative/redactcam/README.md:424 @ 2150869` ([source](https://github.com/Back-Road-Creative/redactcam/blob/215086995f9e8dd3138b2e9e181a2ac6121bde90/README.md)) cautions that coverage checking “does not verify that every pedestrian face was found”. [PPEDCRF](https://arxiv.org/abs/2604.17163v1) studies geolocation despite metadata removal. **INFERENCE:** output restraint and independently evaluated withholding could differentiate; generic SAM redaction and a second pass do not.

**INFERENCE — cheapest unresolved test:** two developers, 3 developer-hours, $0, a withheld synthetic clip with entry/exit, occlusion, reflections, fast small text and audio. Establish ground truth on the final decoded export, not just masks. This tests the evaluator/assembly if existing outputs are available; model detection quality remains unmeasured until authorized paid execution.

## 3. Blind scores with uncertainty bands

**INFERENCE:** conditional hackathon scores, not measured quality or probabilities of winning. A score cannot compensate for an eligibility, rights or safety gate. Bands reflect unresolved execution, differentiation and demand; they are not statistical confidence intervals. No Px is introduced: there is insufficient evidence to justify another build direction.

| Candidate | Impact 30% | Meta tooling 25% | Technical execution 20% | Demo 25% | Weighted central [band] |
|---|---|---|---|---|---|
| P1 | 7.5 [6,8.5]: established workflow need | 8 [6.5,9]: controlled dual interaction | 6.5 [4.5,8]: local speech/causality unproved | 8 [6,9]: clear barrier/fix narrative | 7.550 [5.825,8.650] |
| P2 | 7.5 [5.5,8.5]: institutional need | 6.5 [5,8]: semantic interpretation | 4.5 [2.5,6.5]: correct tags/math difficult | 6 [4,8]: fidelity hard to demonstrate | 6.275 [4.400,7.850] |
| P3 | 7 [5,8.5]: real records buyers | 8 [6.5,9]: multimodal composition | 4 [2,6]: policy/identity/tracking burden | 7 [4.5,8.5]: compelling synthetic example | 6.650 [4.650,8.125] |
| P4 | 6.5 [4.5,8]: user value plausible, demand unproved | 8 [6.5,9]: coordinated models | 6 [3.5,8]: leakage and close precedent | 8.5 [6,9.5]: visual before/after | 7.275 [5.175,8.625] |

**MEASURED — arithmetic:** Python used `w=[.30,.25,.20,.25]` and `sum(a*b for a,b in zip(scores,w))`, likewise for lower/upper vectors. Output: `P1 7.55 (5.825,8.65); P2 6.275 (4.4,7.85); P3 6.65 (4.65,8.125); P4 7.275 (5.175,8.625)`.

**INFERENCE — blind decision:** P1 has a slight central advantage over P4, but their evidence does not separate them. P1 diagnostic assistance has a more defensible failure mode than a P4 safe-to-post verdict; a strictly limited P4 assistance tool remains plausible. Do not commit to a product winner on these point estimates. First discriminate on real NVDA operation, causal barrier evidence and held-out video leakage; if neither demonstrates useful bounded performance, return INSUFFICIENT EVIDENCE.

**MEASURED — Phase 1 timing check:** Unix `date -u +%Y-%m-%dT%H:%M:%SZ` returned `2026-10-26T19:02:33Z` during scoring. Phase 1 used less than its approximately 75-minute allowance; no requirement was inferred to wait out the allowance. Sections 1–3 are frozen by the Phase 1 commit. All later corrections belong in section 9.
