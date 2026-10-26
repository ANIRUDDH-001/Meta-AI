# 10 — Pivot brainstorm (UNAPPROVED)

- **Written:** 2026-10-26T16:58Z (`date -u`).
- **Revised:** 2026-10-26T17:47:51Z (`date -u`), after the red team (file 11) and the response (file 12). The C4 lean is withdrawn. §4 adds the re-score, and §5's spike table is replaced by feasibility probes. The first version is in commit `c00bbda`.
- **Inputs:**
  - the audit consequences (09);
  - the user's confirmation of the Indie track;
  - the user's goals: "attract masses", world-class, shippable, a premium 3-minute story, "ambitious, but not imagining";
  - the user's request to look at Indian development and defence needs.
- **Evidence labels:** CITED (source ID, added to `sources.jsonl` in this pass) · THIRD-PARTY · INFERENCE · UNKNOWN.
- **Scores are INFERENCE, ±1 per criterion.** No candidate has been tested.

## 1. What changed since file 08

1. **The audit shrank Parity-PDF's claims** (09):
   - "Proof" is out.
   - MathML holds only in the HTML twin, not the PDF.
   - E3 can support no competitive claim.
   - The deadline is contested in both directions.
   - What is left is a narrower, harder-to-demo product.
2. **The Indie track is judged on "creativity, technical ambition, and whether it works"** (S-EV). That favours a product judges can try and instantly understand, and lowers the weight of a B2B buying process.
3. **The user wants mass appeal.** File 08 optimised for a compliance buyer. That is a different target.

## 2. Wide list and hard filters

Filters:
- **F-anti:** anti-project list (S-PG p4).
- **F-AUP:** the use policy at dev.meta.ai/use-policy/ (S-META-AUP). The page is labelled Llama 2, so its scope for Muse is UNKNOWN; we treat it as binding to be safe.
- **F-rights:** we can obtain rights-clean data (R6).
- **F-9d:** a working kernel in 9 days with 2 developers.
- **F-claim:** the core claim can be measured honestly in 9 days.

| # | Candidate | F-anti | F-AUP | F-rights | F-9d | F-claim | Result |
|---|---|---|---|---|---|---|---|
| C1 | Parity-PDF, rescoped (HTML twin + evidence report) | pass (R9 misread risk) | pass | pass | medium | medium | **Shortlist** |
| C2 | Parity-PDF audit-only (no writer) | pass | pass | pass | pass | pass | Folded into C1 as its fallback |
| C3 | **Blindfolded agent: web accessibility tester** | pass | pass | pass (own demo site) | medium | pass | **Shortlist** |
| C4 | **"Before you post" video privacy guard** (consumer) | **risk**: Stage One is pass/fail, and the one-line pitch sounds like a "Simple Image Analyzer" (12 RT11) | pass (blurs, never identifies) | pass (self-filmed) | medium | pass | **Shortlist** |
| C5 | Policy-driven video redaction for records offices (old runner-up) | pass | pass | pass (staged) | medium | pass | Superseded by C4 (same engine, broader audience) |
| C6 | Consumer STEM read-aloud | pass | pass | pass | medium | medium | Out: Meta has no TTS (S-MODELS); the voice is not Meta |
| C7 | Indian defence or dual-use | **fail** ("anything political or involving war") | **fail** ("Military, warfare…") | — | — | — | **Rejected** (09 §5) |
| C8 | Government-scheme explainer, Indic languages | **risk** (basic RAG) | pass | pass | pass | weak | Out: crowded (Bhashini, Jugalbandi, Haqdarshak, named only, not researched), and a RAG core |
| C9 | Crop disease from a photo | **fail** (simple image analyzer) | pass | medium | pass | weak | Out |
| C10 | Disaster damage assessment from drone video (SAM tracks) | pass | pass (assessment, not operation) | **weak** (needs licensed disaster footage) | medium | medium | Out: rights to footage, and heavy prior art (named only) |
| C11 | Indian Sign Language translation | pass | pass | weak | **fail** (accuracy in 9 days) | fail | Out |
| C12 | Civic or road defect audit from dashcam video | pass | **risk** ("transportation technologies") | medium | medium | medium | Out: AUP adjacency |
| C13 | Health-worker assistant | **fail** (medical advice) | — | — | — | — | Out |

