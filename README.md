# Masked Emotion LoRA Benchmark

Benchmarking and improving masked-emotion prediction on EXPRESS using baseline reproduction plus LoRA fine-tuning across model families.

## Repository Layout

### Upstream Code (kept intact)
- `LLaMA-Factory/`
- `express-emotion-recognition/`

### Project Assets
- `notebooks/`:
  - `20_baseline_reproduction_runner.ipynb`
  - `30_sanity_check_roberta_baseline.ipynb`
  - `50_roberta_mlm_lora_template.ipynb`
  - `51_mental_roberta_mlm_lora.ipynb`
  - `52_flan_seq2seq_lora.ipynb`
  - `53_llama31_8b_lora_pipeline.ipynb`
  - `54_gemma2_2b_lora_pipeline.ipynb`
  - `55_longformer_mlm_lora.ipynb`
  - `56_gpt_causal_lora.ipynb`
  - `57_roberta_mlm_lora_improvement.ipynb`
  - `57b_roberta_large_mlm_lora_improvement.ipynb`
  - `57c_roberta_large_mlm_lora_hparam_push.ipynb`
  - `57d_xlm_roberta_large_mlm_lora_hparam_push.ipynb`
  - `58_roberta_mlm_lora_ppo.ipynb`
  - `59_roberta_large_continue_from_57c.ipynb`
  - `60_multi_model_comparison.ipynb`
- `configs/model_registry.yaml`
- `outputs/`:
  - `metrics/` (central CSV metrics and per-model run summaries)
  - `figures/` (comparison and overlay plots)
  - `lora_runs/` (adapter checkpoints and trainer states)
  - `lora_data/` (prepared training/eval data)
- `docs/proposal/`:
  - proposal and report docs
  - `SMA_Project_Progress_Report.docx`
  - `notebook60_tables.xlsx`

## Recommended Run Order

1. Run baseline:
   - `20_baseline_reproduction_runner.ipynb`
   - `30_sanity_check_roberta_baseline.ipynb`
2. Run family pipelines:
   - `50` to `56`
3. Run focused RoBERTa optimization:
   - `57`, `57b`, `57c`, `57d`, `59`
4. Run final comparison/report notebook:
   - `60_multi_model_comparison.ipynb`

## Current Status Snapshot

- Baselines reproduced under the shared evaluation pipeline.
- LoRA pipelines implemented for RoBERTa, Mental-RoBERTa, Flan-T5 variants, Llama3.1, Gemma2, and Longformer tracks.
- Best observed run (latest metrics): `roberta_large_59_continue_from_57c_final_e4_lr4e6_plus20e_plus50e_r2` with `AccV = 0.830411` and `AccV-2 = 0.960717`.
- Authors' best baseline from paper setup is approximately `AccV = 0.377345`.
- Absolute gain (AccV): `+0.453066` (about `+120.1%` relative).
- RoBERTa continuation chain used for transfer learning:
  - `57c_final_full_rank64_noval_canonical` -> `59_continue_from_57c_final_e4_lr4e6` -> `...plus20e` -> `...plus20e_plus50e_r2`

## Reporting Assets

- Final multi-model charts/tables are produced in notebook `60`.
- Proposal-aligned progress report:
  - `docs/proposal/SMA_Project_Progress_Report.docx`
- Excel export of notebook 60 tables:
  - `docs/proposal/notebook60_tables.xlsx`

## Notes

- This repo is notebook-driven; use notebook cell config blocks for GPU/model/cache paths.
- Keep evaluation apples-to-apples by using the same cleaning and metric scripts across all runs.
