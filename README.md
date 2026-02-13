# News Recommendation Analysis with EB-NeRD  
**CSCE 676: Data Mining — Spring 2026**  
**Checkpoint 1 — Dataset Selection + Exploratory Data Analysis (EDA)**

This repository contains the work for **Checkpoint 1** of the course project.  
The goal of this checkpoint is to understand the **EB-NeRD** dataset and extract insights that affect **news recommendation** (bias, user behavior, engagement, and temporal patterns).

---

## Table of Contents
- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Repository Structure](#repository-structure)
- [Setup](#setup)
- [How to Run](#how-to-run)
- [Figures Gallery (Quick View)](#figures-gallery-quick-view)
- [EDA Results (with Figures)](#eda-results-with-figures)
- [Key Findings Summary](#key-findings-summary)
- [Notes / Assumptions](#notes--assumptions)
- [Next Steps](#next-steps)
- [Citation](#citation)

---

## Project Overview
News recommendation is challenging because:
- clicks follow a **long-tail / popularity bias**,
- many users have little history (**cold start**),
- engagement feedback (read time, scroll depth) is **skewed**,
- user activity changes over time (**temporal effects**).

In this checkpoint, we run EDA on EB-NeRD to quantify these issues and prepare for building recommenders in later checkpoints.

---

## Dataset
**Dataset:** EB-NeRD (Ekstra Bladet News Recommendation Dataset)

### Expected path used in notebook
Place the dataset parquet file here (same path assumed in the notebook):

```text
data/train/behaviors.parquet
```
Note: The dataset is not included in this repo due to size / licensing constraints.

### Download instructions
1. Download EB-NeRD from the official source provided by the authors / course.
2. Unzip it locally.
3. Create the folder structure:
   ```
   data/
   └── train/
       └── behaviors.parquet
   ```
4. Run the notebook.

---

## Repository Structure
```
.
├── Project Checkpoint 1.ipynb
├── README.md
└── assets/
    └── figures/
        ├── popularity_longtail.png
        ├── daily_interaction_volume.png
        ├── user_activity_clicks_per_user.png
        ├── read_time_distribution.png
        └── scroll_depth_distribution.png
```

---

## Setup
### Option A: Quick install (minimum)
```bash
pip install pandas numpy matplotlib seaborn pyarrow
```

### Option B: Recommended (virtual environment)
```bash
python -m venv .venv
source .venv/bin/activate     # Windows: .venv\Scripts\activate
pip install pandas numpy matplotlib seaborn pyarrow
```

---

## How to Run

### Google Colab
1. Upload the dataset file into the Colab workspace so it exists at: `data/train/behaviors.parquet`
2. Open `Project Checkpoint 1.ipynb`
3. Run all cells from top to bottom.

### Local (Jupyter)
```bash
pip install notebook
jupyter notebook
```
Open `Project Checkpoint 1.ipynb` and run all cells.

---

## Figures Gallery (Quick View)
These are the figures generated from the EDA notebook.

<p float="left">
  <img src="assets/figures/popularity_longtail.png" width="400" />
  <img src="assets/figures/daily_interaction_volume.png" width="400" /> 
  <img src="assets/figures/user_activity_clicks_per_user.png" width="400" />
  <img src="assets/figures/read_time_distribution.png" width="400" />
  <img src="assets/figures/scroll_depth_distribution.png" width="400" />
</p>

---

## EDA Results (with Figures)

### 1) Article Popularity Distribution (Long Tail Evidence)
**What this shows:** Clicks are highly concentrated on a small set of articles.  
**Why it matters:** Simple popularity-based baselines can dominate, and models can become biased toward already-popular items.

### 2) Daily Interaction Volume
**What this shows:** Daily click activity varies across dates.  
**Why it matters:** Train/validation/test splits should be time-based and temporal signals (recency) can help.

### 3) Distribution of User Activity (Clicks per User)
**What this shows:** Most users have low click counts while a small number are highly active.  
**Why it matters:** Cold-start users require special handling (popular/recency baselines, hybrid methods).

### 4) Engagement Signals: Read Time
**What this shows:** Read times are skewed; many sessions are short, with a long tail of longer reads.  
**Why it matters:** Read time can be used as an implicit feedback signal (weighting clicks by engagement).

### 5) Engagement Signals: Scroll Depth
**What this shows:** Scroll depth provides another implicit engagement proxy (how much the user consumed).  
**Why it matters:** Can be used to filter low-quality interactions or weight training examples.

---

## Key Findings Summary
- **Popularity Bias:** Strong long-tail behavior in clicks (few articles dominate).
- **User Activity:** Many users have little history → cold-start is significant.
- **Engagement:** Read-time and scroll-depth distributions are skewed but useful for implicit feedback.
- **Temporal Effects:** Daily interaction volume varies → time-based evaluation is important.

---

## Notes / Assumptions
- Dataset files are not committed to GitHub.
- All figures are generated from the EDA notebook and stored in `assets/figures/`.
- Some columns may contain missing values; cleaning decisions are documented in the notebook.

---

## Next Steps
- Implement baselines: MostPopular, Recency
- Use time-based splits for evaluation
- Evaluate with ranking metrics: NDCG@K, HR@K, MRR
- Explore debiasing / reranking strategies to reduce popularity bias

---

## Citation
If you use EB-NeRD, cite the dataset / paper according to course and dataset author requirements.
