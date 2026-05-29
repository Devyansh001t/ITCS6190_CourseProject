# ITCS 6190 – Cloud Computing for Data Analysis

## Course Project: Data Analysis with Apache Spark

## Project Proposal: NBA Game Outcome Prediction Pipeline


# Devyansh Tailor

---

### Dataset

**Source:** [NBA Games Dataset – Kaggle (nathanlauga/nba-games)](https://www.kaggle.com/datasets/nathanlauga/nba-games)

**Description:** A collection of NBA game logs and player statistics spanning multiple seasons (2004–2020). The dataset includes several CSV files:
- `games.csv` – game-level results (teams, scores, home/away, season)
- `games_details.csv` – player-level box score stats per game
- `teams.csv` – team metadata
- `players.csv` – player metadata
- `ranking.csv` – seasonal standings and win/loss records

**Size:** ~65,000 games; ~950,000 player-game rows across all files

**License:** Public domain / open use (Kaggle hosted)

**Storage:** Full datasets will be stored on AWS S3. Only a small representative sample will be committed to the GitHub repository for testing purposes.

---

### Analytical Questions

1. **Primary (Regression):** Can we predict the point margin (home team score − away team score) of an NBA game using pre-game features such as team offensive/defensive ratings, recent win streaks, rest days, and home court advantage?
2. **Secondary:** Which features are most predictive of winning margin — recent form, rest days, or season-long efficiency ratings?
3. **Streaming:** How do team performance metrics (e.g., rolling average point differential) evolve across a season when ingested game-by-game as a simulated live feed?

---

### Planned Spark Components

| Component | Planned Usage |
|---|---|
| **Structured APIs** | Ingest and join `games.csv`, `games_details.csv`, and `ranking.csv`; compute derived features (rolling averages, rest days, home/away splits) using DataFrame transformations and aggregations |
| **Spark SQL** | (Optional) Query top-performing teams by season, conference-level scoring averages, and home vs. away win rate comparisons |
| **Structured Streaming** | Simulate a real-time game feed by replaying historical game records micro-batch by micro-batch; compute running team stats as new games arrive |
| **MLlib** | Train a Linear Regression model (and optionally a Gradient Boosted Trees regressor) to predict point margin; report RMSE and R² as evaluation metrics |

---

### Reproducibility Plan

The full pipeline will be executable with a single command:
```bash
make run
```
or
```bash
bash run.sh
```
This will cover data ingestion from S3 (or local sample), feature engineering, streaming simulation, model training, and output generation.

---