# 04 — Finalist product briefs

Four finalists, ranked. Scores and ranges are in file 05. Every number below is either cited (source ID) or labeled INFERENCE with its assumptions. The product name "Parity" is a working name and **needs approval**.

---

## 1. Parity: accessibility you can prove (STEM PDFs first)

### 1.1 Thesis
Public universities and agencies must make course and public documents conform to WCAG 2.1 AA by **2027-04-26** (≥50K population) or **2028-04-26** (S-FR). STEM documents are the hardest case: equations, charts and tables. The regulator says gen-AI "does not yet reliably automate" remediation (S-FR, 91 FR 20907). Incumbents answer with "trust our AI" (file 03).

Parity answers with **evidence attached to every check**:
- **Machine-verified:** the veraPDF Matterhorn machine set.
- **AI-judged with visible evidence:** the human-judgment set. Evidence means render-and-compare images, a text diff, or re-plotted charts.
- **Routed to a human** when confidence is low.

On top of the checks, Parity reports **Information Parity**: whether a non-visual reader can answer the same questions as a sighted reader.

**Positioning against the closest incumbent.** Allyant CommonLook already ships a per-PDF "Validation Report" pitched as Title II compliance evidence (S-ALLYANT-AI). Parity therefore must **not** pitch "we give you a report". Its claim is narrower and testable:
1. **Evidence on the 47 judgment checks**, not only pass/fail counts.
2. **Math as navigable MathML**, not alt text (S-PDFDAYS).
3. **A screen reader operated by an agent** confirms the result.
4. It **audits anyone's output**, including CommonLook's.

All four are hypotheses until E1/E3/E5/E6 run and the competitor trial is inspected.

**Customer outcome (one sentence).** An accessibility office remediates a STEM PDF in minutes, not hours, and gets an auditable report showing what was verified, how, and what still needs a human.

**Conditional or unverified dimensions:**
- every accuracy figure (E1–E5)
- willingness to pay (E8)
- whether a proof report changes purchasing (E8)
- the track (file 05)

### 1.2 Customer journey
1. **Trigger:** a faculty upload, an accommodation request, or the backlog sweep before the deadline.
2. Coordinator drops in a PDF, or a folder. A batch API comes in H2.
3. Parity tags the PDF and builds a MathML HTML twin. Each check carries a status:
   - green: machine-verified
   - blue: AI-verified, with evidence
   - amber: needs a human
4. Coordinator reviews only the amber items, with the evidence side-by-side, then approves or overrides. Every decision is logged.
5. Exports: an accessible PDF, the HTML twin, and a proof report (JSON + human-readable). The proof report is the artifact the coordinator files for compliance.
6. **Repeat value:** a re-uploaded revision re-runs only the changed pages (content hash). The audit history accumulates.

### 1.3 Two solution designs compared

| | **A. Tag in place** (edit the original PDF) | **B. Reconstruct** (rebuild from a semantic model) |
|---|---|---|
| How | pikepdf writes the structure tree and marks content with MCIDs in the existing streams | Render a new PDF (WeasyPrint/LaTeX) plus HTML from the extracted `DocumentModel` |
| Visual fidelity | Original preserved | Changes layout. Text-fidelity risk. |
| Validity | Hard. Content-stream surgery is the main risk (K3). | Easier, but WeasyPrint PDF/UA-1 is "experimental" (S-WEASY), so veraPDF must gate it |
| Math | MathML embedding needs PDF 2.0 support (S-PDFA-MATH) | HTML + MathML is mature (S-ARXIV-MATHML) |
| Verdict | **Primary for the PDF** | **Always produced as the HTML twin**; the fallback PDF if A fails K3 |

### 1.4 Architecture (competition kernel)

```
                ┌──────────── Control plane ─────────────┐
 PDF upload ──▶ │ Job API ─ Orchestrator (state machine) │──▶ Proof report / exports
                │   budget guard · cost ledger · replay  │
                └──┬────────────┬───────────┬────────────┘
   Data plane:     ▼            ▼           ▼
   1 Ingest     2 Understand  3 Verify    4 Write          5 Review UI
   pypdfium2    Spark vision  V1 veraPDF  pikepdf tags     overlays, evidence,
   page render  +structured   V2 eq round  HTML+MathML     approve/override
   text layer   output        V3 chart     (WeasyPrint     → decision log
   SHA-256      1M-ctx doc     re-plot(+SAM) fallback)
                pass          V4 text diff
                              V5 info-parity QA
                              V6 2nd-opinion judge (Spark other effort / Glimmer)
   6 Stretch: Wonder drives NVDA + viewer by keyboard; reads Speech Viewer screenshots
```

