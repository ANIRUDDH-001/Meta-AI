# Research ledger — Meta Global AI Developer Hackathon 2026

Purpose: single running record of what has been checked, found, decided and still open, so no search is repeated.
Raw quotes/numbers live in `resources/source_captures.md`. Final deliverables are files `00`–`10` + `sources.jsonl`.

## User instructions in force (2026-10-26)
- Execute `CLAUDE_CODE_INVESTIGATION_MANDATE.md` (v1) structure, but **profile-free**: do NOT inspect participants' GitHub, past projects, skills, interests (user override; V2 mandate agrees). `01_TEAM_CAPABILITY_EVIDENCE.md` therefore records capacity only.
- Read-only research; write only under `research/meta-hackathon-2026/`. No implementation, no paid calls, no forms, no messages.
- Nothing enters repo/rules/methodology without explicit approval via MCQs with reasoning + recommendation. CLAUDE.md / AGENTS.md are drafted as **proposals** under `research/meta-hackathon-2026/proposals/` and only installed after approval.
- Aim: world-class shippable product + premium 3-minute story demo; ambitious but fact-grounded; counter with reasons when warranted.
- (Message 3) Claude **never commits and never accesses GitHub** (web, API, `gh`, MCP): "commits will be exclusively handled by me or codex"; "claude has no permission to access github". Claude leaves uncommitted changes plus a handoff.
- (Message 3) Approvals are judged by usefulness, not count. Plans must be detailed enough that a new chat or a switch to Codex causes no discrepancy; everything is logged so no agent needs to re-read the codebase.
- (Message 3) Install needed skills from official sources and use them proactively. Reason, research and back every claim. Pivot now if confidence is elsewhere; red-team with an independent subagent; then give Codex a counter-prompt. Iterate on user approval.
- (Message 4) Look at Indian defence or development needs, "just a reference / no boundation".
- Process rules adopted after audit A19: timestamps only from `date -u` or file/transcript timestamps; counts only from a command.
- (Message 5, 2026-10-26T17:28:27Z) The user pasted ChatGPT's review of the Codex prompt and said: "now reason and finalise the prompt / also codex can commit / claude can read only / you may install / and should i run the prompt as soon as you revert or after the red team revert ?" Recorded as D14–D16. The prompt is rewritten in two phases (`CODEX_COUNTER_PROMPT.md`).

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
| F38 | Matterhorn **1.1** (April 2021) supersedes 1.02; 136 conditions. The 87/47/2 split is confirmed for 1.02 only; 1.1 split not extracted (Codex task) | PRIMARY-SOURCE CLAIM | S-MATTERHORN-11 |
| F39 | CommonLook "User Verifications" are manual checks; "Verification result set by user" | CLAIMED (vendor docs) | S-CL-USERVERIFY |
| F40 | dev.meta.ai/use-policy/ bans "Military, warfare, nuclear industries or applications, espionage" and "Operation of critical infrastructure, transportation technologies, or heavy machinery". **Page is labelled Llama 2, undated, never names Muse/Model API** → scope UNKNOWN, treated as binding | OBSERVED | S-META-AUP |
| F41 | IFR: SBA Advocacy listed the rule for "rescission, withdrawal, or modification" (20905); DOJ "plans to engage in future rulemaking processes related to the substantive requirements" and "will consider issuing an NPRM" (20908); duties apply "regardless of the compliance dates" (20908). No NPRM found (titleii.org, third-party, as of Oct 12) | OBSERVED + THIRD-PARTY | S-FR |
| F42 | NFB sued DOJ and HHS on 2026-05-21 (D. Md.) over the extensions; no ruling found. HHS §504 deadline 2027-05-11 | THIRD-PARTY | S-NFB-SUIT |
| F43 | ASSETS'25 protocol: 35 base PDFs (5 per criterion) → 125 variants; 7 criteria mapped to WCAG 2.2 SC + PDF/UA; temp 0.7, 3 runs, page-level, most conservative label; inputs withheld to make Cannot Tell; Not Present accuracy 0.55 (best) to 0 (Llama); no licence in paper | PRIMARY-SOURCE CLAIM | S-ASSETS25 |
| F44 | MathML inside PDF needs PDF 2.0 (PDF/UA-2); under PDF/UA-1, math = `Formula` + alt text. So MathML holds only in an HTML twin if AT1 gates on PDF/UA-1 | PRIMARY-SOURCE CLAIM | S-PDFA-MATH |
| F45 | Voice Transcribe gives turn-level timestamps, **no word-level**; Spark audio input is "currently not fully supported" (verbatim; corrected from a paraphrase, 12 RT32); no Meta TTS | PRIMARY-SOURCE CLAIM | S-MODELS |
| F46 | TaskAudit (CHI 2026): vision-free agents via a TalkBack proxy on Android; 48 errors on 54 screens vs 4–20 for existing checkers; 96% task success when no errors | PRIMARY-SOURCE CLAIM | S-TASKAUDIT |
| F47 | Prior art also: AXNav (iOS VoiceOver replay, CHI 2024), ScreenAudit (mobile), AAA (WCAG-EM copilots, AAAI 2026) | PRIMARY-SOURCE CLAIM | S-AXNAV, S-SCREENAUDIT, S-AAA-AUDIT |
| F48 | Agentic web auditing (arXiv 2609.09379): 40 WCAG requirements, recall 86% vs axe-core 36%, precision 56%; 9/10 keyboard traps | PRIMARY-SOURCE CLAIM | S-AGENTIC-AUDIT |
| F49 | User-side LLM repair: unverified edits 24 improvements vs 20 regressions; verified loop caught 57/57 | PRIMARY-SOURCE CLAIM | S-USERSIDE-REPAIR |
| F50 | Commercial AI accessibility testing claims: TestSprite (screen-reader checks), BrowserStack Issue Detection Agent, axe DevTools AI. Whether a real screen reader drives an agent: not checked | CLAIMED | S-TESTSPRITE, S-BROWSERSTACK-A11Y |
| F51 | Guidepup: MIT; drives NVDA (Windows) and VoiceOver (macOS); `spokenPhraseLog()`; no Linux | PRIMARY-SOURCE CLAIM | S-GUIDEPUP |
| F52 | WebAIM Million 2026: 95.9% of home pages fail, 56.1 errors/page (summaries); Deque: axe finds 57% of issues by volume (vendor, 2021) | THIRD-PARTY / CLAIMED | S-WEBAIM-2026, S-DEQUE-57 |
| F53 | EAA court cases: Lille 2026-05-05 Auchan won on procedure (appeal to Douai); Caen June 2026 ordered Carrefour France accessible within 6 months with daily penalty | THIRD-PARTY | S-EAA-ENF |
| F54 | India: SEBI circular 2025-07-31 (IS 17802 / WCAG 2.1 / GIGW 3.0); audit + remediation due **2026-10-31**. *Amar Jain v. UoI* (SC, 2025-04-30): digital access part of Art. 21, 20 KYC directions; blind petitioner | THIRD-PARTY (SEBI site and judgment not read) | S-SEBI-A11Y, S-AMAR-JAIN |
| F55 | Geo-privacy threat: GeoSpy stalking concerns, public access closed (404 Media, Jan 2025); frontier VLMs infer street-level location (VLM-GEOPRIVACY); private attributes inferred up to 77.6% (arXiv 2404.10618); an image-shielding defence paper exists (title only) | THIRD-PARTY / PRIMARY-SOURCE CLAIM | S-GEOSPY, S-VLM-GEOPRIV, S-VLM-PAI, S-VLM-SHIELD |
| F56 | Consumer blur prior art: YouTube Studio auto face blur + custom blur with tracking; BGBlur/YouBlur fixed-class face/plate blur. No open-vocabulary "clue" detector found (absence not proven) | PRIMARY-SOURCE CLAIM / CLAIMED | S-YT-BLUR, S-BGBLUR |
| F57 | Audience: India is Instagram's largest market, ~480M (Statista) to ~555M (NapoleonCat ad reach); 1.3B people (16%) have a significant disability (WHO, via mirror) | THIRD-PARTY | S-IG-INDIA, S-WHO-DISAB |
| F58 | Demand proxy: County of Fresno E-RFP #26-077, document remediation **software**, open 2026-07-27 to 08-25 | THIRD-PARTY (listing) | S-FRESNO-RFP |

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

