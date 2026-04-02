# Project Layout

This workspace keeps upstream codebases intact while placing your team workflow assets at top level.

## Upstream Repos (unchanged)
- `LLaMA-Factory/`
- `express-emotion-recognition/`

## Team Workspace
- `notebooks/`
  - `10_project_index.ipynb`
  - `20_baseline_reproduction_runner.ipynb`
  - `30_sanity_check_roberta_baseline.ipynb`
  - `50_roberta_mlm_lora_template.ipynb`
  - `51_mental_roberta_mlm_lora.ipynb`
  - `52_flan_seq2seq_lora.ipynb`
  - `53_llama31_8b_lora_pipeline.ipynb`
  - `54_gemma2_2b_lora_pipeline.ipynb`
  - `60_multi_model_comparison.ipynb`
- `notebooks/archive/`
  - archived utility notebooks
- `configs/model_registry.yaml` (includes Gemma, Llama, Flan, RoBERTa variants)
- `docs/`
  - `proposal/SMA Final Project Proposal.docx`
  - `papers/fluent_but_unfeeling.pdf`
- `outputs/`
  - `figures/`
  - `metrics/`
- `archive/legacy/`
  - archived top-level legacy artifacts and old configs

## Note
- Active notebooks are run from `notebooks/`.

## Some Preliminary Results

9% improvement on top model from baseline results

<img width="1384" height="584" alt="image" src="https://github.com/user-attachments/assets/32422ec5-3fca-4184-b19e-29a33f3b630a" />

<img width="1349" height="745" alt="image" src="https://github.com/user-attachments/assets/947ee392-3d9b-4770-b540-9f622caa616b" />

