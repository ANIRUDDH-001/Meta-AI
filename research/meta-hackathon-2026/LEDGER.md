# Research ledger — Meta Global AI Developer Hackathon 2026

Purpose: single running record of what has been checked, found, decided and still open, so no search is repeated.
Raw quotes/numbers live in `resources/source_captures.md`. Final deliverables are files `00`–`08` + `sources.jsonl`.

## User instructions in force (2026-10-26)
- Execute `CLAUDE_CODE_INVESTIGATION_MANDATE.md` (v1) structure, but **profile-free**: do NOT inspect participants' GitHub, past projects, skills, interests (user override; V2 mandate agrees). `01_TEAM_CAPABILITY_EVIDENCE.md` therefore records capacity only.
- Read-only research; write only under `research/meta-hackathon-2026/`. No implementation, no paid calls, no forms, no messages.
- Nothing enters repo/rules/methodology without explicit approval via MCQs with reasoning + recommendation. CLAUDE.md / AGENTS.md are drafted as **proposals** under `research/meta-hackathon-2026/proposals/` and only installed after approval.
- Aim: world-class shippable product + premium 3-minute story demo; ambitious but fact-grounded; counter with reasons when warranted.

## Verified facts (see captures for quotes)
| # | Fact | Label | Source |
|---|---|---|---|
| F1 | Submission due Wed 2026-11-04 9:00 PM ET = 2026-11-05 07:30 IST (DST ends Sun 2026-11-01, so ET=EST) | PRIMARY + computed | S-PG p3,p7; S-EV |
| F2 | Stage Two rubric in guide PDF: Impact 30 / Meta Tooling 25 / Tech Depth 20 / Demo 25, scored 0–10 | PRIMARY | S-PG p8–9 |
| F3 | "Both criteria are weighted equally" on public event page refers to **application review** (idea + technical skill), not Stage Two. No "equally weighted" judging sentence found in the guide PDF | OBSERVED | S-EV, S-PG |
| F4 | Tracks: Indie "for individual builders and students… creativity, technical ambition, and whether it works"; Startup "for teams and founders building a real product… technical execution and whether it holds up in production". "Every project enters one track." | PRIMARY | S-EV |
| F5 | Max 4 per team; solo allowed; public repo; new work only; startups may build on existing codebases if new work identified | PRIMARY | S-PG p4 |
| F6 | Anti-projects: medical advice, basic RAG, simple image analyzers, simple AI-for-education chatbots, AI job screener, nutrition coach, personality analyzers, sports analyzers/coaches, political/war | PRIMARY | S-PG p4 |
| F7 | $150 Meta API credit per accepted participant, claimed individually by Nov 4 9 PM ET; **credit card must be on account to make calls**; spend limit is only a notification | PRIMARY | S-PG p5 |
| F8 | Partner credits (Baseten $100 up to 2,000 ppl; Modal $100 first 1,000; Fireworks $25 select teams) are discretionary, not granted | PRIMARY | S-PG p6–7 |
| F9 | Prizes: Indie 150/100/75/50/25K; Startup 250/150/75/50/25K; bonus $50K (Viral 20K, Open-weights 10K, Community 10K, Agentic 5K, Creative 5K) | PRIMARY | S-PG p9–11 |
| F10 | Models & prices: Spark std $1.25 in / $4.25 out per 1M; contributor $0.10/$0.20; Wonder $4/$20; SAM 3.1 $0.20 per 1k video frames, $2.50 per 1k images; Voice Transcribe $0.18/h; Image $0.01/img; search grounding $2.50/1k | PRIMARY | S-PRICING |
| F11 | Spark/Wonder: 1,048,576-token context; text+image+video+audio+PDF in; tool calling, structured output, search grounding; Wonder adds computer use (client-side harness, Responses API only) | PRIMARY | S-MODELS, computer-use doc |
| F12 | PDF input: text from first 100 pages, page images from first 50 only; inline 50 MB, Files API 1 GiB | PRIMARY | file-handling doc |
| F13 | Muse Spark Open = 816B MoE / 42B active, open weights (HF 2026-10-15 per aggregator), not on Model API; Muse Glimmer = distilled, self-host only | PRIMARY / 3rd-party date | S-MODELS, benchmarklist |
| F14 | SAM 3.1 released 2026-03-27 (object multiplexing for multi-object video tracking); on Meta API returns boxes+masks+tracks | 3rd-party report | gigazine, HF card |
| F15 | Official Rules document: not located publicly (event page says it would be published before Oct 26) | UNKNOWN | search |
| F16 | DOJ IFR 91 FR 20902 (2026-04-20, Docket CRT150, RIN 1190-AA82): Title II compliance ≥50K pop. → 2027-04-26; <50K + special districts → 2028-04-26 | OBSERVED (GovInfo PDF in resources/) | S-FR |
| F17 | 91 FR 20907: "Advanced technology, such as generative AI, does not yet reliably automate the remediation of inaccessible content at scale" | OBSERVED | S-FR |
| F18 | 91 FR 20905: a Congressman told DOJ generative AI "cannot reliably automate the remediation of STEM materials at scale, and human oversight is required" | OBSERVED (quoted correspondence) | S-FR |
| F19 | Matterhorn 1.02: 136 failure conditions / 31 checkpoints; 87 software-checkable, 47 need human judgment, 2 untestable | PRIMARY | S-MATTERHORN |
| F20 | Course materials have no Title II exception; preexisting docs exempt unless currently used to access services | THIRD-PARTY (university summaries) | S-TXST, S-PSU |
| F21 | Incumbents already claim STEM: Allyant CommonLook Edu (alt text for math/chem/diagrams, STEM tagging, validation report); YuJa Panorama v25.7 (math images → MathML in HTML alt format) | CLAIMED (vendor) | S-ALLYANT, S-YUJA |
| F22 | ASSETS'25 benchmark (arXiv 2509.18965): 125 PDFs, 7 criteria, P/F/NP/CT; GPT-4-Turbo 0.85 best; repo github.com/Anukriti12/PDF-Accessibility-Benchmark (license unstated) | PRIMARY | S-ASSETS25 |
| F23 | ASU×OSU open pipeline ≈$0.0013/page + Adobe fees, 3.5 min/17 pages; QA checkpoints still in development | PRIMARY (project page) | S-ASU |
| F24 | WCAG 2.1 SC 1.2.5 (AA) requires audio description for prerecorded synchronized video | PRIMARY | S-W3C-125 |
| F25 | Codex AGENTS.md: root→cwd concatenation, 1 file/dir, `AGENTS.override.md`, 32 KiB default cap | PRIMARY | S-CODEX |
| F26 | Claude Code best practices: concise CLAUDE.md ("Would removing this cause Claude to make mistakes?"), verification checks, explore→plan→code, hooks for must-happen rules, subagent adversarial review | PRIMARY | S-CC-BP |
| F27 | Gartner (2025-06-25): >40% agentic AI projects canceled by end-2027 (cost, unclear value, weak risk controls) | PRIMARY press release | S-GARTNER |
| F28 | OpenAI FAQ: ChatGPT Atlas uses ARIA roles/names/states; accessible structure = agent-readable structure | PRIMARY-SOURCE CLAIM | S-OPENAI-ATLAS |
| F29 | Pimloc Secure Redact already does audio NER redaction + faces/plates/on-screen text (fixed categories; open-vocab not found) | CLAIMED | S-PIMLOC |
| F30 | WeasyPrint PDF/UA-1 output "experimental", not guaranteed valid; `pdfua` pikepdf checker covers 16 of 106 machine rules; veraPDF needed for conformance claims | PRIMARY docs / 3rd-party | S-WEASY |
| F31 | Mathpix already converts math PDFs → DOCX/HTML with MathML; universities still tell staff to read back every expression + screen-reader test (no independent accuracy test found) | THIRD-PARTY | S-MATHPIX |
| F32 | Anthology Ally: MathML only from Word Office Math; tagged-PDF alt format only for Word/PPT; math inside PDFs undocumented | PRIMARY-SOURCE CLAIM | S-ALLY |
| F33 | Axon Redaction Assistant: faces/plates/screens + human confirm + exemption log, bundled in US OSP 7+; audio unconfirmed | CLAIMED | S-AXON |
| F34 | Two searches found no QA-based "information equivalence" accessibility metric (absence not proven) | UNKNOWN | S-INFOEQ-SEARCH |
| F35 | Not verified this session (named in queries, no evidence returned): PREP, Continual Engine, Audible Sight, ViddyScribe, Encord/Scale/Voxel51 robotics, CaseGuard, Veritone product details (only a vendor-blog figure: 5–10 h manual per video hour) | UNKNOWN | search logs |
| F36 | Screened out at desk stage with **no evidence searches**: construction progress, insurance claims video, dev bug-repro, prior-auth | INFERENCE only | — |
| F37 | Allyant CommonLook Edu brochure (SHA-256 f0f267d1…494b3d068): "PDF Document Validation Reports… including ADA Title II"; "System of Record"; math/chem/diagram **alt text** generation; 7-day trial. Whether the report gives evidence for the human-judgment checks: UNKNOWN (trial needs a user-created account) | CLAIMED (vendor) | S-ALLYANT-AI |

