# EB-NeRD News Recommendation: From Behavior Mining to Robust Recommenders

I’m building a news recommender pipeline on **EB‑NeRD** to answer a practical question: *how do we make recommendations that work in the real world—where attention is scarce, popularity dominates, and many users have almost no history?* This repo contains my **CSCE 676 (Data Mining), Spring 2026** project work and checkpoints.

- **Main notebook (final deliverable)**: `main_notebook.ipynb` *(placeholder — coming soon; not pushed yet)*
- **Checkpoint 2 notebook**: `checkpoint_2.ipynb`
- **Checkpoint 1 notebook**: `checkpoint_1.ipynb`
- **Video demo**: **[YouTube video link — to be added]**

## Headline results (so far)

- **11.7M** cleaned interactions across **787K** users
- **44.1%** of sessions contain **multi‑article sequences**
- **19.1%** of users are **cold‑start** \((<3 clicks)\)
- **K‑means** found **5** user tiers with **silhouette = 0.58**
- **Gini = 0.69**, indicating **strong popularity bias**

## Research questions

News recommendation looks deceptively simple—rank articles by clicks—but that quickly collapses into a popularity-only system. My first question is: **how severe is popularity bias in EB‑NeRD, and how does it shape what “good recommendations” even mean?** Quantifying the long tail and concentration (e.g., Gini) is foundational for choosing baselines and evaluation strategies.

Second, news is consumed in **bursts and sequences**, not as isolated clicks. So I ask: **how often do sessions contain meaningful multi-article behavior, and can we treat those sequences as a signal for next‑item recommendation?** If a large fraction of sessions have multi‑step reading trails, sequential models and pattern mining become relevant—not just matrix factorization.

Third, I’m interested in product realism: **how do we handle cold-start users and heterogeneous engagement levels?** In practice, many users have tiny histories, while a smaller set drives most interactions. Segmenting users into tiers and measuring cold-start prevalence guides which models are feasible (content-first, recency, popularity-with-constraints, hybrid methods).

## Quick visuals (from Checkpoint 1 EDA)

![Popularity long tail](assets/figures/popularity_longtail.png)

![User activity distribution](assets/figures/user_activity_clicks_per_user.png)

## Dataset (EB‑NeRD)

- **Dataset**: EB‑NeRD (Ekstra Bladet News Recommendation Dataset)
- **Download**: `https://recsys.acm.org/recsys24/challenge/`
- **Scale (current pipeline)**: **11.7M** cleaned interactions, **787K** users
- **Cleaning rule**: remove reads with **read time < 5 seconds** (about **2.7%** of raw data)

### Data placement (required)

- **Colab**: upload to `/content/behaviors.parquet`
- **Local**: place at `data/train/behaviors.parquet`

See `data/README.md` for the exact expected layout.

## How to reproduce (Google Colab)

1. Open the notebook you want to run in Colab:
   - `checkpoint_2.ipynb` (Checkpoint 2), or
   - `checkpoint_1.ipynb` (Checkpoint 1)
2. Upload the dataset parquet to Colab so it exists at:
   - `/content/behaviors.parquet`
3. Install dependencies (either via `pip install -r requirements.txt` after you populate it, or direct installs).
4. Run all cells top-to-bottom.

## Key dependencies

This project targets:

- **Python**: 3.11
- **Core**: `pandas` 2.x, `scikit-learn` 1.x
- **Pattern mining / utilities**: `mlxtend`, `prefixspan`
- **Deep learning**: `torch` 2.x

*(Pinned versions will be added after freezing the environment into `requirements.txt`.)*

## Repo structure (current + planned)

```text
.
├── checkpoint_1.ipynb
├── checkpoint_2.ipynb
├── main_notebook.ipynb                # placeholder; not pushed yet
├── assets/
│   └── figures/
│       ├── popularity_longtail.png
│       ├── user_activity_clicks_per_user.png
│       ├── daily_interaction_volume.png
│       ├── read_time_distribution.png
│       └── scroll_depth_distribution.png
├── data/
│   ├── README.md                      # data placement instructions
│   └── train/                         # local-only (ignored by git)
│       └── behaviors.parquet          # local-only (ignored by git)
└── checkpoints/                       # planned: per-checkpoint exports
    └── ...                            # (folder may be added later)
```

## Results summary

The core takeaway so far: **EB‑NeRD has strong popularity concentration and a large cold-start segment**, so any recommender that works here must be robust to sparse histories and biased feedback—not just optimize clicks.

## Course context

CSCE 676 (Data Mining), Texas A&M University — Spring 2026.
