# 05 — Track and judging sensitivity

> **Post-audit status (2026-10-26T17:08Z, UNAPPROVED).** Corrections from [09](09_AUDIT_RESPONSE.md) and [10](10_PIVOT_BRAINSTORM.md):
> - **Track: Indie, USER-CONFIRMED** (D4: "yes we are allowed for indie. we are not a startup"). Indie is judged on "creativity, technical ambition, and whether it works" (S-EV). §3's conditional Startup analysis is now history.
> - Re-scoring under Indie, with the pivot candidates: file 10 §4. Parity-PDF rescoped drops to 7.48 / 7.50 there (from 7.83 here) after the audit shrank its claims.


## 1. Scoring model (published so it can be challenged)

- **Scale.** Each criterion is scored 0–10, as the Stage Two rubric requires (S-PG p8). Every score is **INFERENCE with about ±1.0 uncertainty**. These are not predictions of judge scores, and **no win probability is given**.
- **Impact.** Demand evidence, buyer reachability, size of the dated trigger, commercial scale.
- **Meta tooling.** How central and how creative the use is. Using 3 or more distinct Meta capabilities on the critical path scores higher.
- **Tech depth.** Verification, invariants and operability, not raw complexity.
- **Demo.** Visual clarity, how hard it is to fake, the risk that it breaks, and story.

| Finalist | Impact | Meta tooling | Tech depth | Demo | **30/25/20/25** | **25/25/25/25** |
|---|---|---|---|---|---|---|
| Parity (STEM PDF evidence) | 8.0 | 7.3 | 8.0 | 8.0 | 7.83 | 7.83 |
| Policy-driven video redaction | 7.0 | 8.5 | 7.5 | 9.0 | **7.98** | **8.00** |
| Audio description studio | 7.5 | 7.5 | 7.0 | 8.5 | 7.65 | 7.63 |
| Robot data QA | 6.0 | 8.0 | 8.0 | 7.0 | 7.15 | 7.25 |

Parity's Impact was 8.5 before the Allyant desk check. It is 8.0 now, because a Title-II-positioned validation report already exists (S-ALLYANT-AI), so part of the "evidence" story overlaps with an incumbent.

**Reading.** Redaction now leads by **0.15–0.17 under both weightings**. That gap is far inside the ±1 noise. **The rubric estimate does not decide between the top two, and if anything it leans slightly toward redaction.** The recommendation therefore rests on factors outside the rubric, stated openly:

1. **The team's dominant priority is startup-scale commercial potential.** Parity has a dated legal trigger (S-FR) and priced, recurring manual work (S-ASU, S-OSU-SUPPLIERS, S-VENNGAGE). Redaction's largest US buyers get Axon's tool bundled (S-AXON). Parity's story (a blind student cannot read their maths homework) also has broader appeal, which matters for the Viral and Community prizes (INFERENCE).
2. **Data rights.** Parity can use public CC-licensed PDFs. Redaction needs staged footage, and real footage is sensitive.
3. **Why-now.** The 2027/2028 compliance dates and the DOJ's own statement that AI is not yet trusted (S-FR) create a specific opening for *evidence*. Redaction has no dated trigger.
4. **Counterweight, honestly stated.** Redaction is the more visual demo and the stronger Meta-tooling story (SAM 3.1 is central). If the team weighs winning the event above business potential, redaction is a defensible pick (MCQ option).

## 2. Sensitivity: what flips the ranking

Baseline: Parity 7.83 vs redaction 7.98 (weighted).

