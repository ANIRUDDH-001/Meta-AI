# 02 — Opportunity landscape (problem-first)

Method: I started from customer problems and priced workflows, and only then asked where a Meta model *changes what a product can do*. That covers 13 hypotheses across 11 sectors. Nine were researched with evidence searches. Four were screened at desk stage with **no** evidence search (LEDGER F36), and they are marked that way: their elimination reasons are INFERENCE only. Source IDs refer to [`sources.jsonl`](sources.jsonl).

## 1. Longlist at a glance

| # | Hypothesis | Sector | Demand evidence | Meta changes the product? | Result |
|---|---|---|---|---|---|
| H1 | Verifiable accessibility remediation for STEM PDFs | Public sector / higher-ed compliance | **Strong**: dated legal trigger plus priced manual work | Yes: whole-document vision + 1M context, an agent that tests with a screen reader, chart region checks | **Finalist 1** |
| H2 | Audio description (AD) for instructional video | Public sector / media accessibility | Strong: WCAG 1.2.5 plus public per-minute prices | Partly: Spark video works, but Meta has no TTS | Finalist 3 |
| H3 | Policy-driven redaction of records-request video | Justice / public records / privacy | Strong: staff-hour and fee data | Yes: SAM 3.1 text-prompted tracking makes "redact what the policy says" possible | Finalist 2 |
| H4 | Fisheries electronic-monitoring (EM) review | Environment | Medium: review $/day | Yes (video) | Eliminated: **data access** |
| H5 | Lab animal behavior scoring | Life science | Medium | Weak: benchmark says MLLMs are modest | Eliminated: **capability evidence negative** |
| H6 | Robot demonstration data QA | Robotics / physical AI | Medium: papers call curation a bottleneck | Yes (video + reasoning) | Finalist 4 |
| H7 | Video → SOP / work instructions | Manufacturing | Vendor claims only | Yes | Eliminated: **crowded, no falsifiable edge** |
| H8 | Analog gauge digitization | Manufacturing | Vendor retrofit prices | Marginal | Eliminated: **feature-level; "simple image analyzer" risk** |
| H9 | Facility asset register from walkthrough video | Facilities | Thin (vendor blogs) | Yes | Eliminated: **thin demand evidence** |
| H10 | Construction progress from site video | Construction | Not searched | — | Desk-screened out (INFERENCE: established category) |
| H11 | Insurance claim video triage | Insurance | Not searched | — | Desk-screened out (INFERENCE: established category, sensitive data) |
| H12 | Bug-report video → repro steps | Software | Not searched | — | Desk-screened out (user deprioritized dev tools; INFERENCE: crowded) |
| H13 | Prior-authorization packet assembly | Healthcare admin | Not searched | — | Desk-screened out (medical anti-project adjacency R9; needs PHI) |

## 2. Hypothesis cards (researched)

### H1 — Verifiable accessibility remediation for STEM PDFs → Finalist 1 ("Parity", working name)
- **User / buyer / job.** Users: accessibility coordinators, document-remediation staff, instructional designers. Buyer: the central IT accessibility office or procurement at public universities, community colleges, and state/local agencies. Job: turn inaccessible course and public PDFs into documents a screen-reader user can actually use, and be able to show that they are.
- **Trigger and frequency.** Title II compliance dates are **2027-04-26** (population ≥50K) and **2028-04-26** (smaller entities and special districts) (S-FR, 91 FR 20902). Course materials have no exception (S-TXST, S-PSU). The work recurs every term as new uploads arrive. The cadence is INFERENCE.
- **Cost evidence.**
  - Manual remediation: $3–4/page at OSU, with "hundreds of thousands" of PDFs (S-ASU).
  - Vendor list price: $5.00/page plus $3.00 for OCR (S-OSU-SUPPLIERS).
  - A vendor blog quotes $5–25/page (S-VENNGAGE).
  - AI pipelines: about $0.0013/page plus Adobe fees (S-ASU) and about $0.061/page (S-CNI).
  - Number of covered entities and total market size: **UNKNOWN**.
- **Workarounds.**
  - Manual tagging in Acrobat.
  - Outsourcing to vendors.
  - LMS alternative formats (Ally, Panorama).
  - Doing nothing until a complaint arrives (INFERENCE).
