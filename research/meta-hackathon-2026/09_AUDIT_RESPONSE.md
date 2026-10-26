# 09 — Response to the independent audit

- **Audit:** `INDEPENDENT_REPOSITORY_AUDIT_2026-10-26.md` (ChatGPT), 23 findings A01–A23, against commit `01ee5bb` (16:09:24 UTC).
- **Response written:** 2026-10-26T16:51Z (from `date -u`).
- **Method:** each finding was checked against our files and, where it makes a factual claim, against the primary source. Claude has no GitHub access, so findings that need GitHub go to Codex (§6).
- **Verdict key:**
  - **ACCEPT**: correct; we change.
  - **PARTIAL**: right problem, wrong or incomplete fix.
  - **DISCLOSED**: already stated in our files; wording tightened only.
  - **UNVERIFIABLE**: Claude cannot check it.
  - **DISPUTE**: wrong.

## 1. Bottom line

| Verdict | Count | IDs |
|---|---|---|
| ACCEPT | 16 | A02, A03, A05, A06, A07, A08, A09, A10, A13, A14, A15, A16, A18, A19, A22, A23 |
| PARTIAL | 4 | A04, A20, A21, and the decision framework |
| DISCLOSED | 1 | A11 |
| UNVERIFIABLE (Codex) | 1 | A12 |
| Severity disputed, substance accepted | 2 | A01, A17 |

The audit is right on the main point: **our "proof" language claimed more than our evidence can carry.** Four things change.

1. **"Proof" and "verified" are retired.** They are replaced by evidence classes (§3.1). The tagline "accessibility you can prove" goes to an MCQ.
2. **E3 is redesigned.** It gets a claim-scoped coverage matrix, a split grouped by base PDF, opaque IDs, and false-pass rate as the primary metric (§3.3).
3. **The PDF writer's math claim was internally contradictory.** We now say so (§2.1, item 4).
4. **The product decision cannot rest on 7.83 vs 7.98.** It gets a timeboxed discriminating test (§4).

### 1.1 What the audit missed (found while checking it)

1. **The 2027 deadline is contested in both directions.**
   - DOJ "plans to engage in future rulemaking processes related to the substantive requirements of the 2024 final rule" and "will consider issuing an NPRM" (S-FR, 91 FR 20908).
   - SBA Advocacy put the rule on its list for "rescission, withdrawal, or modification" (91 FR 20905).
   - The NFB sued DOJ and HHS on 2026-05-21 in the District of Maryland to undo the extensions. No ruling was found (S-NFB-SUIT, THIRD-PARTY).
   - The obligation under existing Title II applies "regardless of the compliance dates" (91 FR 20908).
   - **Consequence:** the audit calls the deadline "the strongest external premise", and so did we. It is a real but movable driver. A weakened rule would hit Parity's why-now. A shortened deadline would help it.
2. **The ASSETS'25 benchmark is 125 variants of 35 base PDFs.** They are highly cited papers, edited in Acrobat Pro (S-ASSETS25). A random split puts variants of one paper on both sides, which leaks. **The split must be grouped by base PDF.**
3. **The ASSETS'25 protocol did not feed models whole PDFs.** Each criterion had its own prompt, given page images plus extracted data (tag tree, alt text, colour values, font metadata). Settings: temperature 0.7, three runs, page by page, and the most conservative page label became the document label. Some inputs were withheld on purpose to create "Cannot Tell" cases. Published accuracies are only comparable if we copy that protocol.
4. **Sample size makes 0.80 vs 0.85 indistinguishable.**
   - The 95% Wilson interval for accuracy 0.80 at n = 125 is **0.72–0.86**.
   - At n = 60 (a held-out half) it is 0.68–0.88.
   - Per-criterion cells (about 18 documents) give 0.57–0.92.
   - Computed with `python -I`; the formula is in §3.3.
   - So E3 can support neither a "beats GPT-4-Turbo" nor a "worse than" claim. The fix is to **drop competitive claims**, not to raise the bar to 0.85 (see A04).

## 2. Per-finding verdicts

