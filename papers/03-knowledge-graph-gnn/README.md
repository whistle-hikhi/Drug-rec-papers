# Knowledge Graph / GNN Methods for Drug & Medicine Modeling

Covers (a) the major biomedical knowledge graphs the field builds on, and (b) GNN/KG-embedding methods applied to medication recommendation and drug repurposing/repositioning. Repurposing is included because it shares almost all its machinery (KG embedding, GNN encoders, link prediction) with recommendation — a drug-repurposing "which drug treats this disease" query and a medication-recommendation "which drug fits this patient" query are structurally the same link-prediction problem over different graphs.

## Foundational knowledge graphs

| Year | Resource | Key idea | Link |
|---|---|---|---|
| 2017 | Hetionet | 47,031 nodes / 2.25M edges across 11 node types & 29 relation types, integrated from 29 public resources; the standard drug-repurposing KG testbed | — |
| 2020 | DRKG (Drug Repurposing Knowledge Graph) | 97,238 entities / 5.87M triples / 107 relation types, merged from DrugBank, Hetionet, GNBR, STRING, IntAct, DGIdb + COVID-19 literature; built by Amazon + academic collaborators | — |

## Methods

| Year | Paper | Venue | Key idea | Link |
|---|---|---|---|---|
| 2021 | Analysis of Drug Repurposing Knowledge Graphs for COVID-19 | arXiv | Applies/analyzes KG embedding approaches on DRKG-style graphs for COVID-19 drug repurposing | [arXiv:2212.03911](https://arxiv.org/abs/2212.03911) |
| 2022 | Task-driven Knowledge Graph Filtering Improves Prioritizing Drugs for Repurposing | BMC Bioinformatics | Uses metapaths to filter Hetionet/DRKG before prediction, improving both accuracy and compute efficiency | [PMC8894843](https://pmc.ncbi.nlm.nih.gov/articles/PMC8894843/) |
| 2022 | EDGE: Knowledge-Driven New Drug Recommendation | arXiv | KG-driven recommendation specifically targeting new/unseen drugs | [arXiv:2210.05572](https://arxiv.org/pdf/2210.05572) |
| 2023 | Molecular-Evaluated and Explainable Drug Repurposing for COVID-19 Using Ensemble KG Embedding | Sci Reports | Ensembles multiple KG embedding models, adds molecular-level evaluation and explainability | [paper](https://www.nature.com/articles/s41598-023-30095-z) |
| 2024 | FedRKG: A Privacy-Preserving Federated Recommendation Framework via Knowledge Graph Enhancement | arXiv | Federated learning + KG enhancement — relevant if cross-institution EHR privacy is part of your framing | [arXiv:2401.11089](https://arxiv.org/pdf/2401.11089) |
| 2024 | Knowledge Graphs for Drug Repurposing: A Review of Databases and Methods | Briefings in Bioinformatics | **Survey** — good map of KG resources (Hetionet, DRKG, and others) and repurposing methods | [paper](https://academic.oup.com/bib/article/25/6/bbae461/7774899) |
| 2024 | Knowledge Graph Driven Medicine Recommendation System Using GNNs on Longitudinal Medical Records | Sci Reports | Builds per-admission clinical + medicine KGs from EHR + ontologies + DDI knowledge, learns embeddings via GNN | ⚠️ [RETRACTED](https://www.nature.com/articles/s41598-024-75784-5) — read for ideas only, do not cite as valid evidence |
| 2025 | Knowledge Enhanced Representation Learning Network for Drug Recommendation | ScienceDirect | KG-enhanced representation learning applied directly to the medication recommendation task | [paper](https://www.sciencedirect.com/science/article/abs/pii/S0306457325001050) |
| 2025 | DREAM-GNN: Dual-Route Embedding-Aware Graph Neural Networks for Drug Repositioning | bioRxiv | Dual-route GNN architecture for drug repositioning/repurposing | [paper](https://www.biorxiv.org/content/10.1101/2025.07.07.663530.full.pdf) |
| 2025 | Traceable Drug Recommendation over Medical Knowledge Graphs | arXiv | Emphasizes traceability/interpretability of recommendations via explicit KG paths | [arXiv:2510.27274](https://arxiv.org/html/2510.27274v1) |
| 2025 | A Survey of Graph Neural Networks for Drug Discovery: Recent Developments and Challenges | arXiv | **Survey** — general GNN-for-drug-discovery landscape (broader than repurposing/recommendation alone); good orientation piece for what's structurally possible with GNNs on molecular/biomedical graphs | [arXiv:2509.07887](https://arxiv.org/pdf/2509.07887) |
| 2026 | XAIPath: Generating Explainable Hypotheses for Drug Repurposing with Graph Neural Networks | PMC | GNN predictions + a post-hoc interpretability layer that extracts and clusters KG paths connecting drug-disease pairs into human-readable "mechanistic hypothesis" groups (via MinHash similarity + K-means) | [PMC13272636](https://pmc.ncbi.nlm.nih.gov/articles/PMC13272636/) |
| 2026 | Drug Repositioning Based on Expert Knowledge Augmented Graph Neural Network | — | Injects curated expert/domain knowledge directly into the GNN rather than relying solely on automatically-mined KG structure | [PubMed:41247891](https://pubmed.ncbi.nlm.nih.gov/41247891/) |
| 2026 | Empowering Graph Neural Network-Based Computational Drug Repositioning with Large Language Model-Inferred Knowledge Representation | PMC | Uses an LLM to *infer* additional knowledge representations that feed into the GNN — a direct bridge to [`04-llm-generative`](../04-llm-generative/README.md#knowledge-graph--llm-fusion)'s KG-LLM fusion thread, applied to repositioning rather than recommendation | [PMC12949635](https://pmc.ncbi.nlm.nih.gov/articles/PMC12949635/) |

## Notes for later reading
- **⚠️ Retraction flagged**: the Sci Reports 2024 "Knowledge graph driven medicine recommendation system" paper was retracted — worth reading to understand *why* (methodology or integrity issue) before citing anything downstream that relies on it. Formal retraction note: [PMC12835236](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12835236/).
- Hetionet and DRKG are the two graphs almost everything above is built or evaluated on — worth reading their construction papers directly rather than only secondary uses, since graph schema/coverage choices propagate into every downstream result.
- "Traceable"/"explainable" framing (2025 entries) suggests interpretability is becoming a distinguishing axis in KG-based recommendation, similar to how DDI-safety was the axis for EHR-based models circa 2021 — worth watching as a trend. The 2026 XAIPath entry extends this specifically to repurposing (explainable hypothesis clusters, not just per-prediction attention weights) — worth comparing its explanation *format* against Traceable Drug Recommendation's KG-path format.
- **KG-LLM fusion is now visible on the repositioning side too** (PMC12949635), not just the recommendation side already noted in `04-llm-generative` — the two threads (repositioning and recommendation) are converging on the same "let an LLM enrich the KG before the GNN reasons over it" pattern from two different starting tasks.
