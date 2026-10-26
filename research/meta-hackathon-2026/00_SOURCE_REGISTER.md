# 00 — Rules and source register

Round 1 retrieved 2026-10-26 from about 13:20 UTC (first saved capture 13:32 UTC by file mtime) to 14:24 UTC (last file mtime). Round 2 (audit response and pivot research) ran 16:42–16:58 UTC, taken from session transcript timestamps. Earlier wording said "13:20–16:30 UTC"; that was an estimate, not a clock reading (audit A19). Every source has a stable ID, and its full record is in [`sources.jsonl`](sources.jsonl) (110 records by `wc -l` on 2026-10-26, after S-CC-SANDBOX, S-LOOKR and S-IMAGO were added; 107 when the red team counted, 12 RT26). Raw quotes are in [`resources/source_captures.md`](resources/source_captures.md), and the running fact list is in [`LEDGER.md`](LEDGER.md) (F1–F58).

Evidence labels: **OBSERVED** · **PRIMARY-SOURCE CLAIM** · **THIRD-PARTY REPORT** · **INFERENCE** · **UNKNOWN/BLOCKED**.

## 1. Principal sources

| ID | What | Integrity |
|---|---|---|
| S-PG | `meta details.pdf`: a print of the authenticated Details page (11 pp, image-only). Pages were rendered to `resources/guide_p01..p11.png` and read visually. | SHA-256 `3e1ed89e8346a763508740e1302e260ca63c4d676f8dae492a016052489b5b1a`. The right edge of the rubric and bonus tables is clipped in the print. |
| S-EV | Public event page, cerebralvalley.ai/e/meta-ai-developer-hackathon | Read in the built-in browser. `/details` shows only a shell when you are not signed in. |
| S-MODELS, S-PRICING, S-FILES, S-CU, S-SEG, S-VIDEO, S-WONDER, S-GLIMMER, S-SPARK-OPEN | Meta Model API docs on dev.meta.ai | Fetch summaries only (PRIMARY-SOURCE CLAIM). None of it was tested by calling the API: no paid usage. |
| S-FR | DOJ interim final rule (IFR) 91 FR 20902–20912, retrieved from GovInfo. The PDF and extracted text are in `resources/`. | SHA-256 `198455d18d3ad17d7b08ce3da20960a75e63c42d2da04f36faceb3561fa482d2`. Quotes are verified against the text. |

## 2. Rules matrix

