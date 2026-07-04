# Masked Emotion LoRA Benchmark

![Python](https://img.shields.io/badge/Python-3.10-blue)
![LoRA](https://img.shields.io/badge/LoRA-Adaptation-orange)
![Evaluation](https://img.shields.io/badge/Evaluation-Reproducible-green)
![LLMs](https://img.shields.io/badge/Models-RoBERTa%20%7C%20T5%20%7C%20LLaMA%20%7C%20Gemma-blueviolet)

Reproducible LoRA adaptation and evaluation benchmark for masked-emotion reasoning on the EXPRESS dataset. The project combines baseline reproduction, task-specific fine-tuning, continuation training, centralized metrics, and cross-family model comparison.

The goal is to measure how adaptation strategy, data handling, and evaluation discipline affect fine-grained model behavior, rather than treating model scale as the only lever.

---

## Key Results

- Best model (RoBERTa-large + continuation training):
  - **AccV = 0.8304**
- Paper baseline (Shu et al., 2025):
  - **AccV ≈ 0.377**
- Improvement:
  - **+0.45 absolute**
  - **>120% relative gain**

Main takeaway:
- Alignment + training strategy matter more than model size for this task.

## Why This Matters

This repo is packaged as an ML systems benchmark, not just a training notebook:

- consistent experiment registry and run naming
- repeatable baseline -> adaptation -> continuation -> comparison flow
- metrics and figures exported for review outside Jupyter
- model-family comparison across encoder and generative architectures
- clear evidence of evaluation-driven iteration

---

## What This Repo Does

- Reproduces baseline results from *Fluent but Unfeeling*
- Applies LoRA fine-tuning across:
  - Encoder models (RoBERTa, XLM-RoBERTa, Longformer)
  - Generative models (Flan-T5, LLaMA, Gemma)
- Introduces continuation training for large gains
- Tracks all experiments with centralized metrics and outputs
- Produces final comparison tables and figures used in the report

---

## Repository Layout

### Upstream Code (kept intact)
- `LLaMA-Factory/`
- `express-emotion-recognition/`

### Project Assets

- `notebooks/`
  - End-to-end experiment pipeline (baseline → LoRA → optimization → comparison)
- `configs/model_registry.yaml`
  - Central model configuration and tracking
- `outputs/`
  - `metrics/` – aggregated results and run summaries
  - `figures/` – plots used in final analysis
  - `lora_runs/` – adapter checkpoints and training states
  - `lora_data/` – processed datasets
- `docs/proposal/`
  - Project report and supporting tables

---

## Recommended Run Order

### 1. Baseline Reproduction
- `20_baseline_reproduction_runner.ipynb`
- `30_sanity_check_roberta_baseline.ipynb`

### 2. Model Family Pipelines
- `50` – `56`

### 3. RoBERTa Optimization (Core Work)
- `57`, `57b`, `57c`, `57d`
- `59` (continuation training)

### 4. Final Comparison
- `60_multi_model_comparison.ipynb`

---

## Notable Experiment Chain

Best-performing pipeline:

```
57c_final_full_rank64_noval_canonical
→ 59_continue_from_57c_final_e4_lr4e6
→ +20 epochs
→ +50 epochs (final)
```

This progression shows:
- initial LoRA gains (~0.59 AccV)
- large improvements from continuation training (~0.83 AccV)

---

## Insights

- Encoder models outperform generative models for masked prediction tasks
- LoRA consistently improves performance, but gains vary by architecture
- Continuation training is the largest driver of improvement
- Models capture general emotional tone well, but struggle with fine-grained distinctions
  - e.g., afraid vs scared, alone vs lonely

---

## Reporting

- Final tables and plots:
  - `notebooks/60_multi_model_comparison.ipynb`
- Report:
  - `docs/proposal/SMA_Project_Progress_Report.docx`
- Exported tables:
  - `docs/proposal/notebook60_tables.xlsx`

---

## Notes

- Notebook-driven workflow (configure paths in cells)
- Use consistent preprocessing and evaluation for fair comparison
