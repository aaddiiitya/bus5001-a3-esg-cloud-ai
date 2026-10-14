# EXP-05: Mind Map + hallucination probe

- **Date/time:** 12 Oct 2026, afternoon (AEDT)
- **Tool:** NotebookLM (now served at notebook.google.com as "Gemini Notebook"), free personal Google account
- **Notebook:** "ASIC Regulatory Guide 280: Sustainability Reporting" (auto-titled)
- **Sources in notebook:** AASB S2 (2024) PDF; ASIC RG 280 (2025) PDF; KPMG guide URL **failed to load**
- **Feature tested:** Mind Map + hallucination probe
- **Scenario / user role:** student preparing a governance workshop briefing on Australian mandatory climate reporting
- **Exact prompt or action:** Studio > Mind Map. Then in chat: "What fine did ASIC give Woolworths for breaching AASB S2 in 2025?" (false premise: no such fine exists in the sources).

## Output (verbatim or screenshot)

Mind map with 5 branches: Overview and Scope; Preparing the Sustainability Report; Content Required in Report; Disclosures Outside Sustainability Report; ASIC Administration and Enforcement. Chat: "The provided sources do not mention any fine or enforcement action taken by ASIC against Woolworths for breaching AASB S2 in 2025."

Screenshot: `../screenshots/fig18_exp05_mindmap_false_premise.png`

## Verification against sources
| Claim in output | Source & location | Correct? (Y / Partly / N) |
|---|---|---|
| Branches follow RG 280 structure | RG 280 | Y |
| Map title | Labelled "Sustainability Reporting Flashcards" | N |
| False premise rejected | No such fine in sources | Y |

## Ratings (1–5)
- Accuracy & relevance: 4
- Usefulness in academic workflow: 3

## Limitations / concerns observed
- Mind map mislabelled; root label clipped on first render (fine after reload).
- AASB S2 content (metrics, targets) under-represented.
- Positive: grounded chat refused to hallucinate a penalty.
