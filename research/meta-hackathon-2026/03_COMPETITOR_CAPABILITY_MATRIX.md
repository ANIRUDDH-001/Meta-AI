# 03 — Competitor capability matrix

**Labels.** **YES-OBS** = observed by us · **CLAIMED** = vendor/author claim · **3P** = third-party report · **PARTIAL** = a source shows limits · **NO-VER** = verified absence · **UNK** = not established. UNK is never read as a competitor weakness.

**What was not done.** No competitor product was run (₹0, read-only), so nothing reaches YES-OBS. Every cell cites a source ID from [`sources.jsonl`](sources.jsonl). The differentiation in our own row is a **hypothesis until the named experiment passes** (file 06).

## 1. Finalist 1 — Parity (verifiable STEM PDF remediation)

### 1.1 Capabilities compared
- C1 auto-tag structure (headings, lists, reading order)
- C2 table headers
- C3 figure alt text
- C4 math → MathML (not just alt text)
- C5 chart → data table
- C6 machine conformance checks (PDF/UA / Matterhorn machine set)
- C7 automated *human-judgment* checks with evidence (Matterhorn's 47)
- C8 per-check proof report a third party can audit
- C9 agent actually operates a screen reader on the output
- C10 information-equivalence score
- C11 can audit *other vendors'* output
- C12 self-host / open weights
- C13 LMS / batch integration
- C14 public price

| Solution | C1 | C2 | C3 | C4 | C5 | C6 | C7 | C8 | C9 | C10 | C11 | C12 | C13 | C14 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **Allyant CommonLook AI / Edu** (S-ALLYANT, S-ALLYANT-AI, S-ALLYANT-PR) | CLAIMED ("tagging STEM content, tables, lists") | CLAIMED (tables) | CLAIMED ("Alternative text generation of math equations, chemistry equations, and diagrams") | PARTIAL: math handled as **alt text**, and alt text ≠ MathML (S-PDFDAYS) | UNK | CLAIMED: per-PDF "Validation Report" with passed/failed/warning counts and checkpoints (PDF/UA, WCAG, HHS) | PARTIAL: "manual tagging tools … issues that require manual review"; no evidence-per-check found | **PARTIAL**: a report "to demonstrate adherence … including ADA Title II" plus a "System of Record"; evidence content not shown | UNK | UNK | UNK | UNK | CLAIMED (system of record; PDF/Word/NIMAS/ePub inputs) | Service $5.00/pg + $3 OCR (S-OSU-SUPPLIERS); software price not public |
| **YuJa Panorama** (S-YUJA, S-NEOMED, S-PURDUE) | PARTIAL: AI "AutoPilot" not available to most users | PARTIAL: tables "checked by hand" | PARTIAL: same | CLAIMED: math images → MathML in the **HTML** alternative format | UNK | UNK | UNK | UNK | UNK | UNK | UNK | UNK | CLAIMED (LMS platform) | UNK |
| **Anthology Ally** (S-ALLY) | PARTIAL: tagged-PDF alternative only from Word/PPT | UNK | UNK | PARTIAL: only Word Office Math → MathML; PDF math undocumented | UNK | CLAIMED: weighted score of checks | UNK | UNK | UNK | UNK | UNK | UNK | CLAIMED (LMS) | UNK |
| **Adobe Auto-Tag API** (used inside S-ASU; S-EQUIDOX-AUTOTAG, S-AXESSTAG) | CLAIMED; PARTIAL ("results vary") | UNK | UNK | UNK | UNK | UNK | UNK | UNK | UNK | UNK | UNK | NO-VER (cloud API) | UNK | UNK (Adobe docs not fetched) |
| **Equidox** (S-ASU-EQ, S-EQUIDOX-AUTOTAG) | CLAIMED | UNK | UNK | PARTIAL: "may not accurately … tag complex STEM notation" | UNK | UNK | UNK | UNK | UNK | UNK | UNK | UNK | UNK | UNK |
| **Mathpix** (S-MATHPIX) | — | — | — | 3P: PDF → DOCX/HTML with MathML; universities still say "read back every expression" | UNK | — | — | — | — | — | — | UNK | UNK | UNK |
| **ASU × OSU open pipeline** (S-ASU) | CLAIMED (via Adobe Auto-Tag) | UNK | CLAIMED (Bedrock) | UNK | UNK | PARTIAL: "quality checkpoints still being developed" | UNK | UNK | UNK | UNK | UNK | CLAIMED (open source, AWS) | PARTIAL (UI "not for production") | CLAIMED ≈$0.0013/pg + Adobe |
| **veraPDF / PAC** (S-MATTERHORN) | — | — | — | — | — | CLAIMED: implement Matterhorn machine checks | NO by design: the 47 need human judgment (INFERENCE from S-MATTERHORN) | PARTIAL: machine-check reports only | — | — | CLAIMED: checks any PDF | YES (veraPDF OSS) | — | Free |
| **LLM evaluators, research** (S-ASSETS25) | — | — | — | — | — | — | PARTIAL: 7 criteria, best 0.85 (GPT-4-Turbo); weak on Not-Present / Cannot-Tell | — | — | — | Research only | Llama 3.2 scored 0.42 | — | — |
| **iTagPDF, CHI '26** (S-ITAG) | CLAIMED: beats Acrobat on most criteria | UNK | CLAIMED | PARTIAL: needs LaTeX source | UNK | UNK | UNK | UNK | UNK | UNK | NO (needs source) | UNK | — | Research |
| **PAVE 2.0** (S-PAVE) | PARTIAL: assisted; tagging score 42%→80% | UNK | UNK | UNK | UNK | UNK | UNK | UNK | UNK | UNK | UNK | UNK | — | Research |
| **AxessTag AI / Nutrient / QyrosXS** (S-AXESSTAG, S-NUTRIENT, S-QYROS) | CLAIMED | UNK | UNK | UNK | UNK | Nutrient CLAIMED (agent compliance loop) | UNK | UNK | UNK | UNK | UNK | UNK | UNK | UNK |
| **Manual remediation vendors** (S-ASU, S-VENNGAGE) | YES (human) | YES | YES | UNK | UNK | UNK | YES (human) | UNK | UNK | UNK | YES (human audits) | — | — | $3–25/pg |
| **Parity (ours, PLANNED)** | E4 | E4 | E3/E5 | E1 | E2 | veraPDF (E4) | E3 | built-in | E6 | E5 | E3 | Glimmer (Q5) | H2 only | target <$0.10/pg (INFERENCE) |

### 1.2 Where competitor workflows stop (evidence)
- Everyone ends with a human checking the result:
  - NEOMED: images, graphics and tables are checked by hand (S-NEOMED).
  - Universities: "read back every expression" after Mathpix (S-MATHPIX).
  - CMU: many PDFs still need manual reading-order and alt-text work (S-CMU).
  - ASU: QA checkpoints are still being developed (S-ASU).
  - The DOJ says gen-AI "does not yet reliably automate" remediation (S-FR).
- Machine validators cover only the machine-checkable part. **47 of 136** Matterhorn failure conditions need human judgment (S-MATTERHORN).
- Math is handled as alt text, or in an HTML alternative format, rather than as MathML inside the PDF, which gives no Nemeth braille (S-PDFDAYS, S-YUJA, S-ALLY).

- **Allyant desk check, done 2026-10-26 (S-ALLYANT-AI).** CommonLook already sells a per-PDF Validation Report, positioned as Title II compliance evidence, plus a remediation history. **A "compliance report" is therefore not a differentiator.** Their public material does not show:
  - evidence attached to the human-judgment checks
  - math as MathML (they generate alt text)
  - verification by operating a screen reader
  - an information-equivalence measure
  - audits of other vendors' output

  Settling those points needs their 7-day trial, which means creating an account. Only the user can do that.

### 1.3 What incumbents do well (do not under-estimate)
- They sit inside the LMS and procurement already (Ally and Panorama, per S-ALLY and S-YUJA). Distribution is their moat.
- Human services vendors already sell audited output.
- Allyant already claims STEM alt text, a Title-II-positioned validation report and a system of record (S-ALLYANT-AI). Their pitch is close to ours. Ours has to be *evidence*, not *a report*.

### 1.4 Strongest argument against launching
> Incumbents own distribution inside the LMS. "Add an LLM judge plus a report" is a feature they can ship in a quarter. Edu procurement is slow and bundles purchases.

Our only defensible answers, all still hypotheses:
1. Be a **neutral auditor** that verifies *any* vendor's output (C11). The vendor that grades its own homework is the conflict buyers worry about.
2. Publish a **measured benchmark**: verifier accuracy on ASSETS'25 plus our own information-equivalence set.
3. **Agent-operated screen-reader evidence** (C9). No source shows any competitor doing this, but UNK ≠ absent.

### 1.5 Differentiation claims, each assumed FALSE until tested

| Claim | Mechanism | Honest baseline | Refuting experiment |
|---|---|---|---|
| Our verifier judges human-judgment checks at least as well as published LLM evaluators | Multi-pass Spark + deterministic evidence (render-and-compare) | GPT-4-Turbo 0.85 on ASSETS'25 (S-ASSETS25) | E3: if we score <0.80, the claim dies (K4) |
| Equation output is checkably correct | Render the produced LaTeX/MathML → visual diff against the source crop | Spark transcription without the round-trip (ablation) | E1: round-trip catches less than half of the injected errors → drop the badge |
| Chart tables are faithful | Re-plot the table → compare with the original chart (+ SAM regions) | Single-pass extraction | E2 (K2) |
| Information Parity measures something real | Same question set answered from visual vs non-visual renderings | Untagged PDF vs gold-tagged reference | E5: if ordering untagged < ours ≤ gold fails → drop the metric |
| An agent can operate NVDA on the output | Wonder computer use + Speech Viewer screenshots | Scripted keyboard path | E6 (K5) |

## 2. Finalist 2 — Policy-driven video redaction

| Solution | Faces / plates | Screens / on-screen text | Audio PII | Text-prompted ("redact X") | Tracking | Exemption log | Human confirm | On-prem | Price public |
|---|---|---|---|---|---|---|---|---|---|
| Axon Redaction Assistant (S-AXON) | CLAIMED | CLAIMED (screens) | UNK (only a competitor blog) | UNK | CLAIMED (boxes) | CLAIMED | CLAIMED | UNK | NO (bundled in US OSP 7+) |
| Pimloc Secure Redact (S-PIMLOC) | CLAIMED | CLAIMED | CLAIMED (NER) | UNK (fixed categories seen) | CLAIMED | UNK | UNK | UNK | UNK |
| Facit (S-FACIT) | CLAIMED | UNK | UNK | UNK | UNK | UNK | UNK | CLAIMED | UNK |
| Veritone, CaseGuard | UNK | UNK | UNK | UNK | UNK | UNK | UNK | UNK | UNK |
| Manual editors | YES (human) | YES | YES | YES (human) | YES | YES | — | — | 1–8 staff h per video h (S-REDACT-COST, S-ISED, S-AXON) |
| Ours (PLANNED) | SAM 3.1 | SAM 3.1 | Voice Transcribe | SAM text prompts (S-SEG) | SAM video tracks | Spark | UI | Glimmer only for text | — |

Strongest argument against: the largest US buyers get Axon's tool bundled.

## 3. Finalist 3 — Audio description

| Solution | AI-generated AD | Extended AD | Human review option | Title II marketing | Public price |
|---|---|---|---|---|---|
| Verbit AI AD (S-VERBIT) | CLAIMED | UNK | CLAIMED | CLAIMED | NO |
| 3Play Media (S-3PLAY) | CLAIMED (synthesized voice) | CLAIMED | CLAIMED (voice artist tier) | UNK | YES: $9/$14 per min synthesized |
| Ai-Media LEXI AD (S-AIMEDIA) | CLAIMED | UNK | UNK | UNK | UNK |
| Recap (S-RECAP) | CLAIMED | UNK | UNK | UNK | UNK |
| Ours | Spark video | Spark | UI | — | Meta has **no TTS** (S-MODELS): NO-VER |

Strongest argument against: the category already ships AI AD. Our edge would have to be measured description quality, and we have no baseline for it.

## 4. Finalist 4 — Robot demonstration data QA

| Solution | Success / failure judgment | Sub-task segmentation | Quality score | Evidence |
|---|---|---|---|---|
| robot-episode-labeler (S-REL) | CLAIMED | CLAIMED (F1 0.629) | UNK | Replicate README |
| DQA framework (S-DQA) | — | — | PRIMARY (85.7% recall) | Paper |
| FailBench (S-FAILBENCH) | Benchmark of VLM judges | — | — | Paper |
| Encord / Scale / Voxel51 robotics | UNK | UNK | UNK | Not verified (F35) |

Strongest argument against: a small buyer set, and the research frontier is moving faster than a 9-day build can.
