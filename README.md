# A-CUT TOPIQ-Lite Mixed112

> **A-CUT Top-Down Multi-Scale Technical IQA Candidate — TOPIQ-Lite Trained on Mixed SPAQ/KonIQ/FLIVE (TFLite FP16)**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](./LICENSE)
[![Project: A-CUT](https://img.shields.io/badge/Project-A--CUT%20Capstone-success.svg)](https://github.com/gwanjongkim/photo_score_project)

## 1. Overview

- **Role in A-CUT**: Evaluated High-Correlation Technical IQA Candidate (SPAQ SRCC 0.899)
- **Task**: Multi-Scale No-Reference Technical Image Quality Assessment (NR-IQA)
- **Architecture**: TOPIQ-Lite (`scripts/topiq_lite.py` & `scripts/topiq_rankcalib.py`): EfficientNetV2B0 multi-stage feature pyramid (`C2, C3, C4, C5`) with top-down semantic guidance and cross-scale attention pooling (`384×384` input).

## 2. Input / Output Contract & Model Artifacts

- **Input Contract**: RGB float32 `[1, 384, 384, 3]`, pixel scale `[0, 1]`
- **Output Contract**: Scalar technical quality score in `[0, 1]` (or `[0, 100]` after ×100 scaling)
- **Model Files (`models/model_files/` & Releases)**:
  - `topiq_lite_mixed112_frozen_fp16.tflite (11.99 MB, SHA256: 19f4a9974dbf)`

## 3. Benchmark Results

| Dataset | Metric | Value | Notes |
| :--- | :---: | :---: | :--- |
| SPAQ | SRCC | **0.8990** | Smartphone photography benchmark |
| KonIQ-10k | SRCC | **0.8630** | In-the-wild authenticity benchmark |
| Official 4,967-Image Protocol | Overall SRCC | **0.7975** (0.8148 unweighted) | Strong global ranking; 5 severe FP on FLIVE tail |

## 4. Key Engineering Notes & 2026 Audit Findings

- **Strong Smartphone Correlation**: Achieves `0.899` SRCC on SPAQ and `0.863` on KonIQ-10k inside a 12.0 MB FP16 TFLite bundle.
- **Why Not Standalone Production**: On FLIVE's extreme low-quality tail, standalone `topiq_lite_mixed112` exhibited 5 severe false positives unless paired with FLIVE/KonIQ safety guards.

## 5. Quick Start

```bash
pip install -r requirements.txt
python scripts/train_topiq_lite.py --help
python scripts/export_topiq_lite_ranking_lam01.py --help
```

For full documentation, see:
- [`docs/model_card.md`](./docs/model_card.md) — Architecture, tensor contracts, and limitations
- [`docs/benchmark_summary.md`](./docs/benchmark_summary.md) — Detailed metrics and dataset evaluations
- [`docs/reproduction_notes.md`](./docs/reproduction_notes.md) — Environment and reproduction guide
- [`models/download.md`](./models/download.md) — Model binary hashes and download notes

## 6. A-CUT Ecosystem Repositories

| Repository | Dimension | Role / Status | Key Metric |
| :--- | :---: | :--- | :--- |
| [acut-nima-mobile](https://github.com/gwanjongkim/acut-nima-mobile) | Aesthetic (IAA) | **Production Ensemble (0.40)** | AVA SRCC `0.5894`, AUC `0.8018` |
| [acut-rgnet-mobile](https://github.com/gwanjongkim/acut-rgnet-mobile) | Aesthetic (IAA) | **Production Ensemble (0.45)** | AADB SRCC `0.6819` (FP16 `0.6648`) |
| [acut-mobile-alamp](https://github.com/gwanjongkim/acut-mobile-alamp) | Aesthetic (IAA) | **Production Ensemble (0.15)** | AVA Acc `0.7633`, AUC `0.7877` |
| [acut-icaa-color-aesthetics](https://github.com/gwanjongkim/acut-icaa-color-aesthetics) | Color Aesthetics | **Verified TF-Native Port** | ICAA17K Color SRCC `0.8791`, MOS `0.9058` |
| [acut-koniq-flive-technical-iqa](https://github.com/gwanjongkim/acut-koniq-flive-technical-iqa) | Technical (IQA) | **Production Baseline (4/7 + 3/7)** | Official SRCC `0.7168` (`0.7958` recon), `0` Severe FP |
| [acut-technical-iqa](https://github.com/gwanjongkim/acut-technical-iqa) | Technical (IQA) | **Umbrella Benchmark** | 4,967-Image Official Protocol Suite |
| [acut-topiq-mixed112](https://github.com/gwanjongkim/acut-topiq-mixed112) | Technical (IQA) | **Evaluated Candidate** | SPAQ SRCC `0.8990`, KonIQ `0.8630` |
| [acut-topiq-flive-hybrid](https://github.com/gwanjongkim/acut-topiq-flive-hybrid) | Technical (IQA) | **Best Log-Only Shadow (60/40)** | Official SRCC `0.8069`, MAE `5.04` |
| [acut-c6-topiq-koniq](https://github.com/gwanjongkim/acut-c6-topiq-koniq) | Technical (IQA) | **Negative Result (Rejected)** | Official SRCC `0.7314`, MAE `15.39` |
| [acut-mdiqa-benchmark](https://github.com/gwanjongkim/acut-mdiqa-benchmark) | Technical (IQA) | **Teacher Ceiling Reference** | KonIQ SRCC `0.9464`, SPAQ `0.9136` |
| [acut-musiq-probe](https://github.com/gwanjongkim/acut-musiq-probe) | Technical (IQA) | **Reference & Probe Study** | Official SPAQ `0.9460`, KonIQ `0.9275` |
| [acut-student-iqa](https://github.com/gwanjongkim/acut-student-iqa) | Technical (IQA) | **Distillation Study (No-Go)** | 14k Student SRCC `0.7436`, SPAQ `0.8984` |
| [photo_score_project](https://github.com/gwanjongkim/photo_score_project) | Full Monorepo | **Core Research Workspace** | Complete Training, Audit & Pipeline Code |

## 7. References & Citation

- Chen, C., Mo, J., Hou, J., Wu, H., Liao, L., Sun, W., Yan, Q., & Lin, W. (2024). *TOPIQ: A Top-Down Approach from Semantics to Distortions for Image Quality Assessment*. IEEE Transactions on Image Processing, 33, 2404–2418.

```bibtex
@misc{acut_topiq_mixed112_2026,
  title        = {A-CUT TOPIQ-Lite Mixed112: A-CUT Top-Down Multi-Scale Technical IQA Candidate — TOPIQ-Lite Trained on Mixed SPAQ/KonIQ/FLIVE (TFLite FP16)},
  author       = {Kim, Gwanjung},
  year         = {2026},
  howpublished = {\url{https://github.com/gwanjongkim/acut-topiq-mixed112}}
}
```