## Pivot candidates (file 10; INFERENCE ±1; user decision PENDING)
| Candidate | Weighted | Equal | Note |
|---|---|---|---|
| C4 "Before you post" video privacy guard | 8.50 | 8.50 | Highest Meta fit (SAM 3.1 + Spark video + Transcribe); threat-based why-now |
| C3 Blindfolded agent (web accessibility) | 8.35 | 8.38 | Legal drivers (DOJ, EAA, SEBI, Amar Jain); crowded research prior art (F46–F50) |
| C5 Redaction B2G | 7.98 | 8.00 | Superseded by C4 |
| C1 Parity-PDF rescoped | 7.48 | 7.50 | Audit shrank its claims (09) |
C4 vs C3 is inside noise → Day-1 spike with pre-registered pass criteria (10 §5).

## Finalists before the audit (superseded by the pivot candidates above; kept as history)
| Rank | Finalist | Est. score 30/25/20/25 | Est. equal | Why not higher / lower |
|---|---|---|---|---|
| 1 (recommended, close call) | **Parity** — proof-carrying accessibility remediation for STEM PDFs (Spark + Wonder AT-tester + SAM chart check + Glimmer verifier) | 7.83 | 7.83 | Strongest why-now (F16–F18); crowded (F21); Allyant report exists (F37) → moat must be judgment-check evidence + MathML + AT-operated test, not "a report" |
| 2 (runner-up) | Policy-driven video redaction (SAM 3.1 + Voice Transcribe + Spark) | 7.98 | 8.00 | Slightly higher rubric estimate (within noise); weaker why-now, Axon bundling, sensitive footage |
| 3 | Audio description studio for instructional video | 7.65 | 7.63 | AI AD already shipped by Verbit/3Play/Ai-Media; no Meta TTS |
| 4 | Robot demonstration data QA | 7.15 | 7.25 | Small buyer set, prior art (FailBench, DQA) |
Scores are INFERENCE (±1.0 per criterion). Eliminated: fisheries EM (data access), rodent scoring (Rodent-Bench weak), video→SOP, gauges, asset register, construction, insurance, dev bug-repro, prior-auth.

