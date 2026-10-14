# Q3 – LLM-based ESG message triage

Run `20261011T161818Z` in Google Colab (Tesla T4, transformers 5.18, torch 2.11).

| Path | Contents |
|---|---|
| `q3_llm_triage_executed.ipynb` | Full notebook **with all outputs** |
| `prompts/` | v1 baseline prompt (from the brief) and v2 revised prompt |
| `data/messages_labelled.txt` | 8 test messages with expected labels |
| `logs/` | Raw LLM outputs (v1 and v2, all 8 messages), zero-shot and rule-based outputs |
| `results/` | Accuracy summary, per-message comparison, consistency check |

**Headline:** category accuracy v1 0%, v2 75%, zero-shot (bart-large-mnli) 75%, rule-based 88%.
