# Benchmark Summary — A-CUT TOPIQ-Lite Mixed112

## Overview
- **Repository**: `acut-topiq-mixed112`
- **Role in A-CUT**: Evaluated High-Correlation Technical IQA Candidate (SPAQ SRCC 0.899)
- **Task**: Multi-Scale No-Reference Technical Image Quality Assessment (NR-IQA)

## Evaluated Metrics

| Dataset | Metric | Value | Notes |
| :--- | :---: | :---: | :--- |
| SPAQ | SRCC | **0.8990** | Smartphone photography benchmark |
| KonIQ-10k | SRCC | **0.8630** | In-the-wild authenticity benchmark |
| Official 4,967-Image Protocol | Overall SRCC | **0.7975** (0.8148 unweighted) | Strong global ranking; 5 severe FP on FLIVE tail |

## Key Engineering & Audit Findings

- **Strong Smartphone Correlation**: Achieves `0.899` SRCC on SPAQ and `0.863` on KonIQ-10k inside a 12.0 MB FP16 TFLite bundle.
- **Why Not Standalone Production**: On FLIVE's extreme low-quality tail, standalone `topiq_lite_mixed112` exhibited 5 severe false positives unless paired with FLIVE/KonIQ safety guards.

## Evidence Files in `results/`
All metric tables, per-sample predictions, parity checks, and audit reports backing the numbers above are stored directly in the [`results/`](../results/) directory of this repository.