## Decisions so far
IDs D1–D10 are the same decisions as in file 07 §1. New IDs continue from D11 (renumbered 17:14 UTC: the earlier LEDGER D5–D7 clashed with 07's D5–D7).
- D1: Proceed profile-free (user override of v1 §3).
- D2: Output folder `research/meta-hackathon-2026/` (v1 path; user said keep everything inside D:\Projects\Meta AI).
- D3 (PENDING user MCQ): product. 07's D3 (Parity) is reopened by the pivot candidates; see D13.
- D4 (USER, 2026-10-26): **Indie track** — "yes we are allowed for indie. we are not a startup".
- D5, D6 (07: approval granularity, governance install): still PROPOSED, pending MCQ.
- D11 (USER): Claude never commits or touches GitHub; the user or Codex commits. Narrowed by D15 (local read-only git) and D20 (public GitHub page reads).
- D12 (CLAUDE, evidence-based): Indian defence **rejected** (S-PG "anything political or involving war"); Indian development needs folded into pivot candidate C3 (file 10 §2).
- D13 (PENDING user MCQ): pivot from Parity-PDF to C3 (blindfolded web agent) or C4 (video privacy guard). Supersedes 07's D7 (Parity pivot gate), which stays as history.
  - **Revised after the red team (file 12):** the C4 lean and "desk favourite" are withdrawn. Day-1 feasibility probes V1–V4 and W1–W3 replace the spikes, under a symmetric rule with an INSUFFICIENT EVIDENCE outcome (file 10 §5, `proposals/docs/ledger/PLAN.md`).
- D14 (USER, 2026-10-26T17:28:27Z): "codex can commit". Codex runs `git commit` when the user tells it to in that session. Push, merge, tag, release and deploy stay with the user (Q11, answered by D19).
- D15 (USER, same message): "claude can read only". Claude may run local read-only git (`status`, `diff`, `log`, `show`). Public GitHub reads: Q12, answered by D20.
- D16 (USER, same message: "you may install"): the **Security Guidance** plugin v2.0.16 from `claude-plugins-official` is installed at local scope for `D:\Projects\Meta AI` (`.claude/settings.local.json` mtime 2026-10-26T17:37:43Z). Active from the next session. Off switch: `SECURITY_GUIDANCE_DISABLE=1`; `ENABLE_STOP_REVIEW=0` turns off only the Stop review.
- D17 (USER, MCQ answered before 18:49:02Z, the next `date -u`): product path **"Wait for Codex first"**. Everything holds until Codex's file 13 is in: no probes, no metered calls. The forced-decision stop (end of 2026-10-28 IST) is unchanged.
  - Conflict, asked back to the user: the D18 option text said "$0 parts (W1, filming) can start meanwhile", while D17 holds everything. Until the user answers, Claude holds everything.
- D18 (USER, same MCQ): probe thresholds **"Freeze after Codex"**. Freeze once Codex's Phase 2 fixes are applied; log the SHA-256 of the gates table then (PROTOCOLS §6). Later edits need a new MCQ.
- D19 (USER, same MCQ; answers Q11): **"Codex commits when told"**. AGENTS line 9 now says: commits by the user, or by Codex when the user tells it to in that session; push, merge, tag, release and deploy by the user only; Claude never runs any of them. The earlier line 9, verbatim: "Any `git commit`, `push`, `merge`, `tag`, release or deploy will be done by user only and claude is not allowed to ever access it."
- D20 (USER, same MCQ; answers Q12): **"Yes, public reads only"**. Claude may read public pages on github.com and githubusercontent.com through WebFetch, without signing in. Still denied: any GitHub write, `gh`, `api.github.com`, `uploads.github.com`, `*.github.io`, the GitHub MCP, and shell fetches (curl, wget, Invoke-WebRequest). Narrows D11.

## Audit and corrections log
| When (UTC) | What | Where |
|---|---|---|
| 16:09:24 | ChatGPT audit snapshot `01ee5bb` (23 findings) | external file |
| 16:52:42 (transcript; was "~16:51") | Response written: 16 ACCEPT, 4 PARTIAL, 1 DISCLOSED, 1 UNVERIFIABLE, 2 severity disputes | 09 |
| 16:58 | Pivot brainstorm written | 10 |
| 17:05 | S-META-AUP is the Llama 2-labelled page; defence rejection now rests on S-PG | 09 §5, 10, 00 R24 |
| 17:05 | Capture-time estimates (~16:40, ~16:55) replaced by file mtimes; 00 retrieval window corrected; Matterhorn 1.1 cited | 00, captures |
| 17:22:39–17:35:14 | Red team (fresh subagent): 40 findings RT01–RT40; verdict "leaving Parity is defensible; lean C4 does not survive" | 11 |
| 17:28:27 | User message 5: ChatGPT's review of the Codex prompt (6 improvements), plus D14–D16 | this ledger |
| 17:43:38 | Response: 34 ACCEPT, 6 PARTIAL, 0 DISPUTE; C4 lean withdrawn; re-score C3 8.23, C4 8.10 | 12 |
| 17:47:51–18:36:29 | **Claude's own error corrected (RT07):** Day 1 is 2026-10-27, not 10-28; build time 144 h, not 128 h. Applied in 07, 09, 10, PLAN. Fixes from 12 applied to 00, 01, 04, 08, LEDGER and the governance drafts | 07, 09, 10, proposals |
| 18:39:35 (transcript) | **Claude's slip corrected:** file 10 cited three IDs missing from sources.jsonl. The earlier ID scan covered only `proposals/`. S-SEGMENT → S-SEG; S-LOOKR and S-IMAGO registered; 110 records | 10, sources.jsonl, 00, 08 |
| 18:41:33 (file mtime) | Codex prompt rewritten: two phases, blind Phase 1 committed first, SHA pinned, licence/probe/rule scrutiny, UNDETERMINED allowed | CODEX_COUNTER_PROMPT.md |
| 18:49:02 onward | User MCQ answers D17–D20 recorded. AGENTS line 9 reworded (D19). The settings draft's WebFetch GitHub denies narrowed to the API, uploads and github.io (D20) | LEDGER, proposals |
| 18:43:41 | `meta details 2.pdf` read as 0 bytes, tracked as the empty blob `e69de29` | repo root |
| 18:53:46 | **That finding is outdated.** By 18:51 the file was 3,536,269 bytes and staged by the user (mtime 2026-10-26T16:26:58Z, earlier than the 0-byte reading; how it changed is unknown). MEASURED with `pypdf` image hashes: 11 pages, no fonts; pages 2–3 and 7–11 identical to `meta details.pdf`; the images new on pages 4–6 are layout fragments (an "Event Details" heading, two icons, 7-px strips); page 1 only lost images. No new rule text found | repo root, CODEX_COUNTER_PROMPT.md |

## Open questions for organizers (cannot send messages; user to ask in Discord #questions)
- Q1 ANSWERED by the user: Indie (D4). Track question closed.
- Q2 Is the Stage Two rubric weighted (30/25/20/25) or equal? (Only weighted version found.)
- Q3 Where are the Official Rules (licensing/IP, eligibility of pre-existing OSS dependencies)?
- Q4 Does "live product" require a publicly hosted deployment judges can access?
- Q5 (for user) GPU with ≥24 GB VRAM available? Decides whether Muse Glimmer can be self-hosted (open-weights bonus).
- Q6 (for user) Who adds the credit card to the Meta API account? It is required for any call (F7); spend limit is only a notification → code-level budget guard mandatory.
- Q7–Q12 live in `proposals/docs/ledger/QUESTIONS.md`. Answered: Q8 (D14), Q9 (D15), Q11 (D19), Q12 (D20). Open there: Q7, Q10.

## Governance drafts (2026-10-26, UNAPPROVED)
- Written to `proposals/` (README has the install map): AGENTS.md (89 lines, single rule source), CLAUDE.md (`@AGENTS.md` + Claude-only), PROTOCOLS.md (MCQ format, task spec, ledger schemas, writer/reviewer, DoD, cadence, demo, incidents, token economy), ledger templates, `.claude/settings.json` (deny/ask permission rules + SessionStart hook), `.codex/config.toml` (on-request / workspace-write), TOOLING_PROPOSAL.md.
- Grounding: S-CC-MEMORY, S-CC-HOOKS, S-CODEX, S-CODEX-CONFIG, S-ANTH-HARNESS, S-CC-BP.
- Next: user MCQs (product, track, approval granularity, governance install), then record answers here and in memory.
- **Revised 17:20 UTC after the audit** (UNAPPROVED):
  - AGENTS.md is 98 lines / 6,292 bytes; user's line 9 kept verbatim, with sub-bullets for Codex commits (Q8) and Claude's no-GitHub rule.
  - PROTOCOLS.md has §1–§12: usefulness-not-count MCQs; PLAN.md and CODEMAP.md rows; red-team loop; daily re-check of reversing facts; §10 evidence classes and L0–L4; §11 budget broker at $100; §12 handoff block.
  - settings.json has 49 deny and 24 ask rules: Claude git writes, `gh`, GitHub WebFetch domains and GitHub MCP denied (S-CC-PERMS); known gap: full-path and `sh -c` calls.
  - New templates: `docs/ledger/PLAN.md` (pre-registered S-W, S-V, D13 gates), `docs/CODEMAP.md`. QUESTIONS gains Q8–Q10. FEATURES AT5/AT6 reworded.
  - Fixed: LEDGER/07 decision-ID clash (now D11–D13); Day-1 date conflict (10 said 10-27, 07 said 10-28; now 10-28) and the spike time share (9.4–12.5%, computed). **That fix was wrong (12 RT07):** the guide says "Building period: Oct 27 – Nov 4" (p4), so Day 1 is 10-27 and build time is 144 h. Corrected in 07, 09, 10 and PLAN.
