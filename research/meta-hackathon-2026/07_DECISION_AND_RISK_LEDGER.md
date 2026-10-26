# 07 — Decision and risk ledger

> **Post-audit status (2026-10-26T17:08Z, UNAPPROVED).** Corrections from [09](09_AUDIT_RESPONSE.md) and [10](10_PIVOT_BRAINSTORM.md):
> - **D4 track: ACCEPTED — Indie** (user, 2026-10-26).
> - **D3 product: reopened.** Pivot candidates C3/C4 (file 10). The decision goes through a Day-1 spike (D13 in LEDGER; it supersedes D7 below).
> - **K4 changes** from "E3 accuracy <0.80" to the false-pass gate in 06 (09 §3.3).
> - **New risks:**
>   - DOJ deadline contested both ways (F41, F42).
>   - MathML vs PDF/UA-1 contradiction (F44).
>   - ASSETS'25 licence unknown (A12; Codex task).
>   - Meta use-policy scope for Muse unknown (F40).
> - **Budget:** proposed cap $100 of the $150 credit, enforced by a reservation broker (09 §3.4). The earlier $120 is superseded if the user approves.


**Status values.** ACCEPTED = decided, with the user's approval where needed · PROPOSED = awaiting the user's MCQ answer · REJECTED · UNKNOWN.
**Owner.** "User" means the participants decide. "Research" means the evidence decided it.

## 1. Decisions

| ID | Decision | Status | Owner | Basis | Reversal condition |
|---|---|---|---|---|---|
| D1 | Profile-free investigation: no GitHub, skills or past work | ACCEPTED | User | User instruction; mandate V2 §0 | — |
| D2 | Outputs in `research/meta-hackathon-2026/` (v1 filenames) | ACCEPTED | User | "put inside the folder only which you are working in" | — |
| D3 | Recommend **Parity** (STEM PDF evidence) as the product | PROPOSED | User | Files 02–05 | Pivot gate (D7) |
| D4 | Track: Indie, conditionally | PROPOSED | User | File 05 §3 | Q1 answer |
| D5 | Approval granularity: per-task spec approval through MCQ | PROPOSED | User | Governance draft | User preference |
| D6 | Install governance drafts (CLAUDE.md / AGENTS.md) | PROPOSED | User | `proposals/` | — |
| D7 | **Pivot gate.** If E3 <0.70, or both K1 and K2 fail, or the Allyant report already does per-check human-judgment evidence → switch to redaction (finalist 2) on Day 2. **Desk check done 2026-10-26: partial overlap.** A Title-II-positioned "PDF Document Validation Report" with "passed, failed, and warning issues" exists, plus a "System of Record" (S-ALLYANT-AI). Whether it carries evidence for the 47 human-judgment checks is still UNKNOWN. That can only be settled by inspecting the 7-day trial, which needs an account the user creates (prohibited for the agent) | PROPOSED | User | File 05 §2; S-ALLYANT-AI | Trial shows judgment-check evidence → pivot |
| D8 | Budget guard in code, with a hard stop of $120 per account (superseded by the proposed $100 cap, 09 §3.4) | PROPOSED | User | R15 (notification only) | — |
| D9 | No PyMuPDF (AGPL) in the shipped product; use pypdfium2 | PROPOSED | User | Licensing | If the repo license is AGPL anyway |
| D10 | Contributor mode only for licensed or synthetic fixtures | PROPOSED | User | S-MODELS (training use) | — |
| X1 | Fisheries EM | REJECTED | Research | No public labeled footage with rights (R6) | Rights-clean dataset found |
| X2 | Lab animal behavior scoring | REJECTED | Research | Rodent-Bench capability evidence (S-RODENT) | — |
| X3 | Video → SOP | REJECTED | Research | Crowded (S-SOP), no falsifiable edge | — |
| X4 | Analog gauges | REJECTED | Research | Feature-level; anti-project risk (R9) | — |
| X5 | Asset register from video | REJECTED | Research | Thin evidence (S-CMMS) | — |
| X6–X9 | Construction, insurance, bug-repro, prior-auth | REJECTED (desk only) | Research | INFERENCE only, no searches (F36) | Revisit only with evidence |
| U1 | Startup-track eligibility for 2 people | UNKNOWN | Organizers | Q1 | — |
| U2 | Stage Two weighting | UNKNOWN | Organizers | Q2 / C1 | — |
| U3 | Official Rules (IP, OSS) | UNKNOWN | Organizers | Q3 | — |
| U4 | "Live product" must be a hosted URL? | UNKNOWN | Organizers | Q4 | — |
| U5 | GPU ≥24 GB VRAM | UNKNOWN | User | Q5 | — |
| U6 | Card holder / key owner | UNKNOWN | User | Q6 | — |
| U7 | Spark image-token accounting | UNKNOWN | Research | Not documented in pages read | First E1 call measures it |

