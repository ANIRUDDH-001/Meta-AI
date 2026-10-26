# 08 — Executive verdict

> **Post-audit status (2026-10-26T17:08Z, UNAPPROVED).** Corrections from [09](09_AUDIT_RESPONSE.md) and [10](10_PIVOT_BRAINSTORM.md):
> - **This verdict is superseded pending the user's choice.** The audit (09) shrank Parity-PDF's claims, and the pivot brainstorm (10) ranks C4 (video privacy guard, 8.50) and C3 (blindfolded web agent, 8.35) above rescoped Parity-PDF (7.48). Those scores are INFERENCE ±1.
> - **Recommendation now:** a Day-1 discriminating spike between C3 and C4 (10 §5).
> - **Track:** Indie, user-confirmed.
> - **Corrections:** the source count was 78, not 74; Matterhorn 1.1 is current; wording is now "evidence", not "proof".


Status: **research complete, decision PENDING the user's MCQ answers.** Nothing has been built, called or installed.

## 1. Recommendation

**Parity — accessibility you can prove, starting with STEM PDFs.** This is a close call (file 05).

- **Customer outcome.** An accessibility office remediates a STEM PDF in minutes rather than hours. It gets an auditable report showing what was checked, how it was checked, and what still needs a human.
- **Conditional dimensions.**
  - Every accuracy figure is UNTESTED (E1–E5).
  - Willingness to pay is UNTESTED (E8).
  - Track is conditional (Q1).
  - Differentiation over Allyant is partly UNKNOWN (D7, trial not inspected).
- **Customer and buyer.**
  - User: accessibility or disability-services coordinators at public universities and agencies.
  - Buyer: the institution's accessibility, IT or procurement office.
  - End beneficiary: blind and low-vision students reading STEM material.

## 2. Evidence for the problem (primary where available)

| Claim | Evidence | Label |
|---|---|---|
| Dated legal trigger | DOJ Title II rule: WCAG 2.1 AA by **2027-04-26** (≥50K population) and **2028-04-26** (smaller entities) | OBSERVED (S-FR) |
| The regulator does not trust AI remediation | 91 FR 20907: generative AI "does not yet reliably automate" remediation at scale | OBSERVED (S-FR) |
| STEM is the hard case | Correspondence quoted in 91 FR 20905 says AI "cannot reliably automate" STEM remediation; the CNI report names math and figures as the main challenge | OBSERVED / THIRD-PARTY |
| Human judgment is structural | Matterhorn (split per 1.02; 1.1 is current, same 136 total): 47 of 136 failure conditions need human judgment | PRIMARY (S-MATTERHORN) |
| Manual work is priced | $3–25 per page, clusters at $5–8 | THIRD-PARTY (S-ASU, S-OSU-SUPPLIERS, S-VENNGAGE) |
| Scale | OSU reports hundreds of thousands of PDFs | THIRD-PARTY |

## 3. Substitutes, and the advantage hypothesis

The serious substitutes are:
- **Allyant CommonLook Edu:** STEM tagging, math alt text, a Title II validation report and a System of Record.
- **YuJa Panorama:** MathML in its HTML format.
- **Anthology Ally:** MathML from Word only.
- **Adobe Auto-Tag, Equidox, Mathpix,** and the open ASU/OSU pipeline.
- **Non-AI:** manual vendors at $3–25 per page, and in-house staff using Acrobat and PAC.

Details are in file 03.

**Advantage hypothesis.** Each part is a hypothesis, not a fact, and each has a test:

| # | Claim | Falsified by |
|---|---|---|
| A1 | Evidence on the human-judgment checks, not only pass/fail counts | Allyant trial shows the same (D7); E3 <0.80 |
| A2 | Math as navigable MathML, checked by round-trip | E1 accuracy <85% or catch rate <50% (K1) |
| A3 | A screen reader operated by an agent confirms the result | E6 <4/5 runs (K5) |
| A4 | A neutral auditor that can grade any vendor's output | Customer interviews show no demand (E8) |
| A5 | An outcome metric (Information Parity) rather than rule counts | E5 shows the metric does not separate good from bad documents |

**What is already confirmed not to differentiate:** "we produce a compliance report" (S-ALLYANT-AI), and "AI tags STEM" (F21).

## 4. Why now, and why Meta

