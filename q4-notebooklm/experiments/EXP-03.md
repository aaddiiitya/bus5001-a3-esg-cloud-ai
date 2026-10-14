# EXP-03: Reports: Briefing Doc

- **Date/time:** 12 Oct 2026, afternoon (AEDT)
- **Tool:** NotebookLM (now served at notebook.google.com as "Gemini Notebook"), free personal Google account
- **Notebook:** "ASIC Regulatory Guide 280: Sustainability Reporting" (auto-titled)
- **Sources in notebook:** AASB S2 (2024) PDF; ASIC RG 280 (2025) PDF; KPMG guide URL **failed to load**
- **Feature tested:** Reports: Briefing Doc
- **Scenario / user role:** student preparing a governance workshop briefing on Australian mandatory climate reporting
- **Exact prompt or action:** Studio > Reports > Briefing Doc, with custom prompt asking for a 1-page briefing for a governance workshop.

## Output (verbatim or screenshot)

"Executive Briefing: ASIC Regulatory Guide 280 (RG 280) - Sustainability Reporting". 3,592 words. Includes executive summary and Group 1/2/3 threshold table.

Screenshot: `../screenshots/fig16_exp03_briefing_doc.png`

## Verification against sources
| Claim in output | Source & location | Correct? (Y / Partly / N) |
|---|---|---|
| Group 2: 2 of $200m revenue / $500m assets / 250 employees; asset owners >= $5bn | RG 280 | Y |
| Group 3: 2 of $50m revenue / $25m assets / 100 employees | RG 280 | Y |
| Group 2 from FYs starting 1 Jul 2026; Group 3 from 1 Jul 2027 | RG 280 | Y |
| Length is 1 page as requested | 3,592 words | N |
| Built from 3 sources | Only 2 loaded | N |

## Ratings (1–5)
- Accuracy & relevance: 4
- Usefulness in academic workflow: 3

## Limitations / concerns observed
- Ignored the length constraint.
- No inline citations in the report, unlike chat.
- Inaccurate source count in header.
- High risk of uncited text being pasted into assessed work (over-reliance / integrity).