## 2. Kill criteria (evaluate in the first ~48 h of build; pre-registered in file 06)

| ID | Condition | Action |
|---|---|---|
| K1 | Equation accuracy <85%, or round-trip catches <50% of the errors | Drop the "checked math" badge; math always goes to the human lane |
| K2 | Fewer than 75% of charts fully within 5% | Charts become amber "needs human" only |
| K3 | Fewer than 8/10 documents pass veraPDF by Day 4 | Design A → B → HTML-only |
| K4 | E3 accuracy <0.80 | Reposition: "reviewer-assist with evidence", not "AI-checked" |
| K5 | Wonder succeeds in fewer than 4/5 runs by Day 6 | Scripted keyboard path in the demo; Wonder claim removed |
| KP | Pivot gate D7 | Switch to finalist 2 |

## 3. Red team

### 3.1 Skeptical customer (accessibility coordinator)
- **"We already have Ally / Panorama in the LMS."**
  - Those tools give an instructor score and alternative formats.
  - Ally's math support is Word-only (S-ALLY), and Panorama's MathML lives in the HTML format (S-YUJA).
  - Parity produces the PDF itself plus per-check evidence, and it can audit their outputs.
  - **Still a risk:** the coordinator may prefer one vendor (E8).
- **"Can I file your evidence report with OCR or the DOJ?"**
  - Unknown. No regulator accepts any specific vendor report. We must not claim compliance certification.
  - Wording: "evidence report", **never** "certified compliant".
- **"FERPA: you are sending our files to an AI API."**
  - Standard mode content is not used for training (S-MODELS).
  - Glimmer self-host is planned for H2 (Q5).
  - A contract or DPA is needed for a pilot, which is an H2 task.
- **"AI alt text has hurt our users before."** Generated text is labeled. Low-confidence items go to humans. Information Parity measures the user outcome rather than assuming it.

### 3.2 Incumbent product owner (e.g. Allyant / YuJa)
- **"We can add an LLM judge next quarter."**
  - True. The moat is not the model call.
  - Parity's defensible position is a **neutral auditor** with a public benchmark and an AT-operated test. A vendor grading its own output has a conflict.
  - Weak point, acknowledged: incumbents own distribution.
- **"Our validation report already does this."**
  - **Partly true (S-ALLYANT-AI).** Allyant's education brochure lists "PDF Document Validation Reports" positioned for "ADA Title II", with "passed, failed, and warning issues; and detailed results", and a "System of Record" for remediation history. It also generates *alt text* for math.
  - So "we give you a compliance report" is **not** a differentiator. The remaining claims are narrower:
    1. evidence for each of the 47 human-judgment checks;
    2. math as navigable MathML rather than alt text;
    3. a screen reader operated by an agent;
    4. a neutral auditor that can grade CommonLook's output too.
  - Not yet known: whether the report covers the judgment checks with evidence. **Inspect the trial before the build commits (D7).** If it does, pivot.
- **"Your 9-day PDF writer will break on real documents."**
  - Probably, on many of them (INFERENCE).
  - The kernel targets a defined class: born-digital STEM.
  - It fails safe: partial results go to `needs_human`, and veraPDF gates every output.