- **Why now.**
  - The compliance dates are 6 and 18 months away.
  - The regulator's stated distrust of AI creates demand for *evidence*, not more automation.
  - Agents increasingly read the same accessibility tree that screen readers use (S-OPENAI-ATLAS, a primary-source claim), so accessible structure also becomes agent-readable structure.
- **Why Meta.** Each model is on the critical path, not added for show:

  | Capability | Role | Status |
  |---|---|---|
  | Muse Spark | Page understanding with structured output over PDF and images; whole-document consistency over a 1M-token context | Documented (S-MODELS) |
  | Muse Wonder | Computer use to operate NVDA like a blind user | Documented; our use is UNTESTED (E6) |
  | SAM 3.1 | Chart-region masks | UNTESTED (E7); claimed only if it helps |
  | Muse Glimmer | Self-hosted second-opinion judge | Only if a GPU is available (Q5) |

  Credits are **not assumed**. They need a card on the account, and posting must be checked on Day 0 (F7, R15).

## 5. Strongest runner-up: policy-driven video redaction

- **What it is.** SAM 3.1 tracking, Voice Transcribe and a Spark policy engine for public-records video.
- **Rubric estimate.** 7.98 / 8.00, slightly *above* Parity's 7.83 / 7.83, within the ±1 noise.
- **Strengths:**
  - the most visual demo;
  - the most central Meta tooling (SAM is the product);
  - measured manual costs (1–8 staff hours per video hour).
- **Weaknesses:**
  - Axon bundles redaction for its largest US buyers;
  - no dated trigger;
  - staged footage is needed, because real footage is sensitive.
- **Pick it instead if** the team values the event outcome over the business case, or if the D7 gate fires.

## 6. Failure modes (what kills Parity)

1. **Differentiation collapses.** Allyant's report already carries judgment-check evidence (D7), so Impact falls to about 6.5 and the score to 7.38.
2. **The PDF writer cannot produce valid PDF/UA in 9 days (K3).** Fall back to the reconstructed PDF, then HTML only. The demo is weaker but survives.
3. **The AI-judged lane is not accurate enough (K4, E3 <0.80).** It becomes "reviewer-assist". The evidence claim weakens.
4. **The Wonder tester is unreliable (K5).** A scripted path replaces it, and the "agent as blind user" moment is lost.
5. **The anti-project misread (R9).** Judges file it as an "AI for education" tool. Mitigation: no chat, compliance framing in the first 20 seconds.
6. **Distribution.** Incumbents sit inside the LMS. That is a business risk after the event, not a risk to the event.

## 7. Evidence gaps (decisive first)