| Scenario | Effect | New score (weighted) | Leader |
|---|---|---|---|
| Allyant's trial shows evidence on the judgment checks (full overlap) | Parity Impact −1.5 | Parity 7.38 | **Redaction** (clearly) |
| Equation round-trip fails K1 and chart check fails K2 | Parity Impact −1, Tech −0.5 | Parity 7.43 | **Redaction** |
| Wonder tester fails K5 (scripted fallback) | Parity Tooling −0.7, Demo −0.5 | Parity 7.53 | **Redaction** |
| Glimmer self-hosted (Q5 = yes) + SAM proves useful (E7) | Parity Tooling +0.7 | Parity 8.00 | Tie |
| E3 ≥0.85 and Information Parity validates (E5) | Parity Tech +0.5, Impact +0.5 | Parity 8.08 | Parity |
| Inference cost doubles | Parity still <$0.12/page vs $3+/page manual | 7.83 | No change |
| Judges read "AI for education chatbot" (R9) | Stage One risk | — | Mitigate in the first 20 s |
| Redaction: SAM tracking poor on motion | Redaction Demo −2, Tech −1 | Redaction 7.28 | Parity |
| Redaction: staged footage judged unconvincing | Redaction Impact −1 | Redaction 7.68 | Parity |

**Conclusion.** This is a **close call**. Parity is recommended because of commercial priority, the dated trigger and data rights, not because of the rubric estimate. Its case gets stronger or weaker on Day 1 evidence (E3, E1, E2, E7) and on the competitor trial. The pivot to redaction is pre-planned (file 07, D7). If the team values the event outcome above the business case, redaction is the defensible pick today.

## 3. Track analysis: Indie vs Startup

| | Indie | Startup |
|---|---|---|
| Official text (S-EV) | "For individual builders and students. Judged on creativity, technical ambition, and whether it works." | "For teams and founders building a real product. Judged on technical execution and whether it holds up in production." |
| Eligibility for us | **UNCLEAR.** "Individual builders" could exclude teams or simply mean non-companies. | **UNCLEAR.** "Teams and founders" fits 2 people, but whether an entity or existing product is required is UNKNOWN (Q1). |
| Existing-code allowance | Not stated, so assume from scratch | Allowed with disclosure (R5). **Competitors may arrive with mature products and real users.** |
| Prizes (S-PG p9–10) | $150K / $100K / $75K / $50K / $25K | $250K / $150K / $75K / $50K / $25K |
| Fit with a 9-day, from-scratch Parity | **High.** Ambition, creativity and "it works" match a verification-heavy kernel. | **Medium.** "Holds up in production" favors teams with deployed products. Our best counter is visible operability: replay, audit trail, budget guard, tests, hosted demo. |
| Number of entrants per track | UNKNOWN | UNKNOWN |
| Track change after application | UNKNOWN (Q1) | UNKNOWN (Q1) |

**Recommendation: Indie, conditionally (confidence medium-low).**
- **Reason.** A from-scratch 9-day product competes better on "creativity, technical ambition, and whether it works" than on "holds up in production" against startups allowed to bring existing products.
- **Conditions:**
  - (a) organizers confirm a 2-person team may enter Indie (Q1);
  - (b) the track was not already fixed by the application.
- **If (a) or (b) fails,** enter Startup and shift emphasis toward production evidence: hosted demo, uptime, replay, tests, cost ledger, a pilot letter if one can be obtained honestly.
- **Do not choose Startup only because the prize is larger.** The larger prize comes with a harder field (INFERENCE).

## 4. Theme
"Build for Your World" (S-PG p1) fits a real-world compliance and accessibility problem (INFERENCE). "Push the Frontier" would fit only if the Wonder screen-reader agent becomes the headline. Keep Build for Your World unless the Wonder result is outstanding.

## 5. Bonus prize fit (optional upside, INFERENCE)

| Bonus | Fit | Condition |
|---|---|---|
| Best Agentic Use-Case ($5K) | Good | Verifier loop plus Wonder tester |
| Best Creative Build ($5K, Muse Image/Wonder) | Possible | Wonder is used meaningfully |
| Best Open-Weights Build ($10K) | Possible | Glimmer self-hosted (Q5) |
| Most Viral ($20K) / Community ($10K) | Possible | Needs public posting, which needs user approval |
