# Drug-rec-papers

A working literature collection on **drug / medication recommendation systems**, organized for ongoing PhD reading. Covers four sub-areas: EHR-based recommendation, drug-drug interaction (DDI) aware recommendation, knowledge graph / GNN methods, and LLM / generative approaches.

Each paper is tracked with year, venue, a one-line summary of its core idea, and a link. Full citations live in [`references.bib`](references.bib). Cross-cutting themes and open questions are in [`NOTES.md`](NOTES.md).

## How this is organized

```
papers/
  01-ehr-based/          patient history -> medication set/sequence prediction
  02-ddi-aware/           interaction-safety-constrained recommendation & DDI prediction
  03-knowledge-graph-gnn/ KG- and GNN-based drug/medicine modeling
  04-llm-generative/      LLMs for medication recommendation & clinical decision support
references.bib            consolidated BibTeX for everything below
NOTES.md                  synthesis: trends, tensions, gaps across the four areas
```

Note the categories overlap heavily in practice — e.g. GAMENet/SafeDrug are EHR-based models that are *also* DDI-aware, and several LLM papers use KG grounding. A paper is filed under its primary contribution; cross-references are noted inline.

## Reading starting points (surveys)

Start here before diving into individual models — these give the lay of the land for each sub-area:

| Area | Survey | Venue/Year |
|---|---|---|
| EHR-based medication rec | [Deep Learning for Medication Recommendation: A Systematic Survey](https://direct.mit.edu/dint/article/5/2/303/114891/Deep-Learning-for-Medication-Recommendation-A) | Data Intelligence (MIT Press), 2023 |
| DDI prediction | [Deep learning for drug-drug interaction prediction: A comprehensive review](https://onlinelibrary.wiley.com/doi/full/10.1002/qub2.32) | Quantitative Biology, 2024 |
| KG for drug repurposing | [Knowledge Graphs for drug repurposing: a review of databases and methods](https://academic.oup.com/bib/article/25/6/bbae461/7774899) | Briefings in Bioinformatics, 2024 |
| LLMs for clinical reasoning | [Aligning Clinical Needs and AI Capabilities: A Survey on LLMs for Medical Reasoning](https://arxiv.org/pdf/2607.07761) | arXiv, 2026 |

## Status

Seeded 2026-08-19 via targeted search across the four focus areas (~55 papers, after a follow-up pass that filled out `04-llm-generative`'s architecture side — agentic/multi-agent, RAG, fine-tuning/alignment, KG-LLM fusion). Not exhaustive — treat as a scaffold to keep extending as you read. See `NOTES.md` for what's thin and worth digging into next.
