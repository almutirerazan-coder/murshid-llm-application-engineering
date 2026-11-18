# Murshid Mini — LLM Application Engineering

A small **fictional** government-service assistant built step by step over four days. It answers known service questions, reads an application's status through an authorized read-only tool, rejects unsuitable input, tests its own behaviour, and caches public answers safely.

**Author:** Razan
**Program:** LLM Application Engineering — SDA-AIE-213, delivered within the [SDAIA Academy](https://github.com/SDAIAAcademy) training context
**Instructor:** Meaad Al-Marri

> **Important — `mode=mock`.** `FakeClient` is a deterministic Python simulator, **not a live language model**. This project practises the engineering *around* an LLM-shaped interface. All data is synthetic. No real service records or personal data are used.

## Problem and intended users
People often ask the same few questions about a service ("How do I check my application?") or want their application status. The intended user is a learner/developer who wants to see how an LLM application is made safe and testable: structured output, controlled tools, guards, tests and caching.

## Progress
| Day | Topic | What was built | Result |
|---|---|---|---|
| 1 | Foundations | Synthetic directory, `FakeClient` mock, `ask()` and the response contract | [baseline_results.json](results/core/baseline_results.json) — three known answers; blank input adds no mock call |
| 2 | Structure and tools | _coming next_ | |
| 3 | Guards and evaluation | _coming next_ | |
| 4 | Cache and final project | _coming next_ | |

## Repository contents
- [`notebooks/murshid.ipynb`](notebooks/murshid.ipynb) — the single cumulative project notebook (all core days, with outputs)
- [`results/core/`](results/core) — JSON results produced by running the notebook


## Homework completed
- _None yet._

## How to run
1. Open [Google Colab](https://colab.research.google.com/) → **File → Upload notebook** → choose `notebooks/murshid.ipynb`.
2. Runtime: Python 3, **CPU** (no GPU). Nothing to install — standard library only, no API key, no downloads.
3. **Runtime → Run all.** Each day's final cell prints `"checks": "passed"` and JSON files appear in `murshid_outputs/`.

---
Attribution: built as coursework for **LLM Application Engineering — SDA-AIE-213** (SDAIA Academy training context), instructor **Meaad Al-Marri**. This link is attribution only, not a claim of endorsement.
