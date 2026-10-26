# 06 — Validation experiment designs (NOT executed)

**Status.** Every experiment below is a design only. Running any of them needs **separate user approval**. Two things block execution today:
- (a) Meta credits must be posted and a card attached (R15).
- (b) The tools must be installed: Docker images for veraPDF, plus pikepdf, pypdfium2, NVDA.

No results are claimed. All thresholds are **pre-registered here**, before any run.

## 0. Common protocol

- **Run ledger:** `runs.jsonl`, one line per model call or tool run. Fields:
  - run_id, experiment, ts_utc, git_sha
  - model_id, mode (standard|contributor), reasoning_effort
  - prompt_sha256, input_sha256, output_sha256
  - tokens_in, tokens_out, tokens_cached, latency_ms, cost_usd, retries
  - verdict, ground_truth_id, abstained, notes
- **Artifacts:**
  - Raw requests and responses, with secrets redacted.
  - A SHA-256 manifest of every fixture.
  - An environment manifest: OS, Docker image digests, package versions.
- **Splits:** a dev split for prompt iteration and a **held-out** split touched once, for the final number. Seeds are fixed for synthetic data.
- **Comparison hygiene:** never change model and architecture in the same comparison.
  - *Model comparison:* the same pipeline with Spark vs Glimmer.
  - *Architecture comparison:* the same model with and without the verifier.
- **Security:**
  - Fixture text is data. It goes into schema-constrained user content, never into system prompts.
  - Every suite includes a negative-control fixture with injected instructions.
  - Computer-use runs happen only in a dedicated VM or Windows user profile with no credentials (E6).
- **Budget:** each experiment has a hard ceiling, enforced by the budget guard. Total ceiling across E1–E7: **$50** of granted credit. ₹0 cash.
- **Contributor mode** is allowed only for fixtures we generated or whose license permits training use. Everything else runs in Standard mode.

## E1 — Equation transcription and round-trip verification (decides the math claim, K1)

| Field | Design |
|---|---|
| Decision | Keep or drop "verified math" in the product and demo |
| H1 / H0 | H1: Spark transcribes ≥85% of held-out equations exactly or equivalently, **and** round-trip render-compare catches ≥50% of the errors that remain. H0: below either bar. |
| Ground truth | (i) 60 **synthetic** random LaTeX equations rendered fresh with fixed seeds, which cannot be in any training set; (ii) 40 crops from CC-BY arXiv papers with their source LaTeX (license checked per paper) |
| Leakage control | Synthetic set is the primary number. The arXiv set may be memorized, so it is reported separately. |
| Baseline | Architecture: Spark single pass without round-trip. Model (separate run): Glimmer if Q5 = yes. |
| Measures | Exact match after normalization, visual equivalence (rendered pixel/SSIM threshold fixed in advance), error-detection recall and precision of the round-trip, tokens, latency p50/p95, $ |
| Pass / fail / abstain | Pass: ≥85% **and** detection recall ≥0.5. Fail: <75%. Between the two: keep math, but always route to the human lane. |
| Cost ceiling | $3 (estimated ~$0.5) |
| Stop | 2 consecutive API errors >5% of calls, or ceiling reached |

## E2 — Chart → data table with re-plot check (K2)

| Field | Design |
|---|---|
| Decision | Keep or drop "verified chart tables" |
| Ground truth | 40 synthetic matplotlib charts (bar, line, scatter, grouped) with known data. Random seeds; varied styles, fonts and gridlines. |
| Baseline | Single-pass extraction vs extraction + re-plot compare (architecture). SAM region masks as a further ablation (E7). |
| Measures | Share of charts with all values within 5% of the axis range; per-value MAE; detection of injected misreadings |
| Pass | ≥75% of charts fully within 5% (K2). Otherwise ship tables only as amber "needs human". |
| Cost ceiling | $2 |

## E3 — Verifier on human-judgment checks, ASSETS'25 benchmark (K4)

| Field | Design |
|---|---|
| Decision | Is Parity's AI-judged lane accurate enough to label checks "AI-verified", or only "reviewer-assist"? |
| Ground truth | ASSETS'25 benchmark: 125 PDFs, 7 criteria, labels P/F/NP/CT (S-ASSETS25). **Check the repo license before use (F22, R6).** |
| Leakage | The benchmark was published in 2025 and may be in training data. Disclose this. Supplement with 10 fresh PDFs labeled by us, blind to model output. |
| Baselines | Published numbers: GPT-4-Turbo 0.85, GPT-4o 0.81 (reported, not re-run). Our own run: veraPDF only, which is machine-only and covers fewer criteria. Optional: Gemini via the free tier if quota exists (UNKNOWN). |
| Measures | Accuracy, per-label confusion (especially NP/CT, where published models were weakest), abstention rate, cost per document |
| Pass | ≥0.80 overall, and no label class below 0.6. Fail means position the lane as reviewer-assist (K4). |
| Cost ceiling | $15 (estimated $5–10 for a full run in Standard mode) |