| # | Rule | Exact source / quote | Status | Applies to us | Ambiguity | How to resolve | Consequence |
|---|---|---|---|---|---|---|---|
| R1 | Deadline | S-PG p3: "Wed, Nov 4 \| 9:00 PM … Submissions due via the CV platform"; p3 "All times are in Eastern Time (ET)"; p7 "9:00 PM EST"; S-EV "9:00 PM ET" | VERIFIED + computed | Yes | ET vs EST: no conflict, because US DST ends Sun 2026-11-01, so 9 PM ET on Nov 4 is EST = **2026-11-05 07:30 IST** | none needed | Plan an internal submit time of **2026-11-04 22:00 IST** (9.5 h buffer). "Late submissions won't be considered" (p7). |
| R2 | Team size | p4: "A maximum of four participants per team. Solo participants are allowed." | VERIFIED | 2 people is fine | — | — | — |
| R3 | Public repo | p4: "Repositories must be public." p7: repo public, video accessible, everyone listed | VERIFIED | Yes | When the repo must be public (submission time vs whole event) is not stated | Ask in Discord #questions | Keep secrets out of git history from the first commit. |
| R4 | New work only | p4: demo "must only highlight the specific features, code, and functionality that you built during the Hackathon … Failure to clearly identify your original contributions will result in immediate disqualification" | VERIFIED | Yes | Whether OSS dependencies (veraPDF, pikepdf…) count as "not ours": INFERENCE says libraries are fine if declared | Ask (Q3) | Keep a **NEW-WORK ledger** and an "Open-source we stand on" section in the README and demo. |
| R5 | Existing codebase | p4: "Startups may build on existing products or codebases, but you must clearly identify what was newly developed" | VERIFIED | Only matters for Startup | No equivalent sentence for Indie, so assume Indie = from scratch | — | We build from scratch either way, so there is no exposure. |
| R6 | Rights to assets | p4: banned to "use code, data, or assets you do not have the rights to" | VERIFIED | Yes: demo PDFs, fonts, test data | — | — | Demo corpus must be CC-BY / public domain / self-made, with a license ledger. |
| R7 | Meta usage (Stage One gate) | p8: project "reasonably used Meta Model API and/or Meta's open-weight models to build the project in the Hackathon" | VERIFIED | Yes | — | — | Meta models must sit on the critical path, not in a side feature. |
| R8 | Themes | p1: "Build for Your World" / "Push the Frontier" | VERIFIED | Pick one | — | — | Parity fits "Build for Your World" (INFERENCE). |
| R9 | Anti-projects | p4: medical advice, basic RAG, simple image analyzers, simple "AI for Education" chatbots, job screener, nutrition coach, personality analyzers, sports, political/war; "not an exhaustive list" | VERIFIED | Screen every idea | Is accessibility for course PDFs "AI for education"? INFERENCE: no. It is document remediation infrastructure, not a chatbot. | Frame it as compliance / document infrastructure in the demo | A judge could misread it, so the opening 20 s must make clear it is not a chatbot. |
| R10 | Demo video | p8: "three minute demo video … one of the primary artifacts Judges use … along with your code and live product" | VERIFIED | Yes | What "live product" means (hosted URL?) | Ask (Q4) | Plan a hosted read-only demo or a reproducible local run. |
| R11 | Stage Two rubric | p8–9 table: Impact **30%**, Meta AI Tooling **25%**, Technical Depth & Execution **20%**, Demo **25%**, each 0–10 | VERIFIED (table) | Yes | **CONFLICT — see C1** | Ask (Q2) | Every ranking is computed under both weightings (file 05). |
| R12 | Stage Three | p9: top 5 per track; final judges "watch the video demos live and rank them using the same rubric" | VERIFIED | Yes | — | — | The video is the finals artifact too, so it gets premium production. |
| R13 | Tracks | S-EV: Indie "for individual builders and students. Judged on creativity, technical ambition, and whether it works." Startup "for teams and founders building a real product. Judged on technical execution and whether it holds up in production." "Every project enters one track." | VERIFIED | Yes | Whether a 2-person team without a company can enter Startup, and whether the track can change after the application | Ask (Q1) | Track recommendation stays **conditional** (file 05). |
| R14 | Submission | p7: "Teams and startups submit one project, not one submission per person." One Representative. | VERIFIED | Yes | — | — | Decide the representative early. |
| R15 | Meta credits | p5: "$150 in Meta Model API credits" per accepted participant, claimed individually by Nov 4 9 PM ET; "credits will be distributed in batches"; "a credit card must be applied to your account"; spend limit is a "notification" | VERIFIED | Yes | Whether credits are already posted to each account: **UNKNOWN** (participants report credits "visible") | User checks the billing page | **A card is required for any call**, and the notification is not a hard cap. A budget guard in code is mandatory (see Q6). |
| R16 | Partner credits | p6–7: Baseten $100 (up to 2,000, selected); Modal $100 (first 1,000); Fireworks $25 (shortlist). "Credits are not guaranteed" | VERIFIED | Not budgeted | — | — | Plan at **$0 partner credit**. |
| R17 | Open-weights bonus | p10–11: $10K "built using Muse Glimmer or Muse Spark Open, served on participants' own hardware or through partner-provided inference" | VERIFIED (column clipped) | Optional | Judging method clipped | — | Glimmer needs local GPU capacity (Q5). |
| R18 | Agentic bonus | p10–11: $5K "strongest use of AI agents to complete meaningful tasks, make decisions, or coordinate multi-step workflows" | VERIFIED | Optional | — | — | Parity's verifier loop plus the Wonder tester fit (INFERENCE). |
| R19 | Creative bonus | p10–11: $5K for Muse Image or Muse Wonder | VERIFIED | Optional | — | — | Wonder usage qualifies (INFERENCE). |
| R20 | Viral / community | p10: Viral $20K (engagement on X after the event); Community Vote $10K (gallery, Nov 16) | VERIFIED | Optional | — | — | Posting needs user approval. |
| R21 | Official Rules | S-EV: "Official Rules will be published before the Hackathon begins … and must be accepted" | **UNRESOLVED** — document not located | Yes | IP/licensing, eligibility details | Ask (Q3); check the CV dashboard | Recommendations stay conditional on it. |
| R22 | Idea pivot after application | Nothing found | **UNRESOLVED** | Yes | Absence of a prohibition ≠ permission | Ask in #questions | Low risk (INFERENCE): the rubric judges the submitted project. |
| R23 | Dates may change | S-EV: "Dates may be subject to change at Meta's sole discretion" | VERIFIED | Yes | — | Re-check the event page daily | Add it to the daily checklist. |
| R24 | Meta use policy | S-META-AUP (dev.meta.ai/use-policy/): "Military, warfare, nuclear industries or applications, espionage"; "Operation of critical infrastructure, transportation technologies, or heavy machinery" | OBSERVED, scope UNKNOWN | Probably | The page is labelled **Llama 2** and never names Muse or the Model API | Ask (Q3, with the Official Rules) | Treat as binding. Defence is out on R9 alone ("political or involving war"). |

