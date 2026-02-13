# News Recommendation Analysis with EB-NeRD
**CSCE 676: Data Mining - Spring 2026**

## 📌 Project Overview
This project explores news recommendation strategies using the **Ekstra Bladet News Recommendation Dataset (EB-NeRD)**. We analyze user behavior, engagement patterns, and dataset biases to build a foundation for advanced recommendation models.

## 📊 Checkpoint 1: EDA & Insights
The first phase of this project focuses on Exploratory Data Analysis (EDA). 
Key findings include:
- **Popularity Bias:** A Gini Coefficient of 0.69, indicating a strong "Long Tail" distribution where a few articles dominate clicks.
- **User Activity:** A median of 9 clicks per user, with 10.6% being "Cold Start" users.
- **Engagement:** Analysis of read times (avg 10-20s) and scroll percentages.

## 📁 Repository Structure
- `Checkpoint1_EDA.ipynb`: Data loading, cleaning, and visualization.
- `data/`: (Optional/Note) Instructions on how to download the EB-NeRD dataset.

## 🚀 How to Run
1. Clone the repository.
2. Install dependencies: `pip install pandas matplotlib seaborn pyarrow`.
3. Open the `.ipynb` file in Google Colab or Jupyter Lab.