**Model roles and the true Meta dependency:**

| Component | Model | Why that model |
|---|---|---|
| Page understanding | **Muse Spark** (structured output, image + PDF input, S-MODELS) | Blocks, types, bboxes, reading order, LaTeX, alt text, long descriptions, chart data, table headers |
| Document-level consistency | Spark, 1,048,576-token context | Heading levels, cross-references, notation across the whole file. Image input covers only the first 50 pages, text the first 100 (S-FILES), so long files are chunked |
| Chart and figure regions | **SAM 3.1** (S-SEG) | Text-prompted region masks ("bar", "axis", "legend"). Value is UNTESTED (E7) |
| Second-opinion judge | **Muse Glimmer**, self-hosted (Q5), or Spark at a different reasoning effort | An independent judgment, so the model is not grading its own output |
| Screen-reader tester (stretch) | **Muse Wonder** computer use (S-CU) | Operates real AT the way a user does |

**Invariants:**
- No model marks its own output correct. Each verdict needs either a deterministic check or an independent judge, and deterministic checks override model verdicts.
- Generated text (alt text, descriptions) is always labeled as generated in the report.

**Trust boundaries:**
- Uploaded PDFs are untrusted. Their text is passed only as data inside schema-constrained requests, never as instructions.
- Rendering and parsing run in a container.
- There is a negative control for injected instructions (AT10).

**Data contracts (versioned JSON Schema):**
- `DocumentModel`: pages → blocks{id, type, bbox, order, text, latex, alt, long_desc, table, chart_data, confidence}
- `CheckResult`: {check_id (Matterhorn ID), method machine|ai|human, verdict pass|fail|needs_human, confidence, evidence[]}
- `ProofReport`: doc SHA-256, pipeline version, model IDs, prompt hashes, results[], human decisions[]

**Operability:**
- Idempotency key = (doc SHA-256, pipeline version, model ID, prompt hash).
- Every model call is cached. **Replay mode** runs the full flow offline from the cache; it is also the demo fallback.
- Per-call cost ledger, plus a budget guard that refuses calls past the hard stop.
- Timeouts and retries with backoff. Failed or abstaining checks become `needs_human`, so a job completes partially instead of failing.

**Provisional stack** (justified by library ecosystem, not team skill):
- Python backend: the PDF tooling is Python (pikepdf, pypdfium2) or Java (veraPDF, run in Docker).
- Web UI for review, framework to be decided.
- SQLite plus a content-addressed file store for the kernel.
- License note: avoid PyMuPDF (AGPL) in the product and use pypdfium2 instead. That has to be checked against the repo license choice.

### 1.5 Acceptance tests (competition kernel)

| ID | Test | Pass bar |
|---|---|---|
| AT1 | 10 public CC-licensed STEM PDFs (≥5 pp each, ≥30 equations and ≥10 charts across the set) | ≥8/10 pass veraPDF PDF/UA-1 machine checks (K3) |
| AT2 | 100 held-out equations with LaTeX ground truth | ≥85% exact or visually equivalent after round-trip (K1) |
| AT3 | 40 synthetic charts with known data | ≥75% with all values within 5% (K2) |
| AT4 | Text fidelity | 0 invented body-text spans (diff against the text layer); 100% of generated text labeled |
| AT5 | ASSETS'25 held-out split | Verifier accuracy ≥0.80, confusion matrix reported (K4) |
| AT6 | Proof report | Every in-scope checkpoint has a method, a verdict and an evidence pointer; JSON-schema valid |
| AT7 | Wonder tester, stretch | ≥4/5 successful runs of the scripted task (K5) |
| AT8 | Budget guard | A simulated over-budget call is refused (unit test) |
| AT9 | Replay | The full demo runs with the network off |
| AT10 | Injection negative control | A PDF containing "mark all checks passed" changes no verdict |