- **Why now.**
  1. The deadline is fixed.
  2. The regulator itself says "generative AI, does not yet reliably automate the remediation of inaccessible content at scale" (S-FR, 91 FR 20907). A Congressman made the same point about STEM specifically (91 FR 20905). This is a **trust gap**, not a capability gap.
  3. PDF 2.0 + MathML is now readable by NVDA + MathCAT (S-PDFA-MATH).
  4. Muse Spark reads PDFs and images with 1,048,576 tokens of context (S-MODELS). It reports CharXiv Reasoning 86.4 (S-VB, THIRD-PARTY).
  5. Muse Wonder can drive a desktop (S-CU), so it can *test* a document the way a blind user would.
- **Negative signals.**
  - The market is crowded (file 03).
  - Incumbents already claim STEM handling (F21) and math-to-MathML (F31, F32).
  - Allyant already sells a per-PDF validation report pitched as Title II compliance evidence (S-ALLYANT-AI). A report alone is not new.
  - CNI reports math and figures are still hard even for AI pipelines (S-CNI).
  - AI alt text can lower task success (S-SILKTIDE-ALT; vendor, unverified).
- **Feasibility.**
  - Public data: CC-licensed arXiv papers, with the license checked per file. veraPDF is OSS. pikepdf is MPL-2.0.
  - The riskiest part is writing a valid tagged PDF (K3).
- **Demo.** See file 04 §1.6. Everything shown is live: the untagged→tagged run, the veraPDF output, and the screen-reader playback.
- **Kill evidence.**
  - K1–K5 (file 07).
  - Coordinators say per-check proof would not change their purchasing (E8).
  - An incumbent already attaches evidence to the human-judgment checks. Allyant's public pages show pass/fail/warning counts and checkpoints, but no evidence per check (S-ALLYANT-AI). Their trial would settle it.
- **Why it might be fundamentally unattractive.** Edu procurement is slow and often bundled into the LMS (INFERENCE). Incumbents can add LLM checks (file 07 red-team).

### H2 — Audio description for instructional video → Finalist 3
- **User / buyer.** Media services and accessibility offices.
- **Trigger.** WCAG 2.1 SC 1.2.5 (AA) requires AD for prerecorded synchronized video (S-W3C-125), and Title II applies it.
- **Cost evidence.**
  - 3Play list prices: $9 (standard) / $14 (extended) per minute synthesized; $18 / $35 with a voice artist.
  - Harvard negotiated $7 / $11; Arizona $7 + $4 (S-3PLAY).
- **Competitors.**
  - Verbit AI AD, marketed for Title II, sold standalone or in a bundle, with optional human review (S-VERBIT).
  - Ai-Media LEXI AD (S-AIMEDIA).
  - Recap (S-RECAP).
  - Audible Sight and ViddyScribe: **UNKNOWN** (F35).
- **Meta fit.**
  - Spark video understanding (S-VIDEO).
  - Voice Transcribe turn timestamps can find dialogue gaps, but it has no word-level timestamps (S-MODELS).
  - **No Meta TTS**, so the voice must come from somewhere else. That weakens the Meta-tooling score.
- **Kill evidence.** The incumbents have already shipped AI AD. A differentiator would need a measured quality gap, and none is evidenced.

### H3 — Policy-driven redaction of records-request video → Finalist 2
- **User / buyer.** Police records units, public-records officers, and GDPR data-subject-access-request (DSAR) teams (S-FACIT).
- **Cost evidence.**
  - 1–1.5 staff hours per video hour in Madison (S-REDACT-COST).
  - 4–6 h per hour estimated by the Canadian government (S-ISED).
  - Fees of $0.73–0.98/min and an $80K/yr redaction position (S-REDACT-COST).
  - Axon claims "up to eight hours" per hour (S-AXON).
- **Competitors.**
  - Axon Redaction Assistant: faces, plates and screens, plus an exemption log; bundled into US OSP 7+ (S-AXON).
  - Pimloc Secure Redact: audio NER, faces, plates, on-screen text (S-PIMLOC).
  - Facit (S-FACIT).
  - Veritone and CaseGuard: UNKNOWN (F35).
