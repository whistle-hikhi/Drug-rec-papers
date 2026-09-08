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
  05-fairness-bias/       fairness/bias evidence & methodology, cross-cutting across 01-04
  06-datasets-beyond-mimic/ non-MIMIC evaluation datasets (eICU, CPRD, NHIRD, private/non-US EHR)
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
| Fairness/bias in clinical AI | [Dissecting Racial Bias in an Algorithm Used to Manage the Health of Populations](https://www.science.org/doi/10.1126/science.aax2342) — landmark, not a survey but the reference point everything else cites | Science, 2019 |

## Status

Seeded 2026-08-19 via targeted search across the four focus areas (~55 papers), then extended three times the same day: to fill out `04-llm-generative`'s architecture side (agentic/multi-agent, RAG, fine-tuning/alignment, KG-LLM fusion); to add `05-fairness-bias` (~29 papers) after the initial pass surfaced no fairness/bias coverage at all; and to add `06-datasets-beyond-mimic` (~9 papers/resources) after noting every `01-ehr-based` model was benchmarked on MIMIC alone.

Refreshed 2026-09-08 with a general sweep for new/recent papers across all six areas (~26 additions, mostly 2025-2026): new DDI-prediction models (AIM-DDI, MARD, InfoMedex, a relation-learning reframing), new KG/GNN repositioning work (XAIPath, expert-knowledge-augmented GNN, an LLM-KG fusion bridge), a new agentic-LLM evaluation paper, and — most notably — **RAREMed and DMRNet**, the first two papers found that evaluate fairness directly on the medication-recommendation task itself (drug-frequency fairness, not yet demographic subgroup fairness) rather than on an adjacent task, partially closing the gap flagged in the previous update. Also corrected one paper's recorded title (arXiv:2510.21084 is "MediRec," not "Chinese Discharge Drug Recommendation..." as previously listed). Collection is now ~119 papers. Not exhaustive — treat as a scaffold to keep extending as you read. See `NOTES.md` for what's thin and worth digging into next.