## E4 — Writer validity with veraPDF (K3)

| Field | Design |
|---|---|
| Decision | Tag in place (design A) vs reconstruct (design B) vs HTML-only |
| Fixtures | 10 CC-licensed STEM PDFs, 5–20 pp: 4 born-digital LaTeX, 3 Word-exported, 3 scanned |
| Measures | veraPDF PDF/UA-1 machine pass or fail, count of failed rules by Matterhorn ID, visual diff against the original (design A), text-fidelity diff |
| Pass | ≥8/10 pass machine checks by Day 4. Otherwise fall back to B, then to HTML-only. |
| Cost ceiling | $8 |

## E5 — Information Parity metric sanity check

| Field | Design |
|---|---|
| Decision | Is "Information Parity" a valid metric worth showing judges? |
| Method | For each document, Spark generates 20 factual questions from the visual rendering. A *separate* call answers them using only the screen-reader-linearized text (NVDA-style). Score = share answered correctly, judged by an exact-answer key fixed at generation time. |
| Validity test | Expected ordering: untagged < Parity output ≤ gold human-tagged reference. Gold source to be identified, with license checked. The PDF/UA reference suite is a candidate: UNVERIFIED. |
| Controls | Question generator and answerer get separate prompts and contexts; a human spot-check of 20% of the questions |
| Pass | The ordering holds on ≥8/10 documents. Otherwise drop the metric from the demo. |
| Cost ceiling | $5 |

## E6 — Wonder operates NVDA (K5, stretch)

| Field | Design |
|---|---|
| Decision | Live agent tester in the demo, or the scripted fallback |
| Environment | A dedicated Windows VM or separate local user account; no browser sessions or credentials; NVDA (free) plus a PDF viewer; Speech Viewer on |
| Task | Open the document, jump to heading 2, read the first equation, report what NVDA said. Max 10 steps. |
| Measures | Success out of 5 runs, steps, tokens (quadratic replay), $ per run, every `pending_safety_checks` event (acknowledged only by a human) |
| Pass | ≥4/5 by Day 6 |
| Cost ceiling | $15 (estimated $0.4–3 per run) |

## E7 — SAM 3.1 on document pages

| Field | Design |
|---|---|
| Decision | Does SAM add value to chart and figure checks, or is it decoration? |
| Method | Text prompts "chart", "table", "equation", "bar", "legend" on 50 page images with hand-drawn ground-truth boxes |
| Measures | IoU, recall; then the E2 delta with and without SAM regions |
| Pass | E2 accuracy improves by ≥5 points. Otherwise do not claim SAM in the product (honesty for the Meta-tooling score). |
| Cost ceiling | $1 (computed $0.125) |

## E8 — Customer discovery (no API cost; the **user** sends messages)

- **Decision.** Does a per-check proof report change buying or adoption?
- **Method.** Ten accessibility or disability-services coordinators at public institutions. Script:
  1. current workflow
  2. hours per STEM document
  3. what is filed as evidence of compliance
  4. reaction to a sample proof report
  5. who signs the purchase
- **Rules:**
  - Messages go out only after user approval, and the user sends them.
  - No quotes are invented.
  - Interviews are recorded only with consent.
- **Kill signal.** Six or more of ten say the proof report would not change their decision.

## Runner-up check: redaction R1 (only if the pivot gate triggers)
- **Method.** SAM 3.1 text-prompt tracking on 3 self-filmed 60-second clips (rights clean), at 5 fps (900 frames, about $0.18).
- **Measures.** Frame recall on hand-labeled targets, and track loss during motion.
- **Pass.** Recall ≥0.95.

## Recommended next three (when authorized)
1. **E3**: decides whether the core thesis (an AI-judged lane with evidence) is credible. $15 ceiling.
2. **E4**: decides the build path (K3), using local tools and about $8.
3. **E1 + E2**: decide the two demo hero claims. $5 ceiling.

Together that is about **$28 at most** of granted credit and roughly 16 person-hours (file 01).