## Opportunity research status
| Hypothesis | Demand evidence found | Competitors found | Status |
|---|---|---|---|
| Audio description (video accessibility) | 3Play list $9/$14 per min synthesized, $18/$35 voice artist; Harvard $7/$11; DOJ Title II: WCAG 2.1 AA, deadlines extended to 2027-04-26 / 2028-04-26 | 3Play, Verbit AI AD (Title II), Ai-Media LEXI AD, Recap | researched |
| PDF/STEM document remediation | Manual $3–$25/page (clusters $5–8); OSU hundreds of thousands of PDFs; DOJ IFR says gen-AI "does not yet reliably automate" remediation at scale; CNI report: AI pass rate 52.5%→93.7%, math & figures still a major challenge | Adobe Auto-Tag API, Allyant CommonLook AI, Equidox, QyrosXS (Claude), ASU/OSU open project, Nutrient | researching |
| Records-request video redaction | 1–1.5 staff h per video hour (WI), 4–6 h (Canada est.), $0.73–0.98/min fees, $80K/yr redaction position | Axon, Veritone, Pimloc Secure Redact, Facit, CaseGuard | researched |
| Fisheries EM video review | review $300–350/day; EU REM for high-risk >18 m vessels, small-scale from 2028-01-10 | Ai.Fish CatchVision, FishVue, CVision AI | researched (data access weak) |
| Animal behavior scoring (science) | manual 3–4× video duration; Rodent-Bench (2026) shows MLLMs modest | DeepLabCut, SLEAP, SimBA, Noldus, AmadeusGPT | researched |
| Robot demo data QA | papers: curation manual/heuristic bottleneck | robot-episode-labeler (F1 0.629), DQA framework, FailBench (2026-09) | researched (prior art heavy) |
| Video→SOP / work instructions | vendor claims only | Siemens Opcenter, Docsie, Guidde, Synthesia | crowded |
| Analog gauge digitization | retrofit $500–5K/instrument (vendor) | Roboflow, iFactory, Surplus | feature-level |
| Facility asset register from video | CMMS onboarding $5K–80K (vendor blogs) | unknown | thin evidence |