## 3. Contradictions and how they are handled

- **C1 — Stage Two weighting.** Mandate v1 §1 reports participant-guide prose saying the criteria are "equally weighted". In the PDF print (S-PG) I found **no such sentence**: only the 30/25/20/25 table. The only "weighted equally" sentence found is on S-EV, and it describes **application review** ("Your project idea … Your technical skill … Both criteria are weighted equally"). The print is clipped, so text could be missing. **Status: UNRESOLVED.** File 05 ranks under both 30/25/20/25 and 25/25/25/25.
- **C2 — Prize totals.** Headings ($400K Indie, $550K Startup) match the listed places. No conflict.
- **C3 — Matterhorn counts.** The current version is **Matterhorn 1.1** (April 2021), which supersedes 1.02 (S-MATTERHORN-11). It keeps 136 failure conditions. The 87 machine-checkable / 47 human / 2 untestable split is confirmed for **1.02 only** (S-MATTERHORN); we could not extract the 1.1 split, so Codex checks it (09 §6). Other pages say 89/47 or 89/45/2. Cite "Matterhorn 1.1, 136 conditions"; quote the split as "per 1.02" and treat ±2 as noise.
- **C4 — DOJ deadline is contested in both directions.** DOJ plans substantive rulemaking and SBA Advocacy listed the rule for "rescission, withdrawal, or modification" (S-FR 20905, 20908), while NFB sued to undo the extension (S-NFB-SUIT, filed 2026-05-21, no ruling found). The obligation applies "regardless of the compliance dates" (S-FR 20908).

## 4. Blocked or partial sources (not bypassed)

