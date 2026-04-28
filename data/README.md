# Data Setup

## EB-NeRD Dataset

The EB-NeRD (Ekstra Bladet News Recommendation Dataset) is required to run the notebooks.

### Download

1. Visit: https://recsys.acm.org/recsys24/challenge/
2. Download the dataset (behaviors.parquet is the main file needed)
3. Unzip locally

### Local Setup (Jupyter/Local Machine)
News-Rec-EBNeRD/
├── data/
│   └── train/
│       └── behaviors.parquet    ← Place the file here

After downloading, place `behaviors.parquet` at `data/train/behaviors.parquet`.

### Google Colab Setup

1. Download `behaviors.parquet` to your local machine
2. In Colab, upload it directly to the session:

```python
from google.colab import files
uploaded = files.upload()
```

3. The notebook expects it at `/content/behaviors.parquet`

### File Size Note

`behaviors.parquet` is ~2.5GB. It is **not** committed to GitHub due to size. You must download it separately using the link above.

### What's in behaviors.parquet

- 12,063,890 raw interactions
- After 5-second bounce filter: 11,739,470 interactions
- 787,028 unique users
- 6,171,934 sessions
- Columns: impression_id, article_id, read_time_seconds, scroll_percentage, user_id, session_id, and more

See `main_notebook.ipynb` for the full data loading and cleaning pipeline.