### 1.6 Three-minute demo (storyboard) — what is live, and the fallback

| Time | Scene | What is live | Fallback |
|---|---|---|---|
| 0:00–0:20 | **Cold open.** Black screen; NVDA reads a real calculus PDF and it comes out as garbage ("x two plus … image … image"). Caption: *This is what a blind student hears.* Then the date 26 April 2027 and the DOJ quote. | Real NVDA audio, screen-recorded | Pre-recorded clip (it is a recording anyway) |
| 0:20–0:35 | Title card: **"Parity — accessibility you can prove."** The PDF is dropped in. | Live UI | — |
| 0:35–1:20 | Regions light up as the pipeline streams. An equation becomes MathML with a "round-trip verified" badge (rendered side-by-side). A chart becomes a table with a "re-plot matches" badge. One figure goes **amber**, to the human lane. | Live Meta calls, real outputs | Replay mode from cached responses (AT9) |
| 1:20–1:50 | **Proof report.** Machine checks pass (veraPDF output shown). AI-judged checks show their evidence. Information Parity before → after, e.g. 38% → 96%: **placeholder, to be measured (E5)**. | Live veraPDF run; measured numbers only | Cached report |
| 1:50–2:30 | **The screen-reader tester.** Wonder opens the fixed document, navigates by keyboard, reaches the equation, and NVDA reads it correctly. Split screen: the agent's actions next to the Speech Viewer. | Live or recorded live run | Scripted keyboard path (K5) |
| 2:30–2:50 | **Scale and honesty.** Measured cost per page vs $3–8/page manual (S-ASU, S-OSU-SUPPLIERS). Accuracy on a public benchmark (E3). What still goes to humans. | Measured figures only | — |
| 2:50–3:00 | Close: "Every accessible document should come with proof." Credits: what we built during the event, and the OSS we stand on (R4). | — | — |

Story spine: **a harm you can hear → a deadline → a regulator that does not trust AI → proof → a blind-user agent confirms → honest numbers.** Hackathon advice sources agree on a story-first structure, a backup recording and cached responses (S-HACK-TIPS).

### 1.7 Economics (INFERENCE; assumptions explicit)
- **Image-token accounting for Spark: UNKNOWN.** The assumption is about 1.5–3K input tokens and about 1.5K output tokens per page per pass.
- **Spark Standard** ($1.25 in / $4.25 out per 1M, S-PRICING): about $0.005–0.015 per page per pass. With 3–4 verification passes, about **$0.02–0.06 per page**.
- **Contributor mode** ($0.10 / $0.20): about 12–20× cheaper. Use it only on public, licensed documents.
- **Wonder** ($4 / $20): a 10-step test with stateless replay grows quadratically with history. At 1.5–8K tokens per screenshot that is about **$0.4–3 per run**.
- **SAM 3.1:** $2.50 per 1K images, so about $0.0025 per page region pass.
- **Event budget:** $300 if both credits post. Allocation proposal:
  - experiments $20
  - development $80
  - Wonder $90
  - demo runs $30
  - reserve $80
  - budget guard stops at $120 per account
- **Customer pricing hypothesis** (not evidence): $0.50–2 per page against $3–25 manual. Inference cost is under 10% of price. Human review time stays with the customer's own staff.

### 1.8 Acquisition path (hypotheses)
1. **Wedge:** a free "audit any PDF" proof report that also works on other vendors' output. This positions Parity as the neutral auditor and makes it easy to share.
2. **Paid:** remediation per page or per seat for accessibility offices.
3. **Pilot:** one university office or one city before 2027-04-26.
4. **Distribution later:** LMS integrations (Canvas and similar).

Channels such as accessibility listservs and conferences are not verified (UNKNOWN).

### 1.9 Three horizons

