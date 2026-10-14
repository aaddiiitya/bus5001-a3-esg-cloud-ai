# BUS5001 Assessment 3 – RPA, AI and Cloud-Enabled ESG Analytics

**Student:** Aditya Manoj Bajpai · La Trobe University · 2026 Semester 2
**Scenario:** Consultant/analyst for a large organisation using cloud automation and AI to improve ESG reporting and operations.

This repository holds the experiment logs and evidence for the Assessment 3 report.

| Folder | Report section | What it contains |
|---|---|---|
| [`q1-dialogflow-cx/`](q1-dialogflow-cx) | Q1 – ESG Sustainability Support Assistant (Dialogflow CX) | Build specification (intents, entities, pages, routes, tests) and demo video script. [Demo video](https://echo360.net.au/media/53e1199d-9387-4bbd-b4d1-9c9d66c81b4f/h5p) |
| [`q2-cloud-security/`](q2-cloud-security) | Q2 – Snowflake/UNC5537 cloud security incident | Summary; analysis and diagram are in the report (Figure 11) |
| [`q3-llm-triage/`](q3-llm-triage) | Q3 – LLM ESG message triage | Executed Colab notebook, prompts v1 → v2, labelled test messages, raw model outputs (`logs/`), accuracy and consistency results (`results/`) |
| [`q4-notebooklm/`](q4-notebooklm) | Q4 – NotebookLM evaluation | Sources list, six experiment logs (EXP-01 to EXP-06), screenshots (report Figures 14–19) |

## Conventions
- Q3 files are prefixed with the run id (`20261011T161818Z`) so logs and results trace to one run.
- Raw model outputs are stored unedited in `logs/`; analysed results in `results/`.
- Q4 logs follow `experiments/_TEMPLATE.md`: prompt, output, verification against sources, ratings, limitations.
- No secrets (API tokens) are committed. See `.gitignore`.
- No personal or real employee data is used; all messages are simulated.
