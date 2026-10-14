# EXP-01: Source-grounded notebook and auto-overview

- **Date/time:** 12 Oct 2026, afternoon (AEDT)
- **Tool:** NotebookLM (now served at notebook.google.com as "Gemini Notebook"), free personal Google account
- **Notebook:** "ASIC Regulatory Guide 280: Sustainability Reporting" (auto-titled)
- **Sources in notebook:** AASB S2 (2024) PDF; ASIC RG 280 (2025) PDF; KPMG guide URL **failed to load**
- **Feature tested:** Source-grounded notebook and auto-overview
- **Scenario / user role:** student preparing a governance workshop briefing on Australian mandatory climate reporting
- **Exact prompt or action:** Created a new notebook. Added three sources by URL: AASB S2 PDF, ASIC RG 280 PDF, KPMG ASRS guide. Read the generated overview.

## Output (verbatim or screenshot)

Two sources loaded. KPMG source shown in red with an info icon (URL could not be fetched). Auto-overview summarises RG 280 (purpose, Corporations Act Chapter 2M, directors' duties, phased rollout, modified liability). Notebook auto-titled after RG 280 only.

Screenshot: `../screenshots/fig14_exp01_sources_overview.png`

## Verification against sources
| Claim in output | Source & location | Correct? (Y / Partly / N) |
|---|---|---|
| RG 280 issued by ASIC, applies under Chapter 2M Corporations Act | RG 280 | Y |
| Phased rollout and modified liability settings | RG 280 | Y |
| Overview reflects all loaded sources | AASB S2 not mentioned | N |

## Ratings (1–5)
- Accuracy & relevance: 3
- Usefulness in academic workflow: 4

## Limitations / concerns observed
- Overview and title reflect only one of two sources (relevance bias toward RG 280).
- KPMG failure is signalled only by a small red marker; easy to miss.
- Later Briefing Doc header claims "3 sources" although only 2 loaded.