## Finalists (analysis complete 2026-10-26; user decision PENDING)
| Rank | Finalist | Est. score 30/25/20/25 | Est. equal | Why not higher / lower |
|---|---|---|---|---|
| 1 (recommended, close call) | **Parity** — proof-carrying accessibility remediation for STEM PDFs (Spark + Wonder AT-tester + SAM chart check + Glimmer verifier) | 7.83 | 7.83 | Strongest why-now (F16–F18); crowded (F21); Allyant report exists (F37) → moat must be judgment-check evidence + MathML + AT-operated test, not "a report" |
| 2 (runner-up) | Policy-driven video redaction (SAM 3.1 + Voice Transcribe + Spark) | 7.98 | 8.00 | Slightly higher rubric estimate (within noise); weaker why-now, Axon bundling, sensitive footage |
| 3 | Audio description studio for instructional video | 7.65 | 7.63 | AI AD already shipped by Verbit/3Play/Ai-Media; no Meta TTS |
| 4 | Robot demonstration data QA | 7.15 | 7.25 | Small buyer set, prior art (FailBench, DQA) |
Scores are INFERENCE (±1.0 per criterion). Eliminated: fisheries EM (data access), rodent scoring (Rodent-Bench weak), video→SOP, gauges, asset register, construction, insurance, dev bug-repro, prior-auth.

## Decisions so far
- D1: Proceed profile-free (user override of v1 §3).
- D2: Output folder `research/meta-hackathon-2026/` (v1 path; user said keep everything inside D:\Projects\Meta AI).
- D3 (PENDING user MCQ): product, track, approval granularity, governance install, plugins/skills.

## Open questions for organizers (cannot send messages; user to ask in Discord #questions)
- Q1 Can a 2-person team without an incorporated company enter the Startup track? Can track be changed after application?
- Q2 Is the Stage Two rubric weighted (30/25/20/25) or equal? (Only weighted version found.)
- Q3 Where are the Official Rules (licensing/IP, eligibility of pre-existing OSS dependencies)?
- Q4 Does "live product" require a publicly hosted deployment judges can access?
- Q5 (for user) GPU with ≥24 GB VRAM available? Decides whether Muse Glimmer can be self-hosted (open-weights bonus).
- Q6 (for user) Who adds the credit card to the Meta API account? It is required for any call (F7); spend limit is only a notification → code-level budget guard mandatory.

## Governance drafts (2026-10-26, UNAPPROVED)
- Written to `proposals/` (README has the install map): AGENTS.md (89 lines, single rule source), CLAUDE.md (`@AGENTS.md` + Claude-only), PROTOCOLS.md (MCQ format, task spec, ledger schemas, writer/reviewer, DoD, cadence, demo, incidents, token economy), ledger templates, `.claude/settings.json` (deny/ask permission rules + SessionStart hook), `.codex/config.toml` (on-request / workspace-write), TOOLING_PROPOSAL.md.
- Grounding: S-CC-MEMORY, S-CC-HOOKS, S-CODEX, S-CODEX-CONFIG, S-ANTH-HARNESS, S-CC-BP.
- Next: user MCQs (product, track, approval granularity, governance install), then record answers here and in memory.