| ID | Verdict | Why (evidence) | Change | Where |
|---|---|---|---|---|
| A01 | ACCEPT substance; DISPUTE "Critical" | No code exists **by design**: the mandate was "Perform read-only research... Do not implement anything". Every experiment is marked "design only" (06). A status is not a defect. | None. We already claim no capability. | — |
| A02 | ACCEPT | ASSETS'25 scores 7 criteria defined against WCAG 2.2 success criteria plus PDF/UA (S-ASSETS25). It is not the 47 Matterhorn human-judgment conditions, and 7-criterion accuracy says nothing about the rest. | Claim scope: "on the 7 ASSETS'25 criteria" only. Coverage matrix: every human-judgment condition Parity touches is covered by an ASSETS criterion, by our own fixture, or is **not covered → needs_human**. Conditions that do not apply to a document (forms, XFA, signatures) are marked N/A. | 04 §1.1, 06 E3 |
| A03 | ACCEPT | A veraPDF pass covers the machine-checkable Matterhorn conditions only. The legal standard is WCAG 2.1 AA (S-FR), not PDF/UA. | Wording: "N of M machine checks passed (veraPDF x.y, PDF/UA-1)". Never "accessible", "compliant" or "certified". | 04, 08 |
| A04 | PARTIAL | The audit is right that ≥0.80 does not show an edge over 0.85. Its implied fix, a competitive bar, is unsupportable at n ≈ 125 (§1.1, item 4). Also, accuracy is the wrong primary metric: the harm is a **false pass**, a check marked passed that actually failed. | Gate on the false-pass rate with an upper confidence bound, plus a risk–coverage curve with abstention to needs_human. No competitive claim unless the baseline is re-run on the identical split with the same protocol. We cannot re-run GPT-4-Turbo, so we make **no** competitive claim. | 06 E3, 07 K4 |
| A05 | ACCEPT | Spark judging Spark at a different reasoning effort is self-consistency, and its errors correlate. Glimmer is a different model from the same vendor, with unknown overlap in training data. | Independence ladder (§3.2). The report states the level of each verdict. | 04 §1.4 |
| A06 | ACCEPT | E5 has the model write the questions and the answer key, so the metric is partly circular. | Synthetic documents generated from a known fact table, with questions and answers produced **by code**. Real documents use human-written Q/A, fixed before any output is seen. The answerer reads the linearised text: from the NVDA speech log where E6 runs, otherwise from a deterministic tag-tree linearizer labelled *proxy*. The metric is renamed "information available to a non-visual reader (proxy)" and does not claim user task success. | 06 E5 |
| A07 | ACCEPT (math); PARTIAL (charts) | **Math:** two different MathML trees can render the same image, but a screen reader speaks the markup, e.g. "f of x" vs "f times x". **Charts:** E2 already scores against synthetic ground truth (06 E2). What is missing is the rate at which the re-plot "matched" while values were wrong. | **E1:** compare MathML structure with reference MathML converted deterministically from the ground-truth LaTeX (converter and licence TBD). Add an adversarial near-miss set (sign flips, swapped sub/superscripts, dropped brackets) and report the false-match rate. **E2:** report the false-verified rate. | 06 E1/E2 |
| A08 | ACCEPT | Writing tags into existing content streams is unproven (K3). The audit also misses that **AT1 gates on PDF/UA-1**, while MathML inside a PDF needs PDF 2.0 (S-PDFA-MATH). Under PDF/UA-1, math is a `Formula` tag with alt text. So claim 2 ("math as navigable MathML, not alt text") holds **only for the HTML twin**. | E4 runs before any UI work. Claim 2 is rescoped to the HTML twin. Audit-first and HTML-first shapes go to the pivot brainstorm (file 10). | 04 §1.1/§1.3, 10 |
| A09 | ACCEPT | Already found: CommonLook User Verifications are manual, with the "Verification result set by user" (S-CL-USERVERIFY). "Not documented" is not "absent". | Differentiator A1 stays a hypothesis until we compare outputs on the same documents. The trial needs an account, which only the user can create. | 08 §3 |
| A10 | ACCEPT | No interviews, no willingness-to-pay evidence, no pilot. The Indie track is judged on "creativity, technical ambition, and whether it works" (S-EV), but Impact is still 30%. | A deadline is a market signal, not validation. Desk proxy: public RFPs and procurement records (file 10). E8 stays user-run. | 08, 10 |
| A11 | DISCLOSED | 02 line 3 already says 9 hypotheses were researched and 4 desk-screened "with **no** evidence search" (F36). | Add: "no claim of a global optimum". | 02 |
| A12 | UNVERIFIABLE (Claude) | The licence text is on GitHub, which Claude may not access. The paper gives no licence for the dataset or the source PDFs. **Added:** even a CC0 dataset licence cannot relicense the 35 third-party scholarly papers it was built from (INFERENCE, not legal advice). | Evaluation use only. Never redistributed. Never shown in the demo unless that paper's own licence allows it. Codex checks `LICENSE` and the README (§6). | 06 E3, 07 |
| A13 | ACCEPT | pdfa.org lists Matterhorn **1.1** (April 2021) as superseding 1.02. The total of 136 conditions is unchanged. The 87/47/2 split is confirmed for 1.02. We could not extract it from the 1.1 PDF, so it is unconfirmed for 1.1. | Cite 1.1 (S-MATTERHORN-11). Keep 1.02 for the split until it is checked. | 00 C3, 03 |
| A14 | ACCEPT | The guide says the spend limit is a "notification" (R15). A per-process counter cannot stop concurrent overrun. | Reservation broker (§3.4). Cap set **below** the credit. The user reconciles against the billing page daily. "₹0" is a goal with monitored residual risk, **not a guarantee**. | AGENTS.md, 04 §1.7 |
| A15 | ACCEPT | Cost per page came from token guesses (04 §1.7 already says "UNKNOWN"). | Report all-in cost per **accepted document**, p50/p95, from measured usage, including retries. Estimate human review minutes separately. | 04 §1.7 |
| A16 | ACCEPT | 5 fps tracking with interpolation cannot claim zero exposed frames at 30 fps. | If redaction is chosen: a full-frame leak check on every output frame. At $0.20 per 1K frames, 3 × 60 s × 30 fps = 5,400 frames ≈ **$1.08** (computed, S-PRICING). | 04 §2, 06 R1 |
| A17 | ACCEPT substance; DISPUTE "High" | One research commit, with governance in `proposals/`: both by design (`proposals/README.md` says "NOT INSTALLED"). | None beyond keeping the research/code boundary explicit. | — |
| A18 | ACCEPT | Already noted (TOOLING D4 limit). Rules are guardrails, not enforcement. | Keys never enter an agent's shell environment. GitHub push protection (a user setting). gitleaks pre-commit plus CI secret scan. The rules are tested in the real environment at install. | proposals |
| A19 | ACCEPT | **Root cause:** I estimated capture times ("~16:40", "~16:55 UTC") instead of reading the clock. File mtimes were 14:04–14:24 UTC. The "74" in 08 went stale when 4 governance sources were added (now 78). | Correct both. **New rule:** timestamps come only from `date -u`. Counts come only from a command (`wc -l`), never from memory. | 00, captures, 08, AGENTS.md |
| A20 | PARTIAL | Our C1 already traced the "equally weighted" sentence. On S-EV it describes **application review**, and the guide print shows only 30/25/20/25. The audit treats the two as equal-status conflicting sources. Both weightings are scored either way. | Stays UNRESOLVED. The user may ask in Discord #questions. | 00 C1 |
| A21 | PARTIAL | Track: **the user confirmed Indie** on 2026-10-26 ("yes we are allowed for indie. we are not a startup"). Official Rules: still not found. | Track becomes USER-CONFIRMED. R21 stays open. | 05, 07 |
| A22 | ACCEPT | The benchmark's folder names (passed/failed/not_present/cannot_tell) give away the labels. | Copy to random IDs. The label map is used only by the scorer script. Prompt iteration uses the dev split only. The held-out split is scored **once** and logged. Check that no PDF text or metadata contains a label string. Blinding is procedural and logged, not cryptographic, and we say so. | 06 E3 |
| A23 | ACCEPT | A hash identifies an input or output; it does not show correctness. A schema-valid report shows traceability only. | `ProofReport` → `EvidenceReport`. Each claim carries its evidence class. No tamper-evidence claim without an external anchor. | 04 §1.4, PROTOCOLS |

