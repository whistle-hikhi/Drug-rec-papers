# LLM / Generative Approaches to Medication Recommendation

The newest and fastest-moving of the four areas. Split into two parts below: **architectures & methods** (how the recommendation is actually produced) and **benchmarks & safety evaluation** (how well it's trusted). The architecture side was thin in the initial pass — this update (2026-08-19) fills it in with four identifiable sub-threads: agentic/multi-agent systems, retrieval-augmented generation, fine-tuning/alignment, and KG-LLM fusion.

## Architectures & Methods

### Agentic / multi-agent

| Year | Paper | Venue | Key idea | Link |
|---|---|---|---|---|
| 2024 | EHRAgent: Code Empowers LLMs for Few-shot Complex Tabular Reasoning on EHRs | EMNLP | Foundational EHR agent (not drug-rec-specific): LLM writes and executes code against tabular EHR data, learns from execution feedback, keeps a long-term memory of successful cases | [arXiv:2401.07128](https://arxiv.org/abs/2401.07128) |
| 2025 | Learning to Be A Doctor: Searching for Effective Medical Agent Architectures | arXiv | Treats "which agent architecture" as a search problem over the space of tool-use/planning/memory designs for clinical tasks, rather than hand-designing one | [arXiv:2504.11301](https://arxiv.org/html/2504.11301) |
| 2026 | SafeRx-Agent: A Knowledge-Grounded Multi-Agent Framework for Safe and Explainable Medication Recommendation | arXiv | Multi-agent pipeline grounded in external knowledge; first to target fine-grained (4th-level ATC code) medication generation with explicit safety/explainability roles split across agents | [arXiv:2605.29146](https://arxiv.org/html/2605.29146) |
| 2026 | ClinicalAgents: Multi-Agent Orchestration for Clinical Decision Making with Dual-Memory | arXiv | Orchestrates multiple specialized agents with a dual (short/long-term) memory architecture for clinical decisions, prescribing included | [arXiv:2603.26182](https://arxiv.org/html/2603.26182v1) |
| 2026 | TheraAgent: Self-Improving Therapeutic Agent for Precise and Comprehensive Treatment Planning | arXiv | Self-improving loop (agent critiques/refines its own treatment plans) rather than a static single-pass pipeline | [arXiv:2605.05963](https://arxiv.org/pdf/2605.05963) |

### Retrieval-augmented generation (RAG)

| Year | Paper | Venue | Key idea | Link |
|---|---|---|---|---|
| 2025 | Med-R²: Crafting Trustworthy LLM Physicians via Retrieval and Reasoning of Evidence-Based Medicine | arXiv | Couples retrieval with an explicit evidence-based-medicine reasoning process rather than retrieval as a bolt-on to generation | [arXiv:2501.11885](https://arxiv.org/pdf/2501.11885) |
| 2025 | Retrieval-Augmented Framework for LLM-Based Clinical Decision Support | arXiv | General RAG pipeline harmonizing unstructured clinical narrative + codified data for CDS inference | [arXiv:2510.01363](https://arxiv.org/abs/2510.01363) |
| 2025 | Retrieval Augmented LLM System for Comprehensive Drug Contraindications | arXiv | RAG specifically scoped to contraindication retrieval — a narrower, safety-critical sub-task of full recommendation | [arXiv:2508.06145](https://arxiv.org/pdf/2508.06145) |
| 2026 | EHR-RAG: Bridging Long-Horizon Structured EHR and LLMs via Enhanced RAG | arXiv | Addresses the specific problem of retrieving from *long-horizon structured* EHR (many visits over years), not just short unstructured notes | [arXiv:2601.21340](https://arxiv.org/pdf/2601.21340) |
| 2026 | A Hybrid Knowledge-Grounded Framework for Safety and Traceability in Prescription Verification | arXiv | Combines retrieval grounding with explicit traceability output — verifies a *given* prescription rather than generating one from scratch | [arXiv:2603.10891](https://arxiv.org/html/2603.10891) |
| 2026 | PACE-RAG: Patient-Aware Contextual and Evidence-Constrained RAG for Clinical Drug Recommendation | arXiv | RAG constrained jointly by patient context and clinical evidence, aimed at reducing hallucinated recommendations | [arXiv:2603.17356](https://arxiv.org/pdf/2603.17356) |

### Fine-tuning, alignment & distillation

| Year | Paper | Venue | Key idea | Link |
|---|---|---|---|---|
| 2023 | When MOE Meets LLMs: Parameter-Efficient Fine-Tuning for Multi-Task Medical Applications | arXiv | Mixture-of-experts + PEFT so one backbone LLM serves multiple medical tasks (medication rec among them) without full fine-tuning per task | [arXiv:2310.18339](https://arxiv.org/pdf/2310.18339) |
| 2024 | Large Language Model Distilling Medication Recommendation Model | arXiv | Distills LLM medical knowledge into a lightweight EHR-based recommendation model rather than using the LLM directly at inference | [arXiv:2402.02803](https://arxiv.org/pdf/2402.02803) |
| 2024 | Enhancing Medication Recommendation with LLM Text Representation | arXiv | Uses LLM-derived text embeddings of clinical notes as an additional feature stream feeding a conventional recommender | [arXiv:2407.10453](https://arxiv.org/abs/2407.10453) |
| 2024 | Med-Pal: Lightweight Large Language Model for Medication Enquiry | arXiv | Small, instruction-tuned model purpose-built for medication Q&A rather than a general-purpose LLM — efficiency-focused architecture choice | [arXiv:2407.12822](https://arxiv.org/pdf/2407.12822) |
| 2024 | A Contrastive Pretrain Model with Prompt Tuning for Multi-Center Medication Recommendation | arXiv | Contrastive pretraining + prompt tuning to generalize across multiple hospitals/EHR systems (a cross-site generalization architecture) | [arXiv:2412.20040](https://arxiv.org/pdf/2412.20040) |
| 2025 | KEDRec-LM: A Knowledge-Distilled Explainable Drug Recommendation Large Language Model | arXiv | Distills KG knowledge into an LLM for recommendation, targeting explainability | [arXiv:2502.20350](https://arxiv.org/html/2502.20350) |
| 2025 | Fine-Grained Alignment of LLMs for General Medication Recommendation without Overprescription | arXiv | LLaMA-2-7B backbone with instruction-tuning specifically penalizing overprescription (too many drugs), not just wrong drugs | [arXiv:2503.03687](https://arxiv.org/pdf/2503.03687) |
| 2025 | Multi-LLM Collaboration for Medication Recommendation | arXiv | Multiple LLMs collaborate (ensemble/debate-style) guided by explicit interaction modeling, rather than one model deciding alone | [arXiv:2512.05066](https://arxiv.org/html/2512.05066v1) |
| 2025 | FLAME: Fine-Grained List-Wise Alignment for Generative Medication Recommendation | NeurIPS | Reframes prescription generation as a sequential drug-by-drug decision process; step-wise GRPO with potential-based reward shaping to explicitly model DDIs per-step | [arXiv:2505.20218](https://arxiv.org/pdf/2505.20218) |
| 2026 | Improving Rare Medication Recommendation with Counterfactual Data Augmentation and LLMs | arXiv | Uses an LLM to generate counterfactual training examples targeting the long-tail/rare-drug problem classical EHR models struggle with | [arXiv:2607.24829](https://arxiv.org/html/2607.24829v1) |

### Knowledge-graph / LLM fusion

| Year | Paper | Venue | Key idea | Link |
|---|---|---|---|---|
| 2025 | DKG-LLM: Dynamic Knowledge Graph and LLM Integration for Diagnosis and Personalized Treatment Recommendations | arXiv | Dynamically *builds* a KG from heterogeneous clinical text + literature at inference time (rather than using a static pre-built KG like Hetionet/DRKG) before recommending | [arXiv:2508.06186](https://arxiv.org/abs/2508.06186) |
| 2025 | Knowledge-Guided LLM for Automatic Pediatric Dental Record Understanding and Safe Antibiotic Recommendation | arXiv | Hybrid: foundation LLM augmented by both retrieval *and* embedding fusion over a domain KG (UMLS/SNOMED-CT/DrugBank + dosage guidelines) | [arXiv:2512.09127](https://arxiv.org/pdf/2512.09127) |
| 2025 | Chinese Discharge Drug Recommendation in Metabolic Diseases with Large Language Models | arXiv | Domain- and language-specific (Chinese, metabolic disease) LLM recommendation system — useful as a non-English/non-MIMIC data point | [arXiv:2510.21084](https://arxiv.org/pdf/2510.21084) |

## Benchmarks & Safety Evaluation

| Year | Paper | Venue | Key idea | Link |
|---|---|---|---|---|
| 2024 | Development and Testing of a Novel LLM-Based Clinical Decision Support System for Medication Safety in 12 Clinical Specialties | arXiv | RAG-based CDS framework evaluated on real prescribing-error scenarios | [arXiv:2402.01741](https://arxiv.org/pdf/2402.01741) |
| 2025 | Large Language Model as Clinical Decision Support System Augments Medication Safety in 16 Clinical Specialties | Cell Reports Medicine | Extension of the 12-specialty study; co-pilot mode raised serious-harm error detection accuracy ~1.5x over pharmacists alone (61% accuracy in co-pilot mode) | [paper](https://www.cell.com/cell-reports-medicine/fulltext/S2666-3791(25)00396-9) |
| 2025 | Rx-LLM: A Benchmarking Suite to Evaluate Safe LLM Performance for Medication-Related Tasks | medRxiv/PMC | Benchmark suite specifically targeting *safety* of LLM medication-related outputs | [PMC12704647](https://pmc.ncbi.nlm.nih.gov/articles/PMC12704647/) |
| 2025 | A Real-World Evaluation of LLM Medication Safety Reviews in NHS Primary Care | arXiv | Deployment-style evaluation in a real primary-care setting rather than a synthetic benchmark | [arXiv:2512.21127](https://arxiv.org/pdf/2512.21127) |
| 2026 | Agentic AI in Healthcare & Medicine: A Seven-Dimensional Taxonomy for Empirical Evaluation of LLM-Based Agents | arXiv | Not a benchmark itself but a **taxonomy for evaluating** agent architectures (incl. prescribing) — useful lens for organizing the agentic papers above | [arXiv:2602.04813](https://arxiv.org/html/2602.04813v1) |
| 2026 | RxEval: A Prescription-Level Benchmark for Evaluating LLM Medication Recommendation | arXiv | Multiple-choice benchmark over real patient trajectories with reasoning-chain-perturbed distractors — more rigorous than free-text eval | [arXiv:2605.14543](https://arxiv.org/pdf/2605.14543) |

## Notes for later reading
- **The architecture gap is now much better covered** (2026-08-19 update): four distinct threads — agentic/multi-agent, RAG, fine-tuning/alignment, KG-LLM fusion — each with multiple 2025-2026 entries. FLAME and SafeRx-Agent are probably the strongest "read first" picks: both explicitly target DDI-safety the same way GAMENet/SafeDrug did for the classical EHR models, so they're the clearest bridge to `01-ehr-based`.
- **Cross-reference with `01-ehr-based`**: the distillation/fusion papers (LLM-distilling-medrec, KEDRec-LM, contrastive-pretrain-prompt-tuning) are explicitly trying to combine this thread with the classical GAMENet/SafeDrug lineage.
- **Still largely absent**: head-to-head Jaccard/DDI-rate comparisons against the classical EHR-based models on the *same* MIMIC splits. FLAME and SafeRx-Agent look closest to reporting this — worth checking their tables directly before assuming it's still a gap.
- **Agentic vs. RAG vs. fine-tuning is not a clean split in practice** — several papers combine two of the three (e.g. ClinicalAgents uses retrieval within an agent loop, DKG-LLM builds a KG then an agent reasons over it). The categorization above is by primary framing, not exclusive membership.
- The Seven-Dimensional Taxonomy paper (2602.04813) is worth reading early, similar to how the survey papers in the top-level README anchor the other three sub-areas — it's the closest thing this thread has to a survey.
