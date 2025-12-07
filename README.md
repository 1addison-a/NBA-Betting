# NBA Over/Under Betting Prediction Model

This project builds a machine learning model to predict **over/under outcomes** for NBA player statistics (Points, Rebounds, Assists) using historical player and team data. The models can assist in sports betting by generating probabilities and implied American odds.

---

## Table of Contents

- [Project Overview](#project-overview)  
- [Dataset](#dataset)  
- [Features](#features)  
- [Methodology](#methodology)  
- [Models](#models)  
- [Evaluation](#evaluation)  
- [Installation](#installation)  
- [Usage](#usage)  
- [Acknowledgement](#acknowledgement)  
- [References](#references)  

---

## Project Overview

The goal is to predict whether a player will score over or under their average performance in a given game. This includes:  

- Points  
- Rebounds  
- Assists  

The predictions are used to calculate implied **American betting odds** and provide recommendations for Over/Under betting strategies.

---

## Dataset

- `Games.csv`: Game-level data (scores, home/away teams, winner).  
- `PlayerStatistics.csv`: Player-level box score statistics.  
- `TeamStatistics.csv`: Team-level aggregated stats.  

The analysis focuses on the **2024-25 NBA season** and only includes players from playoff-contending teams.

---

## Features

The model uses the following features:  

- Player-level: `numMinutes`, `fieldGoalsAttempted`, `threePointersAttempted`, `freeThrowsAttempted`, `turnovers`, `plusMinusPoints`  
- Team-level: `team_teamScore`, `team_assists`, `team_reboundsTotal`  
- Opponent-level: `opp_teamScore`, `opp_reboundsTotal`, `opp_assists`  

Target labels are binary: **Over (1)** or **Under (0)**, calculated based on each player’s season average.

---

## Methodology

1. **Data Cleaning & Filtering**:  
   - Filtered to 2024-25 season  
   - Selected top 7 players per team by minutes  
   - Focused on playoff teams  

2. **Feature Engineering**:  
   - Merge player stats with game data  
   - Add team and opponent statistics  
   - Create over/under binary targets  

3. **Modeling**:  
   - Logistic Regression  
   - XGBoost  

4. **Evaluation Metrics**:  
   - Accuracy  
   - Precision  
   - Recall  
   - F1-score  
   - ROC-AUC  

5. **Betting Analysis**:  
   - Convert model probabilities to implied American odds  
   - Generate final betting recommendations  

---

## Models

- **Logistic Regression**: Interpretable, well-calibrated probabilities  
- **XGBoost**: Captures complex patterns, often higher predictive power  

The best model per stat is selected based on ROC-AUC.

---

## Evaluation

- Confusion matrices, ROC curves, and metric comparisons are generated for each target.  
- Probabilities and odds are summarized for practical betting strategies.  
- Visualizations provide comprehensive insights into model performance.

---

## Installation

```bash
# Clone repository
git clone <your-repo-url>
cd <repo-directory>

# Install dependencies
pip install -r requirements.txt
