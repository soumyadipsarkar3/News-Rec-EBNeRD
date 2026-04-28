# Three Problems, Three Methods: A Sequential News Recommendation System

Modern news recommendation is harder than “rank what’s popular.” Real readers are **heterogeneous** (from casual browsers to deep readers), consumption is **sequential** (threaded exploration across articles), and a meaningful slice of traffic is **cold-start** (little to no history). This project builds a practical, story-driven recommendation pipeline on the **EB‑NeRD** dataset that treats these as *three distinct problems*—and shows why **one algorithm cannot solve all three well**. The key contribution is the **composition**: segment users by engagement, mine order-aware reading patterns, and route sparse-history users to a sequential deep model designed for short interaction traces.

## 2) Pointer to `main_notebook.ipynb`
🎥 https://www.youtube.com/watch?v=ua6LKzbVGfk

👉 **Start here:** **[`main_notebook.ipynb`](main_notebook.ipynb)**

## 3) Research questions

**RQ1 — User heterogeneity:** Do users cluster into interpretable engagement tiers (e.g., skimmers vs deep readers), and can those tiers guide what “good recommendations” should prioritize?

**RQ2 — Sequential reading:** How often do sessions follow multi-article reading trails, and what *order-aware* patterns predict the next article better than unordered co-occurrence rules?

**RQ3 — Cold-start:** For users with extremely short histories, can a Transformer-based sequential recommender outperform simple baselines by extracting signal from minimal evidence?

## 4) Project video

🎥 **[YouTube video — to be added]**

## 5) Data (EB‑NeRD)

- **Dataset**: EB‑NeRD (Ekstra Bladet News Recommendation Dataset), released for the ACM RecSys Challenge
- **Download**: `https://recsys.acm.org/recsys24/challenge/`
- **Preprocessing**: remove **reads < 5 seconds** (about **2.7%** of raw interactions) to reduce bounce noise

**Placement instructions**

- **Colab**: upload the parquet so it exists at `/content/behaviors.parquet`
- **Local**: place at `data/train/behaviors.parquet`

See `data/README.md` for the exact expected layout.

![Popularity long-tail](assets/figures/popularity_longtail.png)
*Figure: Clicks follow a strong long-tail—popularity is a powerful baseline, but also a major bias source (Gini quantified below).*

## 6) How to reproduce (Google Colab)

This project was developed and run in **Google Colab**.

1. **Open** `main_notebook.ipynb` in Colab.
2. **Upload data** to `/content/behaviors.parquet`.
3. **Install dependencies** (from repo root `requirements.txt`):

   ```bash
   pip install -r requirements.txt
   ```

   (In Colab, run `!pip install -r requirements.txt` in a cell.)
4. **Run notebooks in this order**:
   - `main_notebook.ipynb` (final curated analysis + results)
   - `checkpoints/checkpoint_1.ipynb` (project progression: EDA + problem diagnosis)
   - `checkpoints/checkpoint_2.ipynb` (project progression: feasibility + method prototypes)

![Daily interaction volume](assets/figures/daily_interaction_volume.png)
*Figure: Interaction volume varies over time, reinforcing the need for realistic evaluation and time-aware thinking in news recommendation.*

## 7) Key dependencies & versions

- **Python**: 3.11
- **pandas**: 2.x
- **scikit-learn**: 1.x
- **mlxtend**: (Apriori / frequent itemset mining)
- **prefixspan**: (sequential pattern mining)
- **torch**: 2.x (SASRec)

The full environment is captured in `requirements.txt`.

## 8) Repo structure

