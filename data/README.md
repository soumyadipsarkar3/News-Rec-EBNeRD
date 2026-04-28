# Data placement (not tracked in git)

This repository **does not** include EB-NeRD files due to size/licensing. Download the dataset from the RecSys Challenge page and place it as described below.

## Download

- Official source: `https://recsys.acm.org/recsys24/challenge/`

## Expected paths

### Option A (Google Colab)

- Upload the parquet to: `/content/behaviors.parquet`

### Option B (local)

- Place the file at:

```text
data/train/behaviors.parquet
```

Create folders if needed:

```bash
mkdir -p data/train
```

## Cleaning note used in the analysis

- Remove reads with **read time < 5 seconds** (about **2.7%** of raw data).

## Important

- Do not commit dataset files. The repo’s `.gitignore` excludes everything under `data/` except this `README.md`.
