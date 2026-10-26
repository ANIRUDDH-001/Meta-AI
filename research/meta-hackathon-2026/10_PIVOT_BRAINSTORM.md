# 10 — Pivot brainstorm (UNAPPROVED)

- **Written:** 2026-10-26T16:58Z (`date -u`).
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
| C4 | **"Before you post" video privacy guard** (consumer) | pass ("simple image analyzer" misread risk) | pass (blurs, never identifies) | pass (self-filmed) | medium | pass | **Shortlist** |
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
- In *Amar Jain v. Union of India* (30 Apr 2025), the Supreme Court held digital access to be part of Article 21. One petitioner was a blind man unable to complete digital KYC (S-AMAR-JAIN, THIRD-PARTY press; judgment not read).
- SEBI requires regulated entities to make websites and apps accessible (IS 17802, WCAG 2.1, GIGW 3.0). The audit and remediation deadline is **2026-10-31**, five days from now (S-SEBI-A11Y, THIRD-PARTY; SEBI's PDF not read).

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

- **What we would add.** All four are hypotheses, each with its falsifier.
  1. A **real NVDA speech log** as the agent's only input and as OBSERVED evidence. Falsifier: Guidepup cannot capture NVDA speech reliably in our VM.
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
  - Interfaces: a CLI, a GitHub Action and an HTML report.
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
  3. NVDA automation is Windows-only.
  4. Wonder cost is $4/$20 (S-PRICING), so the sighted agent runs only for evidence.
  5. The novelty is in combining known parts, not in a new primitive.

### C4 — "Before you post": a privacy guard for videos (consumer)

- **Thesis.** You upload a reel before posting.
  - Spark watches it the way a stalker would and lists every clue to who you are or where you live: a house number, a street sign, a school logo on a uniform, a parcel label, a car plate, a screen showing a name, a reflection, a landmark.
  - **It never outputs a location guess.**
  - SAM 3.1 tracks each clue through the video by text prompt, and the app blurs it.
  - A **full-frame leak check** inspects every output frame.
  - Voice Transcribe flags spoken names and addresses by turn. There are no word-level timestamps (S-MODELS), so audio is flagged, not bleeped precisely.
- **Why now (CITED).**
  - GeoSpy geolocated photos from scene content in seconds and was publicly usable until 404 Media's report. Users asked it to track specific women (S-GEOSPY, THIRD-PARTY).
  - VLM-GEOPRIVACY (Feb 2026) reports that frontier models infer street-level locations from casual photos and often over-disclose (S-VLM-GEOPRIV).
  - VLMs infer private attributes from images at up to 77.6% accuracy (S-VLM-PAI).
  - SAM 3.1 (March 2026) added multi-object tracking (F14) at **$0.20 per 1K frames**, so a 60-second clip at 30 fps costs about $0.36 (S-PRICING, computed).
- **Prior art.**

| Work | Covers | Gap (hypothesis) |
|---|---|---|
| YouTube Studio Face Blur plus manual Custom Blur with tracking (S-YT-BLUR) | Faces automatically; anything else by hand | No semantic clue detection |
| BGBlur, YouBlur (S-BGBLUR, vendor) | Faces and licence plates automatically | Fixed classes only |
| Axon, Pimloc, Brighter AI (file 03) | B2B faces, plates, screens | Enterprise; fixed classes |
| Attack and benchmark research (S-VLM-PAI, S-VLM-GEOPRIV); image shielding (arXiv 2512.18264) | Measures the threat | No consumer video defence found. "Not found" ≠ absent. |

- **What we would add.** Each item is a hypothesis with its falsifier.
  1. **Open-vocabulary, reasoning-based clue detection across frames**, e.g. a partial sign in one frame combined with a shop name in another. Falsifier: clue recall below 0.75 on planted clues.
  2. **Tracking that holds on handheld phone video**. Falsifier: the leak check finds a clue visible in more than 5% of the frames where it appears.
  3. **Guard-rail by design.** The system lists clues but never guesses the location, so it cannot be turned into a stalking tool. Falsifier: red-team prompts extract a location.
- **Meta on the critical path.** SAM 3.1 (tracking), Spark video understanding (S-VIDEO, mp4 input) and Voice Transcribe are all central. This is the highest Meta-tooling fit of any candidate.
  - **Strategic fit (INFERENCE):** a "privacy check before you post" is a natural Instagram or Facebook feature, and India is Instagram's largest market at about 480–555M users (S-IG-INDIA, THIRD-PARTY estimates).
- **Build (provisional).** ffmpeg (licence to check per build), OpenCV (Apache-2.0) for mask rendering, the SAM 3.1 API (video input, at least 50 frames per request), and a mobile-friendly web upload with a review scrubber.
- **Evaluation.**
  - Self-filmed clips with planted clues give known ground truth.
  - Measures:
    - clue recall and precision;
    - frame coverage, with a human-labelled frame sample (L4) and an automated full-frame check (L3);
    - leak count;
    - false blurs;
    - cost per minute.
  - Baseline: face-and-plate blur only. The "semantic gap" is the number of clues it misses.
- **Demo spine.**
  - A cheerful 30-second "morning routine" reel.
  - Cut to: "Here's what a stranger learns." Spark lists 7 clues; each lights up as SAM tracks it.
  - One tap and everything is blurred. The leak check runs every frame: 0 visible.
  - Close: "AI made finding you easy. We made it hard again."
- **Risks.**
  1. **Irony:** a privacy tool uploads your video to a cloud model. Mitigations:
     - say so plainly;
     - Standard mode only, never Contributor;
     - SAM 3 open weights for local use in H2 (needs a GPU, Q5).
  2. A judge reads it as a "simple image analyzer". Answer: cross-frame reasoning plus tracking plus a leak check is a pipeline, not a classifier.
  3. SAM API behaviour on small text, motion blur and occlusion is UNTESTED.
  4. Audio is turn-level only.
  5. No regulatory deadline. The why-now is a threat, not a mandate.

### C1 — Parity-PDF, rescoped (from 08 and 09)

| Aspect | Rescoped Parity-PDF |
|---|---|
| Product | Tagged PDF (math as alt text under PDF/UA-1) + MathML HTML twin + evidence report with evidence classes + human lane |
| Fallback | Audit-only: an evidence report on any PDF, no writer |
| Strengths | A dated deadline; a clear buyer; most research already done (files 02–08) |
| Weaknesses after the audit | No "proof"; MathML only in the twin; Allyant overlap; E3 cannot support a competitive claim; the deadline is contested (09 §1.1); the demo is harder to make "wow" for a general audience |

## 4. Scores (INFERENCE, ±1 per criterion; computed with `python -I`)

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
- **Decide between them with a Day-1 spike, not with scores** (answers audit §7).
- Each developer spikes one candidate on Day 1 (2026-10-28 per file 07 §5; 2026-10-27 if approvals and credits are in place by then). The pass criteria below are pre-registered here:

| Spike | Fixture | Pass (all must hold) | Cost cap |
|---|---|---|---|
| **S-W (C3)** | Our seeded demo page: 5 barriers, 3 of them interaction-only, plus an accessible control. Proxy speech only. | (a) Control task success ≥ 8/10 runs. (b) ≥ 3 of the 5 seeded barriers found in ≥ 2 of 3 runs. (c) ≤ 1 false barrier on the control across 10 runs. | $3 |
| **S-V (C4)** | 3 self-filmed clips of 30–60 s with 6 planted clues each (18 total) | (a) Spark clue recall ≥ 14/18, with ≤ 3 false clues per clip. (b) SAM masks cover the clue in ≥ 95% of hand-checked frames where it is visible (100 frames per clip). (c) Each clip costs ≤ $0.50. | $3 |

- **Decision rule.**
  - One spike passes: build that one.
  - Both pass: the user chooses. My lean is **C4** for mass appeal and Meta fit, or C3 for legal-driver impact and the Indian story.
  - Neither passes: fall back to C5 or C1 audit-only, decided that evening.
- **No credits by end of Day 1:** a desk decision, recorded as such. Desk favourite: **C4**.
- **Cost.** At most $6 of granted credit. Each developer spends 6–8 h on Day 1: 12–16 h of the 128 build hours (2 developers × 8 days, 2026-10-28 to 11-04, × 8 h), so 9.4–12.5% (computed with `python -I`).

## 6. What this changes elsewhere (only once a pivot is approved)
- Files 04, 06 and 08 get a new finalist brief, new experiments and a new verdict. The Parity-PDF material is kept as history.
- `proposals/docs/ledger/FEATURES.json` is replaced with the chosen product's acceptance tests.
- The governance drafts need no change: they are product-agnostic, apart from the AGPL/PyMuPDF line and the Wonder VM rule.
