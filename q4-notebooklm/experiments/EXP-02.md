# EXP-02: Chat Q&A with inline citations

- **Date/time:** 12 Oct 2026, afternoon (AEDT)
- **Tool:** NotebookLM (now served at notebook.google.com as "Gemini Notebook"), free personal Google account
- **Notebook:** "ASIC Regulatory Guide 280: Sustainability Reporting" (auto-titled)
- **Sources in notebook:** AASB S2 (2024) PDF; ASIC RG 280 (2025) PDF; KPMG guide URL **failed to load**
- **Feature tested:** Chat Q&A with inline citations
- **Scenario / user role:** student preparing a governance workshop briefing on Australian mandatory climate reporting
- **Exact prompt or action:** "I am preparing a 1-page briefing for a governance workshop. Which entities are in Group 1 for mandatory climate reporting in Australia, when does their first reporting period start, and what relief applies to Scope 3 emissions in the first year? Cite the sources."

## Output (verbatim or screenshot)

Structured answer with numbered citations: Group 1 thresholds, NGER reporters, start dates, Scope 3 first-year relief, comparatives relief, modified liability period.

Screenshot: `../screenshots/fig15_exp02_chat_citations.png`

## Verification against sources
| Claim in output | Source & location | Correct? (Y / Partly / N) |
|---|---|---|
| Group 1: at least 2 of revenue >= $500m, gross assets >= $1bn, >= 500 employees | RG 280 | Y |
| Or registered NGER reporter above publishing threshold | RG 280 | Y |
| Group 1 covers FYs starting 1 Jan 2025 to 30 Jun 2026 | RG 280 | Y |
| No Scope 3 disclosure required in first annual reporting period | AASB S2 para. C4(b) | Y |
| No comparative information required in first period | AASB S2 para. C5 | Y |
| Modified liability for FYs starting 1 Jan 2025 to 31 Dec 2027 | RG 280 | Y |

## Ratings (1–5)
- Accuracy & relevance: 5
- Usefulness in academic workflow: 5

## Limitations / concerns observed
- Very reliable when grounded; citations make checking fast.
- Does not flag what the sources do not cover unless asked.
