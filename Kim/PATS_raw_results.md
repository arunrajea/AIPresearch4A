# Raw Experimental Results (160 Emails)

**Experiment:** Jev 1.14 decision model versus general-purpose LLMs on email purpose, urgency, and sender relationship classification.

**Dataset:** 160 emails, with work, promotional, school and personal as separate purpose classes. The values below are the raw summary metrics produced by the experiment scripts. Accuracy is measured against the current provisional reference labels.

## Run 1 — Jev vs. GPT-4o Mini

| Metric | Jev (`typesafe/jev-1.14`) | GPT-4o Mini (`openai/gpt-4o-mini`) |
|---|---:|---:|
| Purpose accuracy | 96.2% (160 evaluated) | 93.8% (160 evaluated) |
| Urgency accuracy | 68.8% (160 evaluated) | 48.8% (160 evaluated) |
| Relationship accuracy | 95.6% (160 evaluated) | 91.2% (160 evaluated) |
| Average response time | 0.179s | 0.837s |
| Reported API cost (total) | $0.007002 | $0.017033 |
| Errors | 0 / 160 | 0 / 160 |

## Run 2 — Jev vs. GLM-5.3 Flash

| Metric | Jev (`typesafe/jev-1.14`) | GLM-5.3 Flash (`z-ai/glm-5.3-flash`) |
|---|---:|---:|
| Purpose accuracy | 96.2% (160 evaluated) | 92.5% (160 evaluated) |
| Urgency accuracy | 69.4% (160 evaluated) | 75.0% (160 evaluated) |
| Relationship accuracy | 95.6% (160 evaluated) | 90.0% (160 evaluated) |
| Average response time | 0.155s | 4.087s |
| Reported API cost (total) | $0.007002 | $0.042860 |
| Errors | 0 / 160 | 0 / 160 |


## Run 3 — Jev vs. Gemini 3.8 Flash


| Metric | Jev (`typesafe/jev-1.14`) | Gemini 3.8 Flash (`google/gemini-3.8-flash`) |
|---|---:|---:|
| Purpose accuracy | 95.6% (160 evaluated) | 93.7% (158 evaluated) |
| Urgency accuracy | 69.4% (160 evaluated) | 83.5% (158 evaluated) |
| Relationship accuracy | 95.0% (160 evaluated) | 93.0% (158 evaluated) |
| Average response time | 0.196s | 5.791s |
| Reported API cost (total) | $0.007002 | $0.292652 |
| Errors | 0 / 160 | 2 / 160 |

## Comparison across completed runs

| Model / run | Purpose | Urgency | Relationship | Avg. time | Total cost | Errors |
|---|---:|---:|---:|---:|---:|---:|
| Jev (with GPT-4o Mini) | 96.2% | 68.8% | 95.6% | 0.179s | $0.007002 | 0/160 |
| GPT-4o Mini | 93.8% | 48.8% | 91.2% | 0.837s | $0.017033 | 0/160 |
| Jev (with GLM-5.3 Flash) | 96.2% | 69.4% | 95.6% | 0.155s | $0.007002 | 0/160 |
| GLM-5.3 Flash | 92.5% | 75.0% | 90.0% | 4.087s | $0.042860 | 0/160 |
| Jev (with Gemini 3.8 Flash) | 95.6% | 69.4% | 95.0% | 0.196s | $0.007002 | 0/160 |
| Gemini 3.8 Flash | 93.7% (158 evaluated) | 83.5% (158 evaluated) | 93.0% (158 evaluated) | 5.791s | $0.292652 | 2/160 |


## Notes on interpretation

- GPT-4o Mini, GLM-5.3 Flash, and Gemini 3.8 Flash were run independently, and Jev was re-run alongside each LLM. Jev's reported metrics differ slightly between the runs.
- Gemini returned 2 errors, so its accuracy denominators are 158, not 160. The average response time and reported cost figures are kept as provided.
- Compare model behavior using per-email CSV outputs in addition to the summary statistics when we conclude.
