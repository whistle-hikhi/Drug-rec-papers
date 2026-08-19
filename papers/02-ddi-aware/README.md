# Drug-Drug Interaction (DDI) Aware Recommendation

Two related but distinct tasks live here: (1) **DDI prediction** — given two (or more) drugs, predict whether/how they interact, usually from molecular structure; and (2) **interaction-aware recommendation** — using DDI knowledge as an explicit constraint or penalty when recommending a combination/package of drugs. Many EHR-based models in [`01-ehr-based`](../01-ehr-based/README.md) (GAMENet, SafeDrug, 4SDrug) already fold DDI-awareness in as a soft constraint; the papers below are the DDI-prediction methods those constraints are typically built on, plus standalone interaction-aware package/combination recommenders.

| Year | Paper | Venue | Key idea | Link |
|---|---|---|---|---|
| 2018 | DeepDDI: chemical structure-based DNN for DDI prediction | PNAS | Classic baseline: structural similarity profile (SSP) from SMILES + DNN multi-label classifier over interaction types | — |
| 2020 | CASTER: Predicting Drug Interactions with Chemical Substructure Representation | AAAI / Bioinformatics | Extracts functional substructures via sequence mining + autoencoder pretraining; projects drug pairs into an interpretable substructure ("dictionary learning") space | — |
| 2021 | SSI-DDI: Substructure-Substructure Interactions for DDI Prediction | Briefings in Bioinformatics | Graph Attention Networks decompose each drug into substructures and predict interaction at the substructure-pair level for interpretability | [paper](https://academic.oup.com/bib/article/22/6/bbab133/6265181) |
| 2021 | MIRACLE: Multi-view Graph Contrastive Representation Learning for DDI Prediction | KDD | Contrastive learning across intra-molecular (structural) and inter-molecular (interaction) graph views, balanced via contrastive loss | — |
| 2021 | Drug Package Recommendation via Interaction-aware Graph Induction | WWW | Message-passing network models interactions between drugs *within* a package; induces a package-level graph rather than treating drugs independently | [arXiv:2102.03577](https://arxiv.org/pdf/2102.03577) |
| 2022 | Interaction-aware Drug Package Recommendation via Policy Gradient | ACM TOIS | RNN-based drug package generator + deep RL (policy gradient) to reduce dependence on drug ordering while respecting interaction constraints | [paper](https://dl.acm.org/doi/10.1145/3511020) |
| 2023 | Relation-aware Graph Structure Embedding with Co-contrastive Learning for DDI Prediction | arXiv | Co-contrastive learning over relation-aware graph structure embeddings | [arXiv:2307.01507](https://arxiv.org/pdf/2307.01507) |
| 2023 | A Knowledge-Graph-Based Multimodal Deep Learning Framework for Identifying DDIs (KGCN_NFM) | PMC | Combines Knowledge Graph Convolutional Networks + Neural Factorization Machines over KG structure and molecular fingerprints | [PMC9919258](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9919258/) |
| 2024 | Deep graph contrastive learning model for DDI prediction | PMC | Graph contrastive learning applied to the DDI prediction task | [PMC11182529](https://pmc.ncbi.nlm.nih.gov/articles/PMC11182529/) |
| 2026 | OpenDDI: A Comprehensive Benchmark for DDI Prediction | arXiv | Recent standardized benchmark — useful as a reference point for which DDI predictors are currently SOTA and how they're evaluated | [arXiv:2602.00539](https://arxiv.org/pdf/2602.00539) |

## Notes for later reading
- Track which **DDI knowledge source** each recommender uses downstream (TWOSIDES, DrugBank interaction lists, or a learned predictor like SSI-DDI/CASTER/MIRACLE) — this matters a lot for how "real" the safety guarantee is.
- The substructure-based line (CASTER → SSI-DDI → MIRACLE) and the package/combination-recommendation line (interaction-aware graph induction → policy-gradient package rec) are two different lineages worth tracking separately.
- OpenDDI (2026) is worth reading early since a fresh benchmark paper usually cites/reproduces most predecessors and clarifies the current leaderboard.