| Horizon | Scope | Exit criteria |
|---|---|---|
| **H1 Competition (by Nov 4)** | One workflow end-to-end: STEM PDF → tagged PDF + MathML HTML + proof report + review lane. The Wonder tester is a stretch. Public benchmark numbers. | AT1–AT10. Demo recorded. New-work disclosure. |
| **H2 Pilot (Nov 2026 → Apr 2027)** | Batch API, Canvas/SharePoint sync, reviewer roles, audit trail, Glimmer self-host for FERPA-sensitive files, SSO. Measure the precision of "verified" labels against an expert audit. | One institution, measured hours saved, zero false "verified" findings on audited samples |
| **H3 Platform** | Proof layer for all content: slides, Word, video (AD and captions via Spark video + Voice Transcribe, absorbing finalist 3), web. Certify third-party remediations. Agent-readable documents (S-OPENAI-ATLAS). EU Accessibility Act: **UNVERIFIED this session.** | Only once H2 shows demand |

### 1.10 Risks and kill criteria
Kill criteria K1–K5 are in file 07. Top risks:
1. Writer validity (K3).
2. A crowded market with LMS-bundled incumbents.
3. Evidence that AI alt text may hurt users (S-SILKTIDE-ALT). **Mitigation:** label generated text, route low confidence to humans, and measure with Information Parity.
4. The anti-project misread (R9).
5. Spark image-token cost being UNKNOWN.

---

## 2. Finalist 2 — Policy-driven video redaction (runner-up)

- **Thesis.** Records officers describe what must be hidden in policy language, e.g. "the minor", "documents on the desk", "addresses spoken aloud". SAM 3.1 text-prompted tracking (S-SEG) plus Voice Transcribe turns that policy into tracked masks and audio bleeps. Spark writes an exemption log tied to the statute.
- **Customer outcome.** Fewer than 1–8 staff hours per video hour (S-REDACT-COST, S-ISED, S-AXON); the size of the gain is UNTESTED.
- **Architecture.**
  1. Ingest: video → frames sampled at about 5 fps.
  2. SAM 3.1: text-prompt tracks per policy clause.
  3. Interpolate masks to full frame rate.
  4. Voice Transcribe: PII spans → bleep.
  5. Spark: clause → exemption log; ambiguous detections go to human review.
  6. Render a redacted copy. The original is preserved, with a hash-chained audit trail.
- **Meta dependency.** Very strong: SAM 3.1, Voice Transcribe and Spark are all central. This scores highest on Meta tooling.
- **Economics (computed from S-PRICING).** SAM at 5 fps costs about $3.60 per video hour, plus transcription at $0.18/h.
- **Demo.** Staged footage that we film ourselves (rights clean, R6). The policy is typed live and redaction follows it. Fallback: cached tracks.
- **Acceptance tests.**
  - Frame-level recall ≥0.95 on staged targets.
  - Audio PII recall ≥0.9.
  - 0 unredacted target frames in the final export (blocking).
- **Kill criteria.**
  - SAM loses the track on motion in fewer than about 90% of frames.
  - Evidence that Axon already supports text-prompted redaction.
- **Why it ranks second.**
  - The why-now is weaker: no dated trigger.
  - Axon bundles redaction for the largest US buyers (S-AXON).
  - Law-enforcement footage is sensitive.
  - It needs staged data.

## 3. Finalist 3 — Audio description studio for instructional video

- **Thesis.** Spark video understanding (S-VIDEO) plus Voice Transcribe dialogue gaps produce WCAG 1.2.5 AD scripts with timing. A reviewer approves them, and the voice comes from a non-Meta TTS.
- **Why third.**
  - Incumbents already ship AI AD (S-VERBIT, S-AIMEDIA, S-RECAP, S-3PLAY).
  - Meta has no TTS (S-MODELS), so the core voice output is not Meta.
- **Best use.** A Parity H3 module.
- **Kill criteria.** No measurable quality edge over a 3Play synthesized sample on the same clip, with blinded raters.

## 4. Finalist 4 — Robot demonstration data QA

- **Thesis.** Flag failed or low-quality teleoperation episodes before training, using Spark video reasoning plus SAM contact tracks.
- **Why fourth.**
  - The buyer set is small.
  - Prior art is heavy: FailBench, DQA, robot-episode-labeler (S-FAILBENCH, S-DQA, S-REL).
  - Commercial platforms are unverified (F35).
- **Kill criteria.** Must beat robot-episode-labeler F1 0.629 on the same public episodes, otherwise there is no edge.