### 2.1 Score reproduction
The audit's arithmetic matches ours: Parity 7.825 / 7.825, redaction 7.975 / 8.000. We agree that these are subjective estimates and not a probability of winning. File 05 already calls it a "close call".

## 3. Designs adopted (proposed; each enters methodology only after MCQ approval)

### 3.1 Evidence classes (replace "verified")

| Class | Meaning | Report wording |
|---|---|---|
| MACHINE | Deterministic tool output: a veraPDF rule, a schema check, a text diff | "machine check passed (tool, version)" |
| OBSERVED | Recorded behaviour of real assistive technology, e.g. an NVDA speech log | "screen reader read: '…'" |
| MODEL | A model judgment, with model ID and independence level (§3.2) | "model-assessed (Spark, L1)" |
| HUMAN | A named reviewer's decision | "reviewed by <role>" |

Unclassified "verified", "compliant" or "certified" never appears in the UI, report, README or demo.

### 3.2 Independence ladder for second opinions

| Level | Judge | Treat as |
|---|---|---|
| L0 | Same model, same prompt | Not allowed as a verdict |
| L1 | Same model, different prompt or effort | Self-consistency; correlated errors |
| L2 | Different model, same vendor (Glimmer vs Spark) | Second model; partial independence |
| L3 | Deterministic check of the output (render-compare, re-plot numbers, veraPDF) | Independent of model reasoning, but narrow in scope |
| L4 | Observed AT output or a human | Strongest available |

