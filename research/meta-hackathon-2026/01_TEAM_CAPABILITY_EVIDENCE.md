# 01 — Team capacity

**Scope limit (user instruction, matching mandate V2 §0).** No GitHub profiles, repositories, past projects, résumés, skills or interests were opened or used. This file records **capacity only**. Mandate v1 §3 asked for a profile audit; the user overrode it explicitly (LEDGER D1). Unknown abilities are listed as things to check *after* product selection, never as reasons to rank ideas.

## 1. Time budget

| Item | Value | Label |
|---|---|---|
| Builders | 2, both accepted | supplied fact |
| Stated availability | 8+ h/day each | supplied fact (stated, not verified) |
| Window | Now (2026-10-26 ~22:00 IST) → internal submit 2026-11-04 22:00 IST = 9.0 days | computed (R1 in file 00) |
| Hard deadline | 2026-11-05 07:30 IST | VERIFIED + computed |
| Person-hours at 8 h/day | 2 × 8 × 9 = **144 ph** | computed |
| Person-hours at 12 h/day | 2 × 12 × 9 = 216 ph | computed. Upside only: do not plan on it. |

Planning rule: **plan on 144 ph** and treat extra hours as buffer, not scope. Reason: the user offered "24 hours for next 10 days", but sustained 16+ h days raise defect rates late in a build. This is general engineering experience, labeled INFERENCE, not a cited study.

## 2. Resources reported by the participants (not independently verified)

| Resource | Status | Use |
|---|---|---|
| Meta Model API, credits "visible" | Reported. Posting of $150 × 2 is UNKNOWN. A card is required to call (R15). | The product's core models |
| Gemini API / Google AI Studio | Reported. Quota UNKNOWN. | Optional **independent baseline** in experiments (E3). Not in the product's core path, because Meta must be central (R7). |
| Claude Code subscription | Reported; in use now | Build agent |
| Codex subscription | Reported | Second build agent / cross-reviewer |
| Docker Desktop / WSL2 | Reported working | Runs veraPDF (Java) and other tools without host installs |
| Partner credits (Baseten / Modal / Fireworks) | **Not granted** | Budget $0 |
| Host OS | Windows 11 Home (OBSERVED from the session environment) | — |
| GPU / VRAM | **UNKNOWN (Q5)** | Decides whether Glimmer (30B) can be self-hosted for the open-weights bonus |

## 3. Money budget (₹0 extra cash)

- Credits: up to $300 if both accounts post $150. Each call needs a card on the account, and the spend limit only notifies (R15).
- Required control: a **code-level budget guard**. Every Meta call goes through one client that checks a running cost ledger and refuses calls once projected spend passes a hard stop (proposal: $120 per account, leaving a $30 margin for pricing or rounding surprises). This is an engineering decision for approval, not a rule.
- Contributor mode (about 12× cheaper on Spark) may be used only for **public, licensed** test documents, because contributor content "may be used" for training (S-MODELS).

## 4. Delivery demand vs capacity for the recommended product (INFERENCE)

Estimate for Parity's competition kernel (file 04):

| Work package | ph | Risk |
|---|---|---|
| Day-1 decisive experiments E1–E4 (file 06) | 16 | Low |
| Ingest + Spark page-understanding schema | 18 | Medium |
| Tagged-PDF writer (pikepdf structure tree) + HTML/MathML twin | 30 | **High**: the main technical risk (K3) |
| veraPDF harness + verifiers V2–V5 | 24 | Medium |
| Review UI + proof report | 22 | Medium |
| Wonder "screen-reader tester" (stretch) | 10 | High; can be replaced by the scripted fallback |
| Demo recording, editing, README, new-work disclosure | 16 | Low |
| Buffer | 8 | — |
| **Total** | **144** | Fits exactly, with no slack beyond the buffer |

Implication: the scope must be cut by kill-criteria gates (K1–K5, file 07), not by optimism. If K3 fails by Day 4, the writer becomes HTML-only. That saves about 15 ph.

## 5. To verify after product selection (not before)

1. Who owns which work package. Assign by the team's own choice: this file does not assess skill.
2. GPU availability (Q5).
3. Who adds the card and who holds which API key (Q6).
4. Whether Java/Docker can run veraPDF on the host (a 5-minute check once installs are approved).