| Gap | Resolves | Who | Cost |
|---|---|---|---|
| Allyant trial: does the validation report carry evidence on the judgment checks? | D7 | **User** (account creation is prohibited for the agent) | ₹0 |
| Stage Two weighting (C1) and Startup eligibility (Q1, Q2) | Track choice, score sensitivity | User asks organizers (Discord #questions) | ₹0 |
| Credits posted and card holder (Q6) | Any metered call | User | ₹0 |
| GPU ≥24 GB VRAM (Q5) | Glimmer self-host, open-weights bonus | User | ₹0 |
| E3, E4, E1+E2 | K4, K3, K1, K2 | Agent, after authorization | ≤$28 of granted credit |
| Spark image-token accounting (U7) | Unit economics | Measured by the first E1 call | Included above |
| Willingness to pay (E8) | Business case | User sends the messages | ₹0 |

## 8. Conditions for reversal

- **Switch to redaction (D7)** if any of these happens:
  - E3 <0.70;
  - K1 and K2 both fail;
  - the Allyant trial shows judgment-check evidence.

  Decide on Day 2 at the latest.
- **Narrow Parity to an audit-only product** ("grade any remediated PDF") if K3 fails but E3 passes. The neutral-auditor wedge (A4) needs no PDF writer.
- **Drop the Wonder segment** if K5 fails by Day 6.

## 9. Track

**Indie, conditionally (medium-low confidence).** A from-scratch 9-day build competes better on "creativity, technical ambition, and whether it works" than against startups bringing existing products.
- **Conditions:**
  - organizers confirm that 2 people may enter Indie (Q1);
  - the track was not already fixed by the application.
- **Otherwise,** enter Startup with production evidence: hosted demo, replay, tests and a cost ledger.

Both weightings are preserved: 30/25/20/25 and 25/25/25/25 (file 05).

## 10. Three-minute demo

The full storyboard, with a live column and a fallback column, is in file 04 §1.6. The story spine:

> a harm you can hear (NVDA reading garbage) → the 2027 deadline → a regulator that does not trust AI → evidence attached to every check → an agent operating a screen reader confirms it → honest, measured numbers.

Placeholders, such as the Information Parity before/after figures, are shown only once measured.

## 11. Kernel vs platform

- **H1 kernel (by Nov 4).** STEM PDF → tagged PDF + MathML HTML twin + evidence report + human review lane; Wonder tester as a stretch.
- **H2 (to Apr 2027).** Batch API, LMS sync, self-hosting for FERPA-sensitive files, one pilot.
- **H3 platform.** An evidence layer for all content (slides, Word, video AD and captions, web), certifying third-party remediation.

## 12. Next authorized action

All of this needs user approval:

1. **User (₹0, Day 0):**
   - answer the MCQs;
   - check credits and the card;
   - ask organizers Q1–Q4;
   - start the Allyant 7-day trial and screenshot one validation report.
2. **Agent (≤$28, Day 1, after explicit go-ahead):** E3 → E4 → E1+E2, pre-registered in file 06.
3. **Optional hedge (about $0.18):** redaction R1 on three self-filmed clips. This keeps the runner-up decision evidence-based.

## 13. Acceptance checklist (V2 §10), verified

| Check | Result | How verified |
|---|---|---|
| No participant profiles, repositories, projects, backgrounds or interests inspected or used | **PASS** | No GitHub or profile URL was fetched. `01` records capacity only. The GitHub MCP failed to connect and was not used. |
| Ideas came from external problem evidence | **PASS** | All 13 hypotheses in `02` cite external demand sources. Four were screened at desk stage only, and this is disclosed (F36). |
| Serious commercial alternatives and non-AI workarounds checked | **PASS** | `03`: 14 parity rows, including manual vendors and in-house tooling; the Allyant brochure was read |
| Every number and capability claim has provenance and uncertainty | **PASS, with disclosed gaps** | Source IDs in `sources.jsonl` (78 lines at this snapshot; 110 by `wc -l` on 2026-10-26 after the red-team response). Scores labeled INFERENCE ±1. Unverified products listed (F35). |
| Advantage and novelty are hypotheses | **PASS** | §3 table A1–A5, each with a falsifier. `03` §1.5. |
| Zero paid usage, product changes or implementation | **PASS** | No Meta API call, no install, no account, no form, no message, no commit. Only research files and one local text extraction of a downloaded brochure. |
| Meta functionality central; capabilities and credits not assumed | **PASS** | §4. Wonder, SAM and Glimmer use is marked UNTESTED or conditional. The credits need a card and are checked on Day 0. |
| Two-person window and 3-minute demo evaluated | **PASS** | `01`: 144 person-hours, work packages. `04` §1.6 storyboard with fallbacks. `07` §5 schedule. |
| Both weightings and track conditions preserved | **PASS** | `05` §1–3; C1 kept open |
| Falsification conditions; the recommendation can be rejected | **PASS** | §6, §8; K1–K5 and D7 in `07` |

## 14. File map (v1 names used; V2 equivalents)

| V2 required output | File in this folder |
|---|---|
| 00 Rules and source register | `00_SOURCE_REGISTER.md` |
| 01 Market problem landscape | `02_OPPORTUNITY_LANDSCAPE.md` (`01_TEAM_CAPABILITY_EVIDENCE.md` is capacity only) |
| 02 Competitor and substitution matrix | `03_COMPETITOR_CAPABILITY_MATRIX.md` |
| 03 Product candidates and commercial case | `04_FINALIST_PRODUCT_BRIEFS.md` |
| 04 Track and judging scenarios | `05_TRACK_AND_JUDGING_SENSITIVITY.md` |
| 05 Architecture and platform horizons | `04_FINALIST_PRODUCT_BRIEFS.md` §1.4, §1.9 |
| 06 Falsification experiment designs | `06_VALIDATION_EXPERIMENT_DESIGNS.md` |
| 07 Decisions, risks and unknowns | `07_DECISION_AND_RISK_LEDGER.md` |
| 08 Executive recommendation | this file |
| sources.jsonl | `sources.jsonl` |
| Running record (not required) | `LEDGER.md`, `resources/source_captures.md` |
