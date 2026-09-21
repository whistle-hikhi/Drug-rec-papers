# Datasets for Drug / Medication Recommendation Research

A catalog of the actual datasets and databases used across this literature — as opposed to [`papers/06-datasets-beyond-mimic`](../papers/06-datasets-beyond-mimic/README.md), which tracks *papers* that evaluate on non-MIMIC data. This folder is the reusable resource list: what exists, what it contains, how to get it, and which model category (`01`–`07`) it feeds.

## A. EHR / clinical encounter datasets (sequential medication recommendation)

The substrate for GAMENet/SafeDrug-style models: per-visit diagnosis, procedure, and medication codes per patient, used to predict the next medication set/sequence.

| Dataset | Scope | Access | Link |
|---|---|---|---|
| **MIMIC-III** (Clinical Database v1.4) | ICU stays, single center (Beth Israel Deaconess, Boston), ~40k patients, 2001–2012 | Free, requires PhysioNet credentialing + CITI training | [physionet.org/content/mimiciii/1.4](https://physionet.org/content/mimiciii/1.4/) |
| **MIMIC-IV** (current: v3.1) | Successor to MIMIC-III; modular hosp/ICU structure, extends to 2019, adds eMAR (electronic medication administration record) | Free, PhysioNet credentialing | [physionet.org/content/mimiciv/3.1](https://physionet.org/content/mimiciv/3.1/) |
| **MIMIC-IV Demo** | 100-patient de-identified subset of MIMIC-IV — no credentialing needed, useful for pipeline testing before applying for full access | Fully open | [physionet.org/content/mimic-iv-demo/2.2](https://physionet.org/content/mimic-iv-demo/2.2/) |
| **eICU Collaborative Research Database** (v2.0) | Multi-center: 208 US hospitals, 2014–2015. Sparser per-hospital than MIMIC (most sites <1,500 records) and lacks procedure codes — the standard multi-center stress test. See [`papers/06`](../papers/06-datasets-beyond-mimic/README.md) for papers using it (DKINet, TEMPT) | Free, PhysioNet credentialing | [physionet.org/content/eicu-crd/2.0](https://physionet.org/content/eicu-crd/2.0/) |
| **CPRD** (Clinical Practice Research Datalink) | UK primary-care longitudinal EHR, ~50M patients, up to 20 years follow-up. Non-ICU, non-US — no medication-*recommendation* paper found using it yet (flagged as an opportunity in `papers/06`) | Paid, application + data-sharing agreement required | [cprd.com](https://www.cprd.com/) |
| **NHIRD** (Taiwan National Health Insurance Research Database) | Population-scale (~100% of Taiwan) administrative claims: diagnoses, prescriptions, procedures. Claims-based, not chart-based — structurally different input than MIMIC/eICU | Restricted, on-site/remote access via Taiwan Health and Welfare Data Science Center | [PMC6367203](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6367203/) |
| **CDrugRed** (CHIP 2025 Shared Task 2) | Purpose-built Chinese medication-recommendation dataset: 5,894 de-identified hospitalization records, 3,190 patients, metabolic-disease focus | Shared-task registration | [arXiv:2511.06230](https://arxiv.org/abs/2511.06230) |

## B. Drug & biomedical knowledge graphs

Used by `03-knowledge-graph-gnn` for KG-grounded recommendation and repurposing, and increasingly as retrieval context for `04-llm-generative`.

| Dataset | Scope | Access | Link |
|---|---|---|---|
| **DrugBank** | ~15k drug entries (small molecules, biologics, experimental), targets, mechanisms, DDI annotations (v5.1.4: 1,706 drugs, ~192k DDI pairs, 86 interaction types) | Free for academic use via account; commercial license for bulk/API | [go.drugbank.com](https://go.drugbank.com/) |
| **PrimeKG** (Precision Medicine KG, Zitnik Lab) | 17,080 diseases, 4.05M relationships across 10 biological scales (drugs, disease, protein, pathway, phenotype...), integrates 20 source databases; single CSV, no DB setup needed. Same lab as TxGNN (`03-knowledge-graph-gnn`). Note: the maintainers now point to **OptimusKG** as the superset/successor | Open, Harvard Dataverse | [doi.org/10.7910/DVN/IXA7BM](https://doi.org/10.7910/DVN/IXA7BM) · [GitHub](https://github.com/mims-harvard/PrimeKG) |
| **Hetionet** (v1.0) | Heterogeneous network for drug repurposing (Project Rephetio): 47k nodes / 11 types (drugs, diseases, genes, ...), 2.25M edges / 24 relationship types | Open | [github.com/hetio/hetionet](https://github.com/hetio/hetionet) |
| **SIDER** (Side Effect Resource, v4.1) | Side effects extracted from drug package inserts/labels; drug–side-effect associations with frequency where available | Open | [sideeffects.embl.de](https://sideeffects.embl.de/) |
| **KEGG DRUG** | Drug structures, classifications, targets, metabolizing enzymes, linked to KEGG pathways | Free for academic use (registration); commercial license (FTP bulk) separate | [genome.jp/kegg/drug](https://www.genome.jp/kegg/drug/) |

## C. Drug-drug interaction (DDI) datasets

Core evaluation resource for `02-ddi-aware` — used both to *train* DDI predictors and to *score* the safety of a recommended combination (the DDI-rate metric used throughout `01-ehr-based`).

| Dataset | Scope | Access | Link |
|---|---|---|---|
| **BIOSNAP ChCh-Miner** (Stanford) | Network of FDA-approved drug–drug interactions: ~1,514 drugs, ~48,514 interaction edges. The most commonly used DDI graph in GAMENet/SafeDrug-lineage papers | Open | [snap.stanford.edu/biodata/datasets/10001](https://snap.stanford.edu/biodata/datasets/10001/10001-ChCh-Miner.html) |
| **DrugBank DDI** | Curated, literature-derived DDI pairs with severity classification, drawn from DrugBank itself | Same access as DrugBank above | [go.drugbank.com](https://go.drugbank.com/) |
| **DDInter 2.0** | Curated DDI database with mechanism descriptions, risk levels, management strategies, and suggested alternative medications — richer annotation than DrugBank/TWOSIDES for clinical-explanation use cases. v2.0: 2,310 drugs, 302,516 DDI records | Free, no login required | [ddinter2.scbdd.com](https://ddinter2.scbdd.com/) |
| **TWOSIDES / OFFSIDES** (nSIDES, Tatonetti Lab) | Mined from FDA Adverse Event Reporting System (FAERS): OFFSIDES = single-drug off-label side effects; TWOSIDES = drug-*pair* adverse-event associations (868k+ significant associations, 59k+ drug pairs, 1,301 adverse events) — population-scale signal-detection data rather than curated literature facts | Open (DB dumps + CSV) | [nsides.io](https://nsides.io/) · [GitHub releases](https://github.com/tatonetti-lab/nsides-release/releases) |

## D. Molecular / chemical structure datasets

Used where models encode drugs by chemical structure rather than (or in addition to) a categorical code — e.g. SafeDrug's dual molecular-graph encoder.

| Dataset | Scope | Access | Link |
|---|---|---|---|
| **PubChem** | >100M compounds, bioassay data, SMILES/structure lookup by drug name or DrugBank ID | Open | [pubchem.ncbi.nlm.nih.gov](https://pubchem.ncbi.nlm.nih.gov/) |
| **ChEMBL** | ~2.4M bioactive compounds with target/assay/bioactivity data, curated from literature | Open | [ebi.ac.uk/chembl](https://www.ebi.ac.uk/chembl/) |
| **DrugBank structures** | SMILES/molecular structure per drug entry, cross-referenced to the DDI/target data above | Same access as DrugBank | [go.drugbank.com](https://go.drugbank.com/) |

## E. Coding vocabularies (glue, not data — needed to link the above)

| Resource | Purpose | Link |
|---|---|---|
| **RxNorm** | Normalized drug names/codes; the standard key for mapping EHR medication codes to DrugBank/ATC | [nlm.nih.gov/research/umls/rxnorm](https://www.nlm.nih.gov/research/umls/rxnorm/) |
| **ATC** (Anatomical Therapeutic Chemical Classification) | Drug classification hierarchy used by GAMENet/SafeDrug to bucket NDC codes into a tractable medication vocabulary | [WHOCC ATC/DDD Index](https://www.whocc.no/atc_ddd_index/) |
| **ICD-9/ICD-10** | Diagnosis/procedure coding used in MIMIC and most claims data | [CMS ICD-10](https://www.cms.gov/medicare/coding-billing/icd-10-codes) |

## Reference code for data processing

Most `01-ehr-based` papers don't redistribute processed MIMIC data (PhysioNet's license forbids it) — instead they ship the *processing pipeline* against a MIMIC download you obtain yourself:

- **GAMENet**: MIMIC-III → `records_final.pkl` pipeline + preprocessed DDI graph — [github.com/sjy1203/GAMENet](https://github.com/sjy1203/GAMENet)
- **SafeDrug**: MIMIC-III/IV processing + medical code mapping (ATC↔RxNorm↔NDC) + ChCh-Miner DDI integration — [github.com/ycq091044/SafeDrug](https://github.com/ycq091044/SafeDrug)

## Notes

- **Getting started fastest**: MIMIC-IV Demo (no credentialing) + BIOSNAP ChCh-Miner (open) + SafeDrug's processing scripts covers the full `01`/`02` pipeline without waiting on PhysioNet approval, which can take days.
- **PhysioNet credentialing is the main access bottleneck** for this whole area (MIMIC-III, MIMIC-IV, eICU all require it) — apply early if training a new model rather than reusing preprocessed data from a paper's repo.
- **DrugBank license changed over the years** — older papers cite freely-downloadable DrugBank XML dumps; current access is account-gated (free tier for academic/non-commercial use still exists, but check current terms before assuming programmatic bulk download works as in older tutorials).
- **PrimeKG → OptimusKG**: the Zitnik Lab now recommends OptimusKG as PrimeKG's superset/successor; PrimeKG is still what most published `03-knowledge-graph-gnn` papers actually used, so keep both names in mind when searching for follow-on work.
- **CPRD and NHIRD remain unused for medication-*recommendation* modeling specifically** (as opposed to pharmacoepidemiology) per the gap noted in `papers/06-datasets-beyond-mimic` — applying the GAMENet/SafeDrug lineage to either would be genuinely new.
