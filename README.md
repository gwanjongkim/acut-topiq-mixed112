# A-CUT TOPIQ Mixed112

#### A-CUT Capstone Project — Mobile Image Quality and Aesthetic Assessment

> TOPIQ-lite mixed112 model candidate for technical IQA.

## Introduction

TOPIQ-lite candidate model trained on the mixed112 dataset (SPAQ, KonIQ, FLIVE). It was evaluated for general technical quality assessment.

- **Role**: Candidate / log-only evidence.
- **Task**: Image Quality and Aesthetic Assessment.

## Model / Method

Based on TOPIQ-lite architecture. This repository contains the model export and parity evidence. It is not currently approved for production replacement but serves as a strong technical signal candidate.

- **Artifacts**: Inferred from scripts

## Dataset and Benchmark

- Benchmark results are summarized below. See `docs/benchmark_summary.md` for detailed per-dataset analysis.
- Note: Large datasets are excluded due to size/license constraints.

## Model Weights / Artifacts

- Due to size constraints, artifacts larger than 50MB are not included in this repository.
- Recommended hosting: GitHub Releases.
- See `models/download.md`.

## Repository Structure

```
.
├── configs/
├── docs/
├── models/
├── results/
├── scripts/
└── requirements.txt
```

## Requirements

Please refer to `requirements.txt`. Minimal dependencies include `torch`, `tensorflow`, `numpy`, and `pillow`.

## Quick Start

```bash
pip install -r requirements.txt
python scripts/test_tflite_parity.py --model_path models/model_files/topiq_lite_mixed112_frozen_fp16.tflite
```
*(Verify path assumptions in `docs/reproduction_notes.md`)*

## Results

| Dataset | Metric | Value | Evidence Path | Decision |
|---------|--------|-------|---------------|----------|
| Official Protocol | topiq_existing SRCC | 0.7975 | outputs/official_protocol_technical_signal_benchmark_20260604/report.md | Log-Only |
| SPAQ | SRCC | 0.899 | outputs/acut_capstone_final_report_20260526/model_metrics_summary.csv | Internal Benchmark |
| KonIQ | SRCC | 0.863 | outputs/acut_capstone_final_report_20260526/model_metrics_summary.csv | Internal Benchmark |

## Limitations

- Results are based on local reproduction and may not exactly match original papers.
- See `docs/model_card.md` for detailed limitations.

## Citation

```bibtex
@misc{acut_topiq_2026,
  title        = {A-CUT TOPIQ Mixed112: Mobile Image Quality and Aesthetic Assessment Model},
  author       = {Kim, Gwanjung},
  year         = {2026},
  note         = {Capstone project repository}
}
```
### Original References

- Chen, C., et al. (2023). TOPIQ: Text-to-image Quality Assessment with Progressive Interactive Queries. arXiv.

## Related Repositories

- [A-CUT Public Model Repositories](..)