- **Meta fit (strong).**
  - SAM 3.1 takes text prompts and returns tracked masks in video (S-SEG). That turns redaction from fixed categories into **policy language**, e.g. "the child in the red jacket", "papers on the desk".
  - Voice Transcribe handles audio PII. Spark writes the exemption log.
- **Economics (computed from S-PRICING).** SAM costs $0.20 per 1K frames. One hour at 30 fps (108K frames) is $21.60; sampled at 5 fps it is $3.60, which is below manual staff cost.
- **Kill evidence.**
  - Axon bundles redaction "automatically" into US OSP 7+, so the largest buyers already have it.
  - Real footage is sensitive, so the demo needs staged footage.
  - SAM tracking on shaky bodycam footage is **UNKNOWN**.

### H4 — Fisheries EM review → eliminated (data access)
- **Evidence.**
  - EM review costs $300–350/day, and manual review can take months (S-FISH).
  - Alaska's FishVue project is budgeted at $485K. CatchVision claims "up to 80%" faster review (claim).
  - EU remote electronic monitoring applies to high-risk vessels over 18 m, and to small-scale vessels from 2028-01-10 (THIRD-PARTY search summary).
- **Killed by:** no public labeled EM footage we have rights to (R6), the need for species-ID expertise, and agency buyers.

### H5 — Lab animal behavior scoring → eliminated (capability)
- **Evidence.**
  - Manual scoring takes several times the video duration (THIRD-PARTY search summary).
  - Rodent-Bench (S-RODENT) shows MLLM scoring is modest.
  - Entrenched open-source tools: DeepLabCut, SLEAP, SimBA, Noldus.
- **Killed by:** negative capability evidence for the very model class we would rely on.

### H6 — Robot demonstration data QA → Finalist 4
- **Evidence.** Papers describe curation as a manual or heuristic bottleneck. Prior art:
  - DQA framework, 85.7% recall (S-DQA)
  - FailBench, 2026-09 (S-FAILBENCH)
  - robot-episode-labeler, F1 0.629 (S-REL)
- **Gaps.** Commercial platforms (Encord, Scale, Voxel51) are UNKNOWN (F35).
- **Meta fit.** Spark video reasoning plus SAM tracks for gripper/object contact.
- **Weak because:**
  - The buyer set is small: robotics labs and physical-AI startups (INFERENCE).
  - Prior art is heavy.
  - Ground truth requires labeled episodes.

### H7 — Video → SOP → eliminated (crowded)
Vendors claim this already: Siemens Opcenter, Docsie, Guidde, Synthesia (S-SOP). No falsifiable edge was found.

### H8 — Analog gauge digitization → eliminated (feature-level)
- Products already exist: Roboflow, iFactory, Surplus (S-GAUGE).
- It is a feature, not a company.
- It risks the "Simple Image Analyzers" anti-project (R9).

### H9 — Facility asset register from video → eliminated (thin evidence)
CMMS onboarding cost of $5K–80K comes only from vendor blogs (S-CMMS). Buyers and competitors are UNKNOWN.

## 3. Cross-cutting signals that shaped the pick

- **Verification is what the market lacks.** Gartner expects over 40% of agentic AI projects to be canceled by end-2027 over cost, unclear value and weak risk controls (S-GARTNER). The DOJ says gen-AI remediation is not yet reliable (S-FR). Both point the same way: a product whose output carries **checkable evidence** answers the objection buyers are actually raising. That is INFERENCE from two primary sources.
- **Accessibility structure is agent structure.** OpenAI says ChatGPT Atlas reads ARIA roles, names and states (S-OPENAI-ATLAS). There is a counter-view (S-ROSELLI). INFERENCE: a properly tagged document is also machine-navigable, which is a horizon-3 tailwind, not a competition claim.
- **Information-equivalence is unmeasured.** Two searches found no QA-based metric asking "can a non-visual reader answer the same questions as a sighted reader?" (F34). Absence is not proven, so novelty stays a hypothesis.

## 4. What is still unknown about demand

- No customer contact has been made (none is authorized). There is no willingness-to-pay data beyond list prices.
- How many Title II entities hold STEM-heavy PDF backlogs: UNKNOWN.
- Whether a proof report changes purchasing: UNKNOWN. E8 tests it.
