# Model Card — A-CUT TOPIQ-Lite Mixed112

## Model Details
- **Model Name**: A-CUT TOPIQ-Lite Mixed112 (`acut-topiq-mixed112`)
- **Developer**: Gwanjung Kim (A-CUT Mobile Photo Evaluation & Curation Capstone)
- **Architecture**: TOPIQ-Lite (`scripts/topiq_lite.py` & `scripts/topiq_rankcalib.py`): EfficientNetV2B0 multi-stage feature pyramid (`C2, C3, C4, C5`) with top-down semantic guidance and cross-scale attention pooling (`384×384` input).
- **Deployment Role**: Evaluated High-Correlation Technical IQA Candidate (SPAQ SRCC 0.899)

## Tensor Input / Output Contract
- **Input Contract**: RGB float32 `[1, 384, 384, 3]`, pixel scale `[0, 1]`
- **Output Contract**: Scalar technical quality score in `[0, 1]` (or `[0, 100]` after ×100 scaling)
- **Included Model Artifacts**:
  - `topiq_lite_mixed112_frozen_fp16.tflite (11.99 MB, SHA256: 19f4a9974dbf)`

## Intended Use
- Designed for on-device or offline photo quality and aesthetics evaluation within the A-CUT smartphone photo selection pipeline.
- Not intended as an uncalibrated standalone medical, forensic, or safety-critical classifier.

## Limitations & Audit Qualifications
- **Strong Smartphone Correlation**: Achieves `0.899` SRCC on SPAQ and `0.863` on KonIQ-10k inside a 12.0 MB FP16 TFLite bundle.
- **Why Not Standalone Production**: On FLIVE's extreme low-quality tail, standalone `topiq_lite_mixed112` exhibited 5 severe false positives unless paired with FLIVE/KonIQ safety guards.
