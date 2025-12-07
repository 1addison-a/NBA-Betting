# NBA Over/Under Betting Prediction Model

This project builds a machine learning model to predict over/under outcomes for NBA player statistics (Points, Rebounds, Assists) using historical player and team data. The models can assist in sports betting by generating probabilities and implied American odds.

## Table of Contents
- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Features](#features)
- [Methodology](#methodology)
- [Models](#models)
- [Evaluation](#evaluation)
- [Installation](#installation)

---

## Project Overview

The goal is to predict whether an NBA player will perform **over or under** their average in a given game. This includes:  
- Points  
- Rebounds  
- Assists  

Predictions are used to calculate **implied American betting odds** and provide recommendations for Over/Under betting strategies. This project blends sports analytics with machine learning concepts, such as feature engineering, model evaluation, and classification.

---

## Dataset

The analysis focuses on the **2024-25 NBA season**, restricted to playoff-contending teams. The following CSV files were used:

- **Games.csv**: Game-level data (scores, home/away teams, winner)  
- **PlayerStatistics.csv**: Player-level box score statistics  
- **TeamStatistics.csv**: Team-level aggregated stats  

**Sample Selection Criteria:**

- Top 7 players per team by total minutes played  
- 16 playoff-contending teams  
- Games from October 22, 2024 onward  

This ensures high-quality, consistent data and reduces noise from sporadic bench performances.

---

## Features

The model uses **12 features** organized into three categories:

### Player-Level (6)
- `numMinutes`: Minutes played  
- `fieldGoalsAttempted`  
- `threePointersAttempted`  
- `freeThrowsAttempted`  
- `turnovers`  
- `plusMinusPoints`: Plus-minus differential  

### Team-Level (3)
- `team_teamScore`: Team total points  
- `team_assists`  
- `team_reboundsTotal`  

### Opponent-Level (3)
- `opp_teamScore`  
- `opp_reboundsTotal`  
- `opp_assists`  

**Target Labels:** Binary  
- **Over (1)**: Player exceeds season average  
- **Under (0)**: Player does not exceed season average  

---

## Methodology

### Data Cleaning & Filtering
- Filtered to the 2024-25 season  
- Selected top 7 players per team by minutes  
- Focused on playoff teams  

### Feature Engineering
- Merge player stats with game data  
- Add team and opponent statistics  
- Create Over/Under binary targets  

### Data Preprocessing
- Missing values (<1%) imputed with zero  
- Logistic Regression features standardized (z-score)  
- XGBoost does not require scaling  
- Stratified 80/20 train-test split (random_state=42)  

---

## Models

### Logistic Regression
- Linear model, interpretable, probability-calibrated  
- L2 regularization to prevent overfitting  

### XGBoost
- Non-linear ensemble of decision trees  
- Captures feature interactions  
- Hyperparameters: `n_estimators=200`, `max_depth=6`, `learning_rate=0.1`, `subsample=1.0`, `colsample_bytree=1.0`, `lambda=1`

**Model Training Procedure:**  
- Train separately for points, rebounds, assists  
- Evaluate using Accuracy, Precision, Recall, F1-score, ROC-AUC  
- Analyze feature importance and decision boundaries  

---

## Evaluation

### Key Results

| Target | Model | Accuracy | ROC-AUC | Best |
|--------|-------|---------|---------|------|
| Points | Logistic Reg | 0.691 | 0.766 | ✓ |
| Points | XGBoost | 0.678 | 0.757 |  |
| Rebounds | Logistic Reg | 0.667 | 0.727 | ✓ |
| Rebounds | XGBoost | 0.643 | 0.686 | - |
| Assists | Logistic Reg | 0.637 | 0.695 | ✓ |
| Assists | XGBoost | 0.618 | 0.655 |  |

**Observations:**
- Logistic Regression outperforms XGBoost overall  
- Points are most predictable, Assists least predictable  
- All models outperform random baseline (0.50 ROC-AUC)  
- Predicted probabilities can be converted to **implied American odds** for betting recommendations.  
  Example: 0.65 probability → +143 odds  

---

## Installation

```bash
# Clone repository
git clone https://github.com/1addison-a/NBA-Betting
cd NBA-Betting/myProject

# Install dependencies
pip install -r requirements.txt
```