### 3.3 Competition judge watching the 3-minute video
- **"Is this a wrapper?"**
  - Show the deterministic validators (veraPDF), render-and-compare evidence, and the second-opinion judge.
  - Show the measured benchmark number (E3) and the Wonder agent operating AT.
  - Multi-model, multi-check, measured.
- **"Is this an 'AI for education chatbot'?" (R9)** There is no chat anywhere. It is document infrastructure for compliance. Say so in the first 20 seconds.
- **"Did you build this during the event?"** A NEW-WORK ledger plus an "OSS we stand on" credit card in the video (R4).
- **"Is it live?"** Show the live run first. Replay mode exists, but is used only if the network fails, and the video discloses it.
- **"Why Meta?"**
  - Spark's 1M-context multimodal pass and Wonder's computer use (operating NVDA) are central.
  - SAM and Glimmer are claimed only if E7 and Q5 pass. No decorative API calls.

**Red-team verdict.** The thesis survives **conditionally, and narrower than first drafted**. The free desk check found that Allyant's report exists and is pitched for Title II, which took Parity's Impact from 8.5 to 8.0 (file 05). What remains open is whether that report gives evidence for the human-judgment checks. Only the trial can show that, and only the user can open the trial account. Until then, Parity's lead over redaction comes from factors outside the rubric, not from the rubric estimate.

## 4. Risk register

| Risk | Likelihood | Impact | Mitigation | Trigger |
|---|---|---|---|---|
| PDF writer invalid (K3) | High | High | Design B and HTML fallback; veraPDF in CI | Day 4 |
| Credits not posted / no card | Medium | Blocking | User checks on Day 0; budget guard | Day 0 |
| Spend overrun (notification only) | Medium | High | Budget guard + cost ledger + replay cache | Any call |
| API key leaked in the public repo | Medium | High | `.env` git-ignored, pre-commit secret scan, keys never in the client | Every commit |
| Prompt injection via a PDF | Medium | Medium | Data-only prompts, deterministic overrides, AT10 | — |
| Wonder computer-use acts on the host | Low | High | VM / separate account, human acknowledges safety checks | E6 |
| License violation (fixtures, AGPL) | Medium | High | License ledger per fixture; pypdfium2 | Each fixture |
| Rubric misread as anti-project | Low | High | Framing in the first 20 s | Script review |
| Demo network failure | Medium | High | Replay mode, pre-recorded segments | Recording day |
| Schedule slip | High | High | Feature freeze 2026-11-02 23:59 IST; record on Nov 3 | Daily STATE review |
| Late submission | Low | Fatal | Internal submit 2026-11-04 22:00 IST | — |
| Official Rules contradict assumptions | Low | High | Q3; re-check the event page daily (R23) | — |

## 5. Proposed schedule (IST, for approval)

| Day | Date | Gate |
|---|---|---|
| 0 | Oct 26 | Approvals, credits/card check, Allyant report inspection, repo + governance install |
| 1 | Oct 27 (corrected from "Oct 28"; 12 RT07) | E3, E4, E1, E2 → pivot gate D7. Superseded by the probes in 10 §5 |
| 2–3 | Oct 29–30 | Walking skeleton end-to-end (ingest → Spark → writer → veraPDF → report) |
| 4 | Oct 31 | K3 decision; review UI |
| 5–6 | Nov 1–2 | Verifiers, Information Parity, Wonder (K5 Day 6); **feature freeze Nov 2 23:59** |
| 7 | Nov 3 | Record and edit the demo; README; new-work ledger |
| 8 | Nov 4 | Buffer; submit by 22:00 IST (hard deadline Nov 5 07:30 IST) |

> **Correction (2026-10-26, 12 RT07):** the building period is Oct 27 – Nov 4 (guide p4), so there are 9 build days and Day 1 is Oct 27. Days 2–8 above are the Parity-only plan, one day late against the corrected Day 1. They are re-planned only if Parity-PDF is chosen. The current Day-1 plan is 10 §5 and `proposals/docs/ledger/PLAN.md`.