**Indian development needs in the end:** the strongest Indian case is **accessibility of India's digital public and financial services**, which belongs inside C3, not as a separate product:
- In *Amar Jain v. Union of India* (30 Apr 2025), the Supreme Court held digital access to be part of Article 21. One petitioner was a blind man unable to complete digital KYC (S-AMAR-JAIN, THIRD-PARTY press; judgment not read). **Read the judgment and quote it with a paragraph number before it goes in the demo** (12 RT25).
- SEBI requires regulated entities to make websites and apps accessible (IS 17802, WCAG 2.1, GIGW 3.0). The deadline is **2026-10-31**, five days from now (S-SEBI-A11Y, THIRD-PARTY; SEBI's PDF not read).
  - **Source problem (12 RT24):** S-SEBI-A11Y's headline extends only the audit. Other secondary sources say audit and remediation share Oct 31.
  - Cite SEBI's circular before use. The date passes during the build, so the pitch becomes "entities that missed 31 Oct now need evidence fast".

## 3. Shortlist deep-dives

### C3 — Blindfolded agent: "find where blind users get stuck, before they do"

**Thesis.** Two agents get the same task on a website, e.g. "complete KYC" or "book a ticket":
- a **sighted** agent, which uses screenshots;
- a **blindfolded** agent, which gets only what the screen reader says and can only press keys.

The gap between their results is the accessibility barrier, located to the step and the element. Spark proposes a fix, and the blindfolded agent re-runs to confirm it.

**Why now (CITED).**
- 95.9% of the top million home pages have detectable WCAG failures, averaging 56.1 errors per page (S-WEBAIM-2026, THIRD-PARTY summaries of WebAIM; WebAIM not fetched).
- Automated rules cover about 57% of issues by volume (S-DEQUE-57, vendor study).
- Interaction-only failures need someone to use the page.
- Legal drivers:
  - DOJ Title II covers web and documents (S-FR).
  - EAA court orders: Carrefour France was ordered in June 2026 to make its shop accessible (S-EAA-ENF, THIRD-PARTY).
  - SEBI's 2026-10-31 deadline.
- About 1.3 billion people have a significant disability (S-WHO-DISAB, via a mirror of the WHO fact sheet).

**Prior art (honest; this is crowded academically).**

| Work | What it does | Gap left for us (hypothesis) |
|---|---|---|
| TaskAudit, CHI 2026 (S-TASKAUDIT) | Vision-free agents run tasks through a **TalkBack proxy** on Android. Finds 48 errors on 54 screens vs 4–20 for checkers; 96% task success when no errors | Mobile only; proxy, not a real screen reader; no fix loop |
| AXNav, CHI 2024 (S-AXNAV) | LLM replays manual tests with VoiceOver on iOS and produces a video | iOS; replays tests rather than measuring a gap |
| Agentic web auditing, arXiv 2609.09379 (S-AGENTIC-AUDIT) | One VLM agent per WCAG criterion (40). 86% recall vs axe-core 36%, precision 56% | Criterion audit, not task parity; sighted agents |
| AAA, AAAI 2026 (S-AAA-AUDIT) | MLLM copilots across WCAG-EM steps | Audit workflow, not a blindfolded user |
| TestSprite, BrowserStack Issue Detection Agent, axe DevTools AI (S-TESTSPRITE, S-BROWSERSTACK-A11Y) | Commercial AI accessibility testing, with screen-reader claims | Claims only; not checked whether a real screen reader drives an agent |
| **Added after the red team (11 §3, RT14; on 11's evidence, not re-fetched):** ScreenAudit (mobile; recall 69.2%, precision 71.3% vs a checker's 31.3%); "Are We There Yet?" (arXiv 2609.00524: computer-use agents for 8 blind users were unreliable); UXAgent (arXiv 2502.12561); an MCP accessibility-tree agent (arXiv 2608.24898); Scott Logic 2024 (LLM driving a screen reader); Assistiv Labs (cloud screen-reader automation); W3C AT Driver; Guidepup's virtual screen reader | LLM agents on accessibility trees or screen readers | **With the proxy alone, C3 is "an LLM agent reading the AX tree", which is common.** Novelty rests on the real NVDA log, the sighted/blind gap and the fix loop together. If W1 fails, C3 is dropped (§5) |

- **What we would add.** All four are hypotheses, each with its falsifier.
  1. A **real NVDA speech log** as the agent's only input and as OBSERVED evidence. Falsifier: probe W1 fails, i.e. Guidepup cannot capture NVDA speech in 3 of 3 attempts on the Windows 11 Home host, against our own local page. NVDA runs on the host, not in a VM: the VM rule covers Wonder computer use (12 RT15).
  2. A **differential sighted/blind gap**, so barriers are tied to a task rather than to rules. Falsifier: the blindfolded agent fails control pages more than 10% of the time, so the gap is agent noise.
  3. A **closed fix loop**: patch, re-run, confirm. Falsifier: fewer than half of the proposed fixes make the blind run succeed.
  4. **Hindi and Indian flows**. NVDA's Hindi voices are UNVERIFIED.
- **Meta on the critical path.**
  - Spark is the blindfolded agent: text observations, tool calls for keys.
  - Wonder (computer use, S-CU) is the sighted agent and is also eligible for the Creative bonus.
  - Spark localises the failing element and writes the fix.
  - Glimmer is optional, as a local second model (L2).
- **Build (provisional).**
  - Playwright (Apache-2.0) as the browser.
  - Speech: a Chromium accessibility-tree linearizer as a fast proxy, plus NVDA through Guidepup (MIT; S-GUIDEPUP; Windows only) for the evidence runs. Proxy fidelity is measured against NVDA.
  - Interfaces: a CLI and an HTML report. A GitHub Action needs a Windows runner with NVDA, so it is dropped until tested (12 RT15).
  - A fictional demo site: an "eKYC" flow with no real brand, in an accessible control version and a seeded version.
- **Evaluation (designable now).**
  - Seed N barriers of K types, static and interaction-only, into the demo site.
  - **Recall and precision vs axe-core**, which we run ourselves.
  - False-barrier rate on the control site.
  - Proxy–NVDA agreement.
  - Fix-loop success.
  - Cost per task.
- **Demo spine.** A blind man went to India's Supreme Court because he could not finish KYC. We blindfolded an AI and gave it the same task: hear NVDA, watch the agent get stuck at an unlabeled button, see the sighted agent finish in 12 steps, apply Spark's one-line fix, re-run, and hear it succeed. Then honest numbers: recall vs axe-core, and cost per run.
- **Risks.**
  1. Agent flakiness masquerades as barriers. The control-site gate addresses this.
  2. Running agents on third-party sites raises ToS and legal questions. Only our own sites, or a user's site with an ownership confirmation.
  3. NVDA automation is Windows-only, and is UNTESTED on this host (W1).
  4. Wonder cost is $4/$20 (S-PRICING), so the sighted agent runs only for evidence.
  5. The novelty is in combining known parts, not in a new primitive.

### C4 — "Before you post": a privacy guard for videos (consumer)

- **Thesis.** You upload a reel before posting.
  - Spark watches it the way a stalker would and lists every clue to who you are or where you live: a house number, a street sign, a school logo on a uniform, a parcel label, a car plate, a screen showing a name, a reflection, a landmark.
  - **It never outputs a location guess, the clue text or timestamps.** The output is the redacted video plus a risk level and counts per category, e.g. "3 location clues blurred" (12 RT12). Clues are concrete objects only, because SAM takes "a short noun phrase that names one concrete object" (12 RT02).
  - SAM 3.1 tracks each clue through the video by text prompt, and the app blurs it.
  - A **full-frame leak check** inspects every output frame.
  - Voice Transcribe flags spoken names and addresses by turn. There are no word-level timestamps (S-MODELS), so audio is flagged, not bleeped precisely.
- **Why now (CITED).**
  - GeoSpy geolocated photos from scene content in seconds and was publicly usable until 404 Media's report. Users asked it to track specific women (S-GEOSPY, THIRD-PARTY).
  - VLM-GEOPRIVACY (Feb 2026) reports that frontier models infer street-level locations from casual photos and often over-disclose (S-VLM-GEOPRIV).
  - VLMs infer private attributes from images at up to 77.6% accuracy (S-VLM-PAI).
  - SAM 3.1 (March 2026) added multi-object tracking (F14; THIRD-PARTY, and the API docs state no track schema). It costs **$0.20 per 1K frames**, but SAM segments one object type per request (S-SEG). Cost = clue types × fps × seconds × $0.0002. A 60 s clip with 6 types costs $2.16 at 30 fps, $0.72 at 10 fps and $0.36 at 5 fps (computed; corrected from "$0.36 at 30 fps", 12 RT01).
- **Prior art.**

| Work | Covers | Gap (hypothesis) |
|---|---|---|
| YouTube Studio Face Blur plus manual Custom Blur with tracking (S-YT-BLUR) | Faces automatically; anything else by hand | No semantic clue detection |
| BGBlur, YouBlur (S-BGBLUR, vendor) | Faces and licence plates automatically | Fixed classes only |
| Axon, Pimloc, Brighter AI (file 03) | B2B faces, plates, screens | Enterprise; fixed classes |
| Attack and benchmark research (S-VLM-PAI, S-VLM-GEOPRIV, THIRD-PARTY aggregator); image shielding (arXiv 2512.18264) | Measures the threat | No consumer video defence found. "Not found" ≠ absent. |
| Lookr: AI Photo Privacy (S-LOOKR; added after the red team) | Pre-share scan of **photos** for "faces, plates, signs, logos, and content-policy risks", with AI replacement; $4.99/mo | Photos only; no cross-frame inference |
| Imago Obscura (S-IMAGO, arXiv 2505.20916) | Pre-share image-privacy co-pilot: context-relevant risks, then blur, inpaint or replace | Images only; research prototype |
| DataCamp "SAM3 Tutorial: Build a Privacy Filter"; Meta's Segment Anything Playground effects (11 §3, THIRD-PARTY, not re-checked) | Text-prompted blur of faces, plates and screens in images and MP4 | **The blur itself is a tutorial.** What is left is cross-frame inference plus the leak check |

- **What we would add.** Each item is a hypothesis with its falsifier.
  1. **Open-vocabulary, reasoning-based clue detection across frames**, e.g. a partial sign in one frame combined with a shop name in another. Falsifier: probe V2 fails (fewer than 5 of 6 staged props, §5).
  2. **Tracking that holds on handheld phone video**. Falsifier: after redaction, a native-fps full-frame check finds any readable planted prop (12 RT03; the earlier "5% of frames" bar contradicted "0 visible").
  3. **Guard-rail by design.** The system outputs no clue text, no timestamps and no location guess (12 RT12). Falsifiers:
     - red-team prompts extract a location or a clue list;
     - a third party's reel run through it yields a usable map. The residual risk: comparing output with original shows where the blur went.
  4. **The Spark → SAM instance handoff (added; 12 RT02).** SAM documents box and point prompts. Spark's video page states no timestamps or boxes. Falsifier: probe V1 or V2 fails (§5).
- **Meta on the critical path.** SAM 3.1 (tracking), Spark video understanding (S-VIDEO, mp4 input) and Voice Transcribe are all central. The SAM blur alone is Meta's own showcase (12 RT09), so the tooling claim rests on Spark's cross-frame inference.
  - **Strategic fit (INFERENCE):** a "privacy check before you post" is a natural Instagram or Facebook feature, and India is Instagram's largest market at about 480–555M users (S-IG-INDIA, THIRD-PARTY estimates).
- **Build (provisional).** ffmpeg (licence to check per build), OpenCV (Apache-2.0) for mask rendering, the SAM 3.1 API (video input, at least 50 frames per request), and a mobile-friendly web upload with a review scrubber.
- **Evaluation.**
  - Clips with **staged props only** (fake house numbers and plates, a fictional crest), filmed in a neutral place with no bystanders and a consent log, give known ground truth (12 RT13). Unplanted clues are judged by the other developer before scoring (12 RT23).
  - Measures:
    - clue recall and precision;
    - frame coverage, with a human-labelled frame sample (L4) and an automated full-frame check (L3);
    - leak count;
    - false blurs;
    - cost per minute.
  - Baseline: face-and-plate blur only. The "semantic gap" is the number of clues it misses.
- **Demo spine.**
  - A cheerful 30-second "morning routine" reel.
  - Cut to: "Here's what a stranger could piece together." Regions light up as SAM tracks them, and a risk meter shows that two clues in different frames combine. No clue text is shown (12 RT12). The first 10 s must show this cross-frame inference (12 RT11).
  - One tap and everything is blurred. The leak check runs every frame: 0 readable. Cost the demo clip separately with the RT01 formula (12 RT40).
  - Close: "AI made finding you easy. We made it hard again."
- **Risks.**
  1. **Irony:** a privacy tool uploads your video to a cloud model. Mitigations:
     - say so plainly;
     - Standard mode only, never Contributor;
     - SAM 3 open weights for local use in H2 (needs a GPU, Q5).
  2. A judge reads it as a "simple image analyzer", and Stage One is pass/fail. Answer: cross-frame reasoning plus tracking plus a leak check is a pipeline, not a classifier. Measured by the V4 read test; the demo's first 10 s carry the cross-frame inference (12 RT11).
  3. SAM API behaviour on small text, motion blur and occlusion is UNTESTED.
  4. Audio is turn-level only.
  5. No regulatory deadline. The why-now is a threat, not a mandate.
  6. The Spark → SAM handoff is undocumented on Spark's side (V1, V2).
  7. **C5 shares this SAM engine.** If V1 or V3 fails, C5 fails too (12 §2).

### C1 — Parity-PDF, rescoped (from 08 and 09)

| Aspect | Rescoped Parity-PDF |
|---|---|
| Product | Tagged PDF (math as alt text under PDF/UA-1) + MathML HTML twin + evidence report with evidence classes + human lane |
| Fallback | Audit-only: an evidence report on any PDF, no writer |
| Strengths | A dated deadline; a clear buyer; most research already done (files 02–08) |
| Weaknesses after the audit | No "proof"; MathML only in the twin; Allyant overlap; E3 cannot support a competitive claim; the deadline is contested (09 §1.1); the demo is harder to make "wow" for a general audience |

## 4. Scores (INFERENCE, ±1 per criterion; computed with `python -I`)

**Revised (12 §3), scored against the official rubric wording (guide p8):**

| Candidate | Impact 30 | Meta 25 | Depth 20 | Demo 25 | Weighted | Change |
|---|---|---|---|---|---|---|
| C3 Blindfolded agent | 8.0 | 8.0 | 8.5 | 8.5 | **8.23** | Demo −0.5: a fictional eKYC site has less mass appeal than a reel |
| C4 Privacy guard | 7.5 | 8.0 | 8.0 | 9.0 | **8.10** | Impact −0.5 (RT08), Meta −1.0 (RT09) |
| C5 Redaction, B2G | 7.0 | 8.5 | 7.5 | 9.0 | 7.98 | none |
| C1 Parity-PDF rescoped | 7.5 | 7.0 | 8.0 | 7.5 | 7.48 | none |

- C3 and C4 are 0.13 apart, inside the noise, so the scores do not decide.
- The scores miss two risks, which the probes in §5 test directly: C4's Stage One misread (RT11) and C3's NVDA dependency (RT14).

**First version (superseded; kept as history):**

| Candidate | Impact 30 | Meta 25 | Depth 20 | Demo 25 | Weighted | Equal |
|---|---|---|---|---|---|---|
| C4 Privacy guard | 8.0 | 9.0 | 8.0 | 9.0 | **8.50** | **8.50** |
| C3 Blindfolded agent | 8.0 | 8.0 | 8.5 | 9.0 | 8.35 | 8.38 |
| C5 Redaction, B2G (old runner-up) | 7.0 | 8.5 | 7.5 | 9.0 | 7.98 | 8.00 |
| C1 Parity-PDF rescoped | 7.5 | 7.0 | 8.0 | 7.5 | 7.48 | 7.50 |

**Reading.**
- C4 and C3 are **0.15 apart, well inside the noise**, and the scores alone should not decide between them.
- Both beat rescoped Parity-PDF by about 0.9, which is roughly one point per criterion. That is the size of gap a reasonable judge could reverse, so it is a direction, not a verdict.

**Why the ranking might be wrong.**
- C3's Impact could be higher than C4's: it rests on legal mandates, whereas C4 rests on a threat.
- C4's "simple image analyzer" misread could cost it Stage One.

## 5. Recommendation (needs the user's MCQ answer)

- **Pivot away from Parity-PDF** to C3 or C4.
- **No lean between them.** The first version leaned C4 and named a "desk favourite"; both were withdrawn after the red team (12 §1). The original spike table (S-W, S-V) is in commit `c00bbda`.
- **Day-1 feasibility probes** look for blocking failures; they do not rank the candidates. Day 1 is **2026-10-27**: the guide's "Building period: Oct 27 – Nov 4" (p4). The earlier "2026-10-28" came from 07 §5, which was wrong (12 RT07).
- Pass criteria are pre-registered here and in `proposals/docs/ledger/PLAN.md`. They are UNAPPROVED until the user's MCQ answer.

| Probe | Owner | Setup (time-box) | Blocking pass criteria | Cap |
|---|---|---|---|---|
| **V1** instance (C4) | Dev A | One staged 30 s clip with two fake house-number plates; one is marked sensitive (≤ 2 h, filming included) | SAM masks the marked plate and never the other one, in all 30 human-checked frames where either is visible, by at least one route:<br>(a) a box from a user tap;<br>(b) a box from Spark on one frame;<br>(c) a class prompt plus a Spark crop filter | $1 |
| **V2** grounding (C4) | Dev A | One staged 30 s clip with 6 concrete props, in a neutral place | Spark lists ≥ 5 of the 6 with a time within ±1 s of the truth, in 2 of 3 runs, and with ≤ 1 non-clue listed per run | $1 |
| **V3** cost and leak (C4) | Dev A | V2's clip through the whole pipeline, at a tracking fps stated before the run | Billed cost ≤ $1.00 per 30 s clip, from the usage record. A native-fps full-frame check finds 0 readable planted props, confirmed by Dev B | $1 |
| V4 read test (C4) | Dev B | 3 people outside the team hear the one-sentence pitch | Reported, not blocking: how many call it an image analyzer | $0 |
| **W1** NVDA capture (C3) | Dev B | NVDA + Guidepup on the Windows 11 Home host, against our local page, on a 10-step keyboard task (≤ 2 h) | A complete speech log is captured in 3 of 3 attempts | $0 |
| **W2** blind finding (C3) | Dev B | An accessible control page and a seeded page with 3 interaction-only barriers, written by Dev A. Run axe-core first. | Control: the task completes in ≥ 4 of 5 runs.<br>Seeded: at least 1 barrier that axe-core misses is found and located in ≥ 2 of 3 runs | $2 |
| W3 fix loop (C3) | Dev B | Spark patches one W2 barrier | Reported, not blocking: whether the blind re-run succeeds | in W2 |

- **Sample sizes are small.** The probes answer go/no-go only and report Wilson 95% intervals (e.g. 3/3 is compatible with a true rate well below 1). The fixture for each probe is written by the developer who does not run it (12 RT05).
- **Decision rule.** A candidate passes when all of its bold (blocking) probes pass.

| Outcome | Then |
|---|---|
| Only C3 passes | Build C3. |
| Only C4 passes | Build C4. |
| Both pass | The user chooses from the probe results. No lean is written in advance. |
| Neither passes | If V1 and V3 passed and only V2 failed: C5 is open. Otherwise: C1 audit-only. |
| **INSUFFICIENT EVIDENCE** (credits not posted, or a probe could not run) | No default candidate. See below. |

- **When evidence is insufficient:**
  - Run every $0 part: W1, the axe-core baseline and the fixture filming.
  - V1 can run on SAM 3 open weights if a GPU is available (Q5) or partner GPU credits arrive (guide p6–p7).
  - Hard stop at the end of 2026-10-28 IST. The user then decides, and it is logged as "decided on insufficient evidence", naming the untested risk and adding a kill check on 2026-10-30.
- **Cost and time.** At most $6 of granted credit. Each developer spends ≤ 5 h on 2026-10-27, fixtures included: ≤ 10 h of the 144 build hours (2 developers × 9 days × 8 h), so 6.9% (computed with `python -I`). Code written before 2026-10-27 is throwaway and is not shipped (new-work rule, p4).

## 6. What this changes elsewhere (only once a pivot is approved)
- Files 04, 06 and 08 get a new finalist brief, new experiments and a new verdict. The Parity-PDF material is kept as history.
- `proposals/docs/ledger/FEATURES.json` is replaced with the chosen product's acceptance tests.
- The governance drafts need no change: they are product-agnostic, apart from the AGPL/PyMuPDF line and the Wonder VM rule.