### 3.3 E3 redesign
- **Scope:** the 7 ASSETS'25 criteria, plus a coverage matrix to Matterhorn 1.1 conditions.
- **Protocol:** copy the ASSETS'25 inputs (page images plus criterion-specific extracted data), or disclose every difference.
- **Split:** grouped by base PDF. S-ASSETS25 uses 5 base PDFs per criterion, 35 in total.
  - Dev: 1 base PDF per criterion (7 in total), for prompt iteration.
  - Held-out: the other 4 per criterion (28 in total, about 100 documents), touched once.
- **Primary metric:** false-pass rate (predicted Passed, truth Failed) at a stated coverage, with its 95% Wilson interval.
  - Wilson: `(p + z²/2n ± z·√(p(1−p)/n + z²/4n²)) / (1 + z²/n)`, z = 1.96.
- **Proposed gate (needs approval):** the lane may say "model-assessed" only if the false-pass point estimate is ≤ 0.05 **and** its upper bound is ≤ 0.15, at coverage ≥ 0.5. Otherwise the lane is "reviewer-assist".
- **Secondary metrics:** accuracy with CI; per-label confusion; abstention rate; cost per document.

### 3.4 Budget reservation broker (A14)
- **Reserve:** before each call, reserve the worst-case cost (input estimate × input price + `max_output_tokens` × output price, plus an image upper bound) in SQLite inside `BEGIN IMMEDIATE`. Refuse if spent + reserved > cap.
- **Settle:** after the call, settle the actual usage and release the remainder. A crashed call keeps its reservation until reconciled.
- **Keys and cap:** one key per developer. Proposed cap **$100 of the $150 credit**, down from the $120 draft; the $50 headroom absorbs unknown image-token accounting.
- **Reconcile:** the user compares against the Meta billing page daily. A mismatch above $2 stops calls.
- **Residual risk, stated:** price changes, billing lag, unknown image accounting. No guarantee.

## 4. Decision framework (PARTIAL)
The audit says to choose "only after a discriminating experiment". We agree in principle. But Day 1 of the build is 2026-10-28 (07 §5), and every experiment needs posted credits plus a card (R15), so an open-ended wait would cost build days. Proposal, to be approved by MCQ:
- **Day-1 gate (≤ 6 h, ≤ $10):**
  - E4-lite on 3 real STEM PDFs, local tools, $0.
  - E1 on 30 synthetic equations.
  - E3 on the dev split only.
- **Rule fixed in advance:** if E4-lite fails on 2 of 3 PDFs, **or** E1 is below 75%, Parity's PDF writer is dropped and we go audit-first or HTML-first (file 10). If credits are not posted by the end of Day 1, the pivot decision is made on desk evidence and recorded as such.

## 5. Indian defence and Indian development needs (user request)
- **Defence: rejected, with evidence.**
  - The guide's anti-projects list "anything political or involving war" (S-PG p4).
  - The use policy at dev.meta.ai/use-policy/ prohibits "Military, warfare, nuclear industries or applications, espionage" (S-META-AUP).
    - **Correction (re-check at 17:05 UTC):** that page is labelled **Llama 2**, carries no date, and does not mention Muse or the Model API. Whether it binds Muse API use is UNKNOWN.
    - Search titles also report that in Nov 2024 Meta let US national-security agencies use Llama (THIRD-PARTY, titles only). That exception does not cover an Indian team.
  - A third-party report says the Muse Spark Open licence bans running critical infrastructure (S-BERI-LICENSE, THIRD-PARTY). We did not read the licence itself.
  - **The rejection rests on S-PG alone, which is enough:** "anything political or involving war" is a hackathon disqualifier whatever the AUP says.
  - A dual-use framing would still be screened against the anti-project rule at Stage One. The expected cost is disqualification, so it is not worth exploring.
- **Development needs: in scope**, examined in file 10. Two limits apply:
  - The same (Llama 2-labelled) policy bars "operation of critical infrastructure, transportation technologies, or heavy machinery", and BERI reports a similar bar in the Spark Open licence. We treat it as binding to be safe. Advisory and information tools are outside that bar; controlling the grid, water or transport is inside it (INFERENCE).
  - The medical-advice anti-project rules out diagnosis tools.

## 6. Handed to Codex (needs GitHub; Claude has no GitHub access)
1. A12: read `LICENSE` and the README of `Anukriti12/PDF-Accessibility-Benchmark`. Record the effective licence and whether it covers the base PDFs.
2. A13: confirm the 1.1 split (machine / human / no test) from the Matterhorn 1.1 PDF if Codex can extract it.
3. Check every claim in this file against its cited source and report any we got wrong.

## 7. Process rules adopted from this audit
- Timestamps come only from `date -u`. Counts come only from a command.
- Every capability claim carries an evidence class (§3.1). Every second opinion carries an independence level (§3.2).
- "Not documented" is never written as "absent".
- Any external fact that could reverse the decision (rules, deadlines, licences) is re-checked at the start of each build day.
