# Fairness & Bias in Drug/Medication Recommendation

Added 2026-08-19 to close the gap flagged in [`NOTES.md`](../../NOTES.md): none of the original four areas surfaced anything on demographic bias in recommended medications. This category is cross-cutting by nature — it applies to EHR-based models, KG/GNN methods, and LLMs alike — so it's organized by *what kind of harm/evidence* rather than by which of the other four areas it touches.

No paper found so far evaluates fairness **on the exact GAMENet/SafeDrug-style medication-recommendation task** (Jaccard/DDI-rate broken out by demographic subgroup) — that specific intersection looks like an open gap in the literature itself, not just in this collection (see notes below). What exists instead are: (a) the landmark case showing algorithmic bias in a *related* clinical-risk task, (b) fairness studies on the *closest adjacent task* (opioid/substance-use prediction, which is prescribing-relevant), (c) general clinical-prediction fairness methodology, (d) LLM/clinical-NLP bias benchmarks, and (e) fairness-aware recommender-systems methodology transferable to the drug-rec setting.

## A. Foundational & surveys — start here

| Year | Paper | Venue | Key idea | Link |
|---|---|---|---|---|
| 2019 | Dissecting Racial Bias in an Algorithm Used to Manage the Health of Populations | Science | **Landmark paper.** A widely deployed commercial risk algorithm used health *cost* as a proxy for health *need*; because less is spent on Black patients for the same level of sickness, the algorithm assigned them systematically lower risk scores than equally sick White patients — reducing referrals to extra care. The canonical example of a proxy-variable bias mechanism worth citing whenever motivating this whole sub-area. | [Science](https://www.science.org/doi/10.1126/science.aax2342) |
| 2021 | Algorithm Fairness in AI for Medicine and Healthcare | arXiv | Survey of fairness definitions/metrics and where they break down specifically in clinical settings | [arXiv:2110.00603](https://arxiv.org/abs/2110.00603) |
| 2022 | Algorithmic Fairness in Computational Medicine | eBioMedicine | Review of fairness concepts applied across computational-medicine pipelines (data, model, deployment) | [paper](https://www.thelancet.com/journals/ebiom/article/PIIS2352-3964(22)00432-7/fulltext) |
| 2022 | Evaluation and Mitigation of Racial Bias in Clinical Machine Learning Models: Scoping Review | JMIR Medical Informatics | Of 12 studies reviewed, 8 (67%) found racial bias present; documents which fairness metrics are actually used in practice (equal opportunity difference most common) and flags inconsistency across studies | [PMC9198828](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9198828/) |
| 2024 | AI-Driven Healthcare: A Survey on Ensuring Fairness and Mitigating Bias | arXiv | Broader 2024 survey spanning data bias, model bias, and mitigation techniques (pre-/in-/post-processing) across healthcare AI | [arXiv:2407.19655](https://arxiv.org/html/2407.19655v1) |

## B. Prescribing / opioid-specific bias — closest adjacent task to drug recommendation

| Year | Paper | Venue | Key idea | Link |
|---|---|---|---|---|
| 2023 | Predicting Opioid Use Outcomes in Minoritized Communities | arXiv | Directly examines how ML opioid-outcome prediction underperforms/misfires for minoritized populations | [arXiv:2307.03083](https://arxiv.org/html/2307.03083) |
| 2023 | Disparities in Postoperative Opioid Prescribing by Race and Ethnicity | Northern California EHR study (observational, not ML) | Real-world evidence that Black patients received prescriptions with lower mean morphine milligram equivalents than White patients post-surgery — grounding evidence for what a fair *recommendation* system should and shouldn't reproduce | [PMC10163682](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10163682/) |
| 2024 | Mitigating Sociodemographic Bias in Opioid Use Disorder Prediction: Fairness-Aware Machine Learning Framework | JMIR AI | Proposes and tests a bias-mitigation algorithm on OUD prediction; reports 1.5-41.6% bias reduction across sex/race/income/marital-status subgroups depending on model | [PMC11372321](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11372321/) |
| 2024 | Fairness in Computational Innovations: Identifying Bias in Substance Use Treatment Length-of-Stay Prediction Models with Policy Implications | arXiv | Bias analysis specifically framed around downstream *policy* consequences, not just model metrics | [arXiv:2412.05832](https://arxiv.org/html/2412.05832v1) |
| 2024 | Measurement Bias in Machine Learning-Enhanced Opioid Risk Scoring Systems | preprint | Focuses specifically on *measurement* bias (how the label/feature itself encodes bias) rather than model-output bias — a distinct and often-overlooked bias source | [ResearchGate](https://www.researchgate.net/publication/385030640_Measurement_Bias_in_Machine_Learning-Enhanced_Opioid_Risk_Scoring_Systems) |
| 2025 | Evaluating the Impact of Data Biases on Algorithmic Fairness and Clinical Utility of Machine Learning Models for Prolonged Opioid Use Prediction | JAMIA Open | Explicitly separates *data* bias from *algorithmic* bias and measures both fairness and clinical utility jointly rather than fairness alone | [paper](https://academic.oup.com/jamiaopen/article/8/5/ooaf115/8269328) |
| — | Using Machine Learning to Advance Disparities Research: Subgroup Analyses of Access to Opioid Treatment | PMC | Subgroup-analysis methodology applied to treatment-access disparities | [PMC8928038](https://pmc.ncbi.nlm.nih.gov/articles/PMC8928038/) |

## C. General clinical-prediction fairness methodology (EHR-based, not drug-specific)

Useful for methodology (fairness metrics, mitigation techniques, how EHR data quality itself introduces bias) even though the prediction target isn't medication — directly transferable to auditing the `01-ehr-based` models.

| Year | Paper | Venue | Key idea | Link |
|---|---|---|---|---|
| 2023 | The Impact of Electronic Health Records (EHR) Data Continuity on Prediction Model Fairness and Racial-Ethnic Disparities | arXiv | Shows that *missingness/continuity patterns* in EHR data (which differ by race/insurance status) are themselves a bias source, independent of the model | [arXiv:2309.01935](https://arxiv.org/pdf/2309.01935) |
| 2023 | Detecting Algorithmic Bias in Medical-AI Models Using Trees | arXiv | Uses decision trees as an auditing/detection tool to surface where a black-box medical model's bias lives | [arXiv:2312.02959](https://arxiv.org/pdf/2312.02959) |
| 2024 | Equity in Healthcare: Analyzing Disparities in Machine Learning Predictions of Diabetic Patient Readmissions | arXiv | Case study of subgroup disparity in a chronic-disease prediction task structurally similar to medication recommendation | [arXiv:2403.19057](https://arxiv.org/html/2403.19057v1) |
| 2024 | Assessing Fairness in Machine Learning Models: A Study of Racial Bias Using Matched Counterparts in Mortality Prediction for Patients with Chronic Diseases | ScienceDirect | Matched-counterpart methodology for isolating racial bias from confounding severity differences | [paper](https://www.sciencedirect.com/science/article/abs/pii/S1532046424000959) |
| 2025 | Evaluating Algorithmic Bias in 30-Day Hospital Readmission Models: Retrospective Analysis | PMC | Retrospective bias audit of a widely-used readmission-risk model | [PMC11066744](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11066744/) |
| 2025 | Refocusing Algorithmic Fairness on Feature-Level Bias: A Diagnostic Approach Using Dutch EHR Data | medRxiv | Diagnoses *which features* drive unfairness rather than only measuring outcome-level disparity — useful diagnostic lens, and non-US (Dutch) data point | [paper](https://www.medrxiv.org/content/10.1101/2025.11.09.25339863.full.pdf) |
| 2026 | Multimodal Survival Modeling and Fairness-Aware Clinical Machine Learning for 5-Year Breast Cancer Risk Prediction | arXiv | Recent example of fairness constraints built directly into a multimodal clinical model's training objective, not bolted on after | [arXiv:2602.21648](https://arxiv.org/pdf/2602.21648) |

## D. LLM / clinical-NLP bias benchmarks

Relevant to [`04-llm-generative`](../04-llm-generative/README.md) — none of these target medication recommendation specifically, but several (CLIMB, EquityMedQA) include treatment-recommendation-adjacent prompts.

| Year | Paper | Venue | Key idea | Link |
|---|---|---|---|---|
| 2024 | A Toolbox for Surfacing Health Equity Harms and Biases in Large Language Models (EquityMedQA) | Nature Medicine | 7-dataset, 4,619-example adversarial benchmark; defines 6 dimensions of equity-related harm (inaccuracy across identity axes, lack of inclusion, stereotyping, omission of structural explanations, etc.) via participatory design with equity experts and physicians | [arXiv:2403.12025](https://arxiv.org/pdf/2403.12025) |
| 2024 | CLIMB: A Benchmark of Clinical Bias in Large Language Models | arXiv | Dedicated clinical-bias benchmark distinct from general-purpose LLM bias benchmarks | [arXiv:2407.05250](https://arxiv.org/pdf/2407.05250) |
| 2024 | Evaluation of Bias Towards Medical Professionals in Large Language Models | arXiv | GPT-4, Claude-3, Mistral-Large show significant gender/racial bias when evaluating *medical professionals* themselves — relevant if your system involves LLM-mediated clinician-facing output | [arXiv:2407.12031](https://arxiv.org/pdf/2407.12031) |
| 2025 | Evaluating and Addressing Demographic Disparities in Medical Large Language Models: A Systematic Review | Int'l J. for Equity in Health | 24 studies reviewed; 22 (91.7%) found bias — gender bias in 15/16 studies, racial/ethnic bias in 10/11 — the closest thing this thread has to a survey | [PMC11866893](https://pmc.ncbi.nlm.nih.gov/articles/PMC11866893/) |
| 2025 | Evaluating Bias in Retrieval-Augmented Medical Question-Answering Systems | arXiv | Bias specifically introduced/amplified by the *retrieval* step in medical RAG — directly relevant to the RAG architectures in `04-llm-generative` | [arXiv:2503.15454](https://arxiv.org/html/2503.15454v1) |
| 2025 | FairMedQA: Benchmarking Bias in Large Language Models for Medical Question Answering | arXiv | Another dedicated medical-QA fairness benchmark; worth comparing scope against CLIMB/EquityMedQA rather than treating as redundant | [arXiv:2505.19562](https://arxiv.org/pdf/2505.19562) |
| 2025 | Toward Revealing Nuanced Biases in Medical LLMs | arXiv | Argues coarse demographic-parity checks miss subtler, intersectional biases; proposes finer-grained analysis | [arXiv:2507.21176](https://arxiv.org/pdf/2507.21176) |
| 2025 | Dr. Bias: Social Disparities in AI-Powered Medical Guidance | arXiv | Focused on patient-facing medical guidance (closer to a patient-facing recommendation system than clinician-facing CDS) | [arXiv:2510.09162](https://arxiv.org/html/2510.09162) |
| 2026 | Race, Ethnicity and Their Implication on Bias in Large Language Models | arXiv | Focused specifically on race/ethnicity as the bias axis, across general and medical LLM use | [arXiv:2601.12868](https://arxiv.org/pdf/2601.12868) |

## E. Fairness-aware recommender-systems methodology (general, transferable)

Not healthcare-specific, but this is the methodological toolbox (fairness definitions, pre/in/post-processing mitigation) that a fairness-aware *medication* recommender would draw on — worth reading if you're designing a mitigation method rather than only auditing existing models.

| Year | Paper | Venue | Key idea | Link |
|---|---|---|---|---|
| 2022 | Fairness in Recommendation: Foundations, Methods and Applications | arXiv | General survey of fairness notions (individual, group, provider-side, consumer-side) in recommender systems | [arXiv:2205.13619](https://arxiv.org/pdf/2205.13619) |
| 2023 | A Survey on Fairness-Aware Recommender Systems | arXiv | Complementary survey, more focused on the pre-/in-/post-processing mitigation taxonomy | [arXiv:2306.00403](https://arxiv.org/pdf/2306.00403) |
| 2024 | Understanding Fairness in Recommender Systems: A Healthcare Perspective | RecSys '24 | The one entry in this section that *is* healthcare-specific: studies public understanding of fairness metrics (demographic parity, equal accuracy, equalized odds, PPV) in a healthcare-recommendation framing | [arXiv:2409.03893](https://arxiv.org/html/2409.03893v2) |

## Notes for later reading

- **The real gap is narrower than it first looked.** Fairness *is* well-studied for adjacent clinical-prediction tasks (readmission, mortality, opioid-use-disorder risk) and heavily studied for LLM medical QA — but a subgroup-broken-down fairness audit of the actual GAMENet/SafeDrug/COGNet-style combinatorial medication-recommendation task (from `01-ehr-based`) does not appear to exist yet in the literature searched. If your PhD contribution needs a fairness angle, this specific intersection — DDI-safety-constrained recommendation *and* demographic fairness, evaluated jointly — looks like genuine white space rather than a search artifact. Worth a second, more exhaustive search (including ACM FAccT and health-informatics venues directly) before concluding it's fully open.
- **Read Obermeyer et al. (2019) first regardless of angle** — it's the reference point nearly every other paper here either cites or structurally mirrors (proxy-variable bias via a cost/utilization stand-in for need). Understanding its mechanism makes the rest of section A-C easier to place.
- **Opioid-prescribing bias (section B) is the best proxy for "fairness in drug recommendation" available right now** — it's the one drug-adjacent task where subgroup fairness has actually been measured against ML predictions, even though it's a risk/eligibility prediction task rather than a combinatorial recommendation task.
- **Section C's methodology is directly reusable**: the EHR-continuity-as-bias-source finding (arXiv:2309.01935) and the matched-counterpart method both transfer cleanly to auditing `01-ehr-based` models on MIMIC, where data missingness/continuity is known to correlate with demographics.
- **Cross-reference with `04-llm-generative`**: the RAG-bias paper (arXiv:2503.15454) is a direct fairness lens on the RAG architectures already collected there (EHR-RAG, PACE-RAG, etc.) — read together.
