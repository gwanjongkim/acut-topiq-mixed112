# Reproduction & Execution Notes — A-CUT TOPIQ-Lite Mixed112

## Environment Setup
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
```

## Available Scripts (`scripts/`)
```bash
python scripts/train_topiq_lite.py --help
python scripts/export_topiq_lite_ranking_lam01.py --help
```

## Preprocessing & Parity Verification
- **Input Specification**: RGB float32 `[1, 384, 384, 3]`, pixel scale `[0, 1]`
- **Output Specification**: Scalar technical quality score in `[0, 1]` (or `[0, 100]` after ×100 scaling)
- Ensure EXIF orientation transposition (`ImageOps.exif_transpose`) is applied prior to resizing so portrait smartphone photos are not evaluated rotated.