| Source | Blocker | Workaround |
|---|---|---|
| cerebralvalley.ai `/details` | Needs sign-in; shell only | Used the user-supplied PDF print (S-PG). |
| federalregister.gov 2026-07663 | Redirected to the `unblock.federalregister.gov` bot check, which was **not** bypassed | Same document from GovInfo (S-FR). |
| cni.org CNI_Project_Tressler.pdf | HTTP 403 | Figures come from the search summary only, labeled THIRD-PARTY. |
| pdfremediator.apps.ucsd.edu | TLS certificate rejected | Not read. Only its existence is noted. |
| QyrosXS (AWS Marketplace) | URL not captured | Listed as CLAIMED with URL UNKNOWN. |
| Official Rules | Not found | Q3. |
| titleii.org/title-ii-updates | WebFetch ECONNRESET (round 2) | Search summaries only; "no NPRM found as of Oct 12" is THIRD-PARTY. |
| Matterhorn 1.1 PDF | Text not extractable by the fetch tool | 1.1 split UNCONFIRMED; Codex task. |
| github.com (ASSETS'25 repo licence) | Claude has no GitHub access (user rule) | Codex task (09 §6). |
| sebi.gov.in, who.int, webaim.org, Supreme Court judgment | Not fetched (time) | Secondary sources, labelled THIRD-PARTY. |

## 5. Open questions (user to ask in Discord #questions; I cannot send messages)

- Q1: Can an unincorporated 2-person team enter Startup? Can the track change after the application?
- Q2: Stage Two: weighted (30/25/20/25) or equal?
- Q3: Where are the Official Rules? Are declared OSS dependencies acceptable?
- Q4: Must the "live product" be a public URL that judges can open?
- Q5 (for the user): Is a GPU with ≥24 GB VRAM available? This decides whether Glimmer can be self-hosted.
- Q6 (for the user): Who adds the card to the Meta account? A budget guard in code is mandatory either way.

## 6. Source index

Meta platform: S-MODELS, S-PRICING, S-FILES, S-CU, S-VIDEO, S-SEG, S-WONDER, S-GLIMMER, S-SPARK-OPEN, S-SAM31, S-VB, S-BENCHLIST.
Regulation and standards: S-FR, S-TXST, S-PSU, S-W3C-125, S-MATTERHORN, S-MATTERHORN-11, S-PDFA-MATH, S-PDFDAYS, S-NFB-SUIT, S-META-AUP, S-BERI-LICENSE.
India and EU drivers: S-AMAR-JAIN, S-SEBI-A11Y, S-EAA-ENF.
PDF accessibility market: S-ALLYANT, S-ALLYANT-PR, S-ALLYANT-AI, S-CL-USERVERIFY, S-MATHPIX, S-ALLY, S-FRESNO-RFP, S-YUJA, S-NEOMED, S-PURDUE, S-EQUIDOX-AUTOTAG, S-AXESSTAG, S-NUTRIENT, S-QYROS, S-ASU, S-ASU-EQ, S-CNI, S-OSU-SUPPLIERS, S-VENNGAGE, S-CMU, S-UCSD.
Research: S-ASSETS25, S-ITAG, S-PAVE, S-ARXIV-MATHML, S-STEM-ALT, S-RODENT, S-FAILBENCH, S-DQA, S-INFOEQ-SEARCH.
Agentic accessibility testing (file 10, C3): S-TASKAUDIT, S-AXNAV, S-AGENTIC-AUDIT, S-AAA-AUDIT, S-SCREENAUDIT, S-USERSIDE-REPAIR, S-TESTSPRITE, S-BROWSERSTACK-A11Y, S-GUIDEPUP, S-WEBAIM-2026, S-DEQUE-57.
Video privacy (file 10, C4): S-GEOSPY, S-VLM-GEOPRIV, S-VLM-PAI, S-VLM-SHIELD, S-YT-BLUR, S-BGBLUR, S-IG-INDIA, S-WHO-DISAB.
Other domains: S-3PLAY, S-VERBIT, S-AIMEDIA, S-RECAP, S-REDACT-COST, S-ISED, S-PIMLOC, S-AXON, S-FACIT, S-FISH, S-REL, S-SOP, S-GAUGE, S-CMMS, S-LOOKR, S-IMAGO.
Agents and market: S-OPENAI-ATLAS, S-ROSELLI, S-INFOWORLD, S-GARTNER, S-GAO, S-SILKTIDE-ALT.
Engineering governance: S-CODEX, S-CODEX-CONFIG, S-CC-MEM, S-CC-MEMORY, S-CC-HOOKS, S-CC-BP, S-CC-PERMS, S-CC-SANDBOX, S-ANTH-HARNESS, S-WEASY, S-HACK-TIPS.