```text
News-Rec-EBNeRD/
├── main_notebook.ipynb
├── requirements.txt
├── README.md
├── .gitignore
├── checkpoints/
│   ├── checkpoint_1.ipynb
│   └── checkpoint_2.ipynb
├── data/
│   └── README.md
└── assets/
    └── figures/
        ├── popularity_longtail.png
        ├── user_activity_clicks_per_user.png
        ├── daily_interaction_volume.png
        ├── read_time_distribution.png
        ├── scroll_depth_distribution.png
        ├── correlation_matrix.png
        ├── kmeans_elbow_silhouette.png
        ├── cluster_profiles_bars.png
        ├── cluster_pca_scatter.png
        ├── apriori_rules.png
        ├── sasrec_training_curves.png
        └── sasrec_evaluation.png
```

## 9) Results summary

- **11.7M** cleaned interactions across **787K** users  
- **44.1%** of sessions contain **multi-article sequences**  
- **19.1%** of users are **cold-start** \((<3 clicks)\)  
- **K-means** finds **5** user tiers with **silhouette = 0.58**  
- **Gini = 0.69**, confirming **strong popularity bias**  

The big takeaway is that EB‑NeRD is a **high-bias, high-sparsity, sequence-heavy** environment: readers differ sharply in engagement, many sessions contain meaningful multi-step trails, and a large cold-start segment limits history-based methods. The practical insight is that the strongest approach is **not a single model**, but a **composed system** that routes users to the method best matched to the evidence available (tier + sequence + history length). Full analysis and evaluation live in `main_notebook.ipynb`.

![User activity distribution](assets/figures/user_activity_clicks_per_user.png)
*Figure: Engagement is highly skewed—many users have very short histories, motivating cold-start handling and tier-aware modeling.*

![Correlation matrix](assets/figures/correlation_matrix.png)
*Figure: Behavioral signals (clicks, read time, scroll depth) carry complementary information—useful for segmentation rather than relying on clicks alone.*

![K-means elbow + silhouette](assets/figures/kmeans_elbow_silhouette.png)
*Figure: Clustering diagnostics supporting \(k=5\) engagement tiers with silhouette 0.58.*

![Cluster profiles](assets/figures/cluster_profiles_bars.png)
*Figure: Interpretable engagement tiers—useful for thinking about different recommendation objectives (novelty vs reliability vs depth).*

![Apriori rules](assets/figures/apriori_rules.png)
*Figure: Co-occurrence rules capture “read-together” behavior but ignore direction; this motivates order-aware sequence mining (PrefixSpan).*

![SASRec training curves](assets/figures/sasrec_training_curves.png)
*Figure: SASRec training behavior on sequential click traces—used as the cold-start path when histories are too short for stable collaborative signals.*

![SASRec evaluation](assets/figures/sasrec_evaluation.png)
*Figure: Comparative evaluation summary used to assess the cold-start recommendation approach (see notebook for metrics and setup).*

## Checkpoint Progression

Checkpoint 1 established the data story (popularity bias, heterogeneity, and sequential sessions) and defined what a realistic recommendation setting looks like on EB‑NeRD. Checkpoint 2 translated that diagnosis into feasible method choices—segmentation, sequential pattern mining, and a Transformer sequential model—setting up the final notebook as a curated end-to-end narrative where the contribution is the **integrated system**, not isolated experiments.

## Limitations & Future Work

- **Offline-only evaluation**: ranking metrics on held-out data don’t replace online A/B tests or real user feedback loops.
- **Temporal dynamics**: topic drift and recency effects are critical in news; a production system should model freshness and time-aware behavior explicitly.
- **Cold-start remains hard**: users with 0–2 clicks have extremely limited signal; hybrid strategies (content, context, popularity-with-constraints) are still needed.
- **Clustering assumptions**: K-means favors roughly spherical clusters; alternative models (GMM, density-based) may capture irregular behavior better.
- **Pattern mining coverage**: frequent pattern methods can miss rare-but-important trails; scaling and sampling choices matter for recall.
- **Content understanding**: this work primarily uses behavioral traces; adding text/topic embeddings and entity signals could improve personalization and robustness.

CSCE 676 (Data Mining), Texas A&M University — Spring 2026
