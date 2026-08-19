# Cross-Cutting Notes

Synthesis across [`01-ehr-based`](papers/01-ehr-based/README.md), [`02-ddi-aware`](papers/02-ddi-aware/README.md), [`03-knowledge-graph-gnn`](papers/03-knowledge-graph-gnn/README.md), [`04-llm-generative`](papers/04-llm-generative/README.md), [`05-fairness-bias`](papers/05-fairness-bias/README.md). Update this as the collection grows.

## The field's recurring axis: accuracy vs. safety

Every sub-area re-derives some version of the same tradeoff:
- EHR-based: Jaccard/F1 (matches actual prescription) vs. DDI rate of the recommended set.
- DDI-aware: interaction-prediction recall vs. false-positive rate (over-flagging safe combinations is also costly).
- KG/GNN: link-prediction accuracy vs. explainability/traceability of *why* a drug was linked.
- LLM: raw recommendation quality vs. verified safety (hence the 2025-2026 explosion of safety benchmarks rather than new recommender architectures).

Worth stating explicitly in a related-work section rather than treating each area as solving unrelated problems — the throughline is safety-constrained accuracy.

## Convergence between sub-areas

- **EHR-based models increasingly *are* DDI-aware** (GAMENet onward) — the two areas were split for search purposes but functionally the EHR-based lineage absorbed the DDI constraint by ~2019 rather than treating it as a separate downstream step.
- **KG/GNN and LLM approaches are actively merging** (KEDRec-LM, "LLM distilling medication recommendation model") — the KG's structured constraint plus the LLM's generative/reasoning flexibility is a clear active combination point, not yet settled.
- **Drug repurposing and medication recommendation are the same link-prediction problem on different graphs** (patient-drug vs. disease-drug) — methodology from `03-knowledge-graph-gnn` repurposing papers is directly transferable, worth reading even if repurposing itself isn't the target application.

## Gaps / thin spots in the current collection (worth expanding)

- **No papers yet on evaluation datasets beyond MIMIC** — everything in `01-ehr-based` leans on MIMIC-III/IV; worth checking whether other EHR datasets (eICU, CPRD, non-US records) are used anywhere, since MIMIC-only evaluation is a known field-wide limitation.
- ~~No explicit fairness/bias papers~~ — **addressed 2026-08-19**: new `05-fairness-bias` category, ~29 papers. But the search also surfaced a *narrower, sharper* gap worth carrying forward: no paper evaluates fairness on the actual combinatorial medication-recommendation task (GAMENet/SafeDrug-style, subgroup-broken-down Jaccard/DDI-rate) — only on adjacent tasks (opioid-use-disorder risk, readmission, LLM medical QA). That intersection looks like genuine white space, not just a search artifact, though it deserves a second, more exhaustive pass (ACM FAccT, health-informatics venues) before relying on that conclusion.
- **No cost-effectiveness or clinician-in-the-loop / human-factors papers** — the collection is all model-side; nothing yet on how clinicians actually use or override these systems in practice.
- ~~LLM area has heavy benchmark/eval representation but few new architectures~~ — **addressed 2026-08-19**: `04-llm-generative` now has 20 architecture papers across four threads (agentic/multi-agent, RAG, fine-tuning/alignment, KG-LLM fusion) plus 6 benchmark/eval papers. FLAME and SafeRx-Agent are the strongest read-first picks since both explicitly target DDI-safety, mirroring GAMENet/SafeDrug's role in `01-ehr-based`.
- **One retracted paper flagged** in `03-knowledge-graph-gnn` (Sci Reports 2024 KG medicine recommendation) — confirm you understand the retraction reason before relying on any of its claims, even informally.

## Suggested reading order

1. Survey papers listed in the top-level [README](README.md) — one per sub-area, ~2-3 hrs total, gives shared vocabulary.
2. The EHR-based "spine": GAMENet → SafeDrug → MICRON → COGNet → MoleRec (each explicitly benchmarks the prior ones).
3. Pick one DDI-prediction method (SSI-DDI or MIRACLE) to understand how the DDI constraint used upstream is actually computed.
4. One KG paper (Hetionet or DRKG construction) to understand what's actually inside the knowledge graphs being embedded.
5. Two or three LLM papers spanning the "distillation," "safety benchmark," and "RAG" threads to see how differently framed the same underlying problem is.
6. Obermeyer et al. 2019 (Science) as the fairness-in-clinical-AI reference point, then one opioid-prescribing-bias paper from `05-fairness-bias` section B as the closest existing analogue to "fairness in drug recommendation."

## Log

- **2026-08-19**: Initial seed, ~35 papers across 4 areas via targeted web search. Not systematic (no formal database query / PRISMA-style search yet) — treat as a scaffold.
- **2026-08-19 (later same day)**: Filled the LLM-architecture gap noted above — added ~20 papers to `04-llm-generative`, split into agentic/multi-agent, RAG, fine-tuning/alignment, and KG-LLM fusion sub-threads, plus one taxonomy/survey paper (2602.04813). Collection is now ~55 papers total.
- **2026-08-19 (again)**: Added `05-fairness-bias` (~29 papers: foundational/surveys, opioid/prescribing-specific bias, general clinical-prediction fairness methodology, LLM/clinical-NLP bias benchmarks, fairness-aware recommender-systems methodology). Surfaced a sharper follow-up gap: no fairness audit exists yet of the actual medication-recommendation task itself, only adjacent tasks. Collection is now ~84 papers total.
