# Take Me Out to the Ball Game  
### Bayesian OPS+ Forecasting with Statcast Data

---

## Purpose  
Major League Baseball teams, analysts, and scouts face a recurring challenge: predicting what a hitter will do next—not just what they’ve already done. Traditional statistics lag reality, and black-box models often fail to offer interpretable guidance.

This project builds a transparent, Bayesian forecasting pipeline that models hitter performance—specifically OPS+—using rolling Statcast features, player-specific baselines, and probabilistic inference. The aim is to support baseball decision-making, including trade valuation, matchup planning, waiver claims, and player development.

---

## Action  
To achieve this goal, the project:

1. **Aggregates Statcast event-level and monthly performance data** into a clean analytical dataset.  
2. **Engineers baseball-specific features**, including rolling OPS, xwOBA deltas, launch-speed trends, and hot-streak indicators.  
3. **Constructs player-specific baselines**, enabling detection of deviations from a hitter’s own norms.  
4. **Implements a hierarchical Bayesian model (Pyro)** to generate OPS+ predictions with credible intervals.  
5. **Uses Gaussian Mixture Model (GMM) priors** to encode hitter archetype expectations (power hitters, contact hitters, replacement-level types).  
6. **Performs posterior predictive sampling and calibration diagnostics**, including CI coverage and residual analysis.  
7. **Evaluates the model league-wide on the 2022 season**, testing predictive stability and uncertainty accuracy.

---

## Conclusions  
The project finds that:

• **Rolling quality-of-contact features** (3-day, 7-day, and 100-day deltas) meaningfully predict near-future OPS+.  
• **Player-specific baselines outperform league-averaged metrics**, improving detection of trend shifts.  
• **Bayesian priors stabilize predictions**, especially in sparse or noisy situations.  
• **Credible intervals achieved ~72% coverage** for a nominal 95%, indicating conservative calibration.  
• Predictive reliability is highest for players with consistent trending behavior; volatile or injured hitters display wider uncertainty bands.  
• The pipeline provides **interpretable, variance-aware guidance** useful for baseball scouting and analytics operations.

These outcomes align with the project’s purpose: deliver a transparent, interpretable forecasting foundation for MLB hitter performance without relying on opaque black-box models.

---

## Evidence  
The repository includes all supporting materials:
```
├── data/
│   └── bayesian_test_predictions5.csv → Monthly OPS+ predictions with 95% credible intervals and full input features
├── plots/
│   ├── top25_pred_vs_actual_5.png     → Top 25 predicted OPS+ vs actuals
│   ├── bottom25_pred_vs_actual_5.png  → Bottom 25 predicted OPS+ vs actuals
│   ├── coverage_by_decile_95CI.png    → Coverage rate by predicted OPS+ decile
│   └── bayesian_calibration_5.png     → Calibration plot with 95% credible intervals
├── models/                            → Pyro model code and saved checkpoints (available on request)
├── notebooks/                         → Training, evaluation, and posterior diagnostics
```


---

# Extended Technical Description

## Bayesian OPS+ Forecasting for Baseball Players  
This project implements a probabilistic model for forecasting player-level OPS+ using rolling Statcast and performance trends. It’s designed with real-world baseball decision-making in mind—trade deadlines, scouting reports, platoon usage, and discovering untapped upside.

Whether it’s late July and you’re weighing a trade return, or early April and you’re evaluating a non-roster invitee, the core question remains:

**What can this player do next—not just what has he done?**

The model was run league-wide on the 2022 season to test calibration, variance control, and predictive performance. Its real value emerges when zooming in to player-specific trajectories: identifying hot streaks worth trusting, cold streaks showing regression risk, or subtle signs of meaningful mechanical changes.

---

## Project Objective  
Build a Bayesian forecasting model that:

• Predicts OPS+ with interpretable **uncertainty intervals**  
• Incorporates **rolling monthly metrics** and Statcast data  
• Provides variance-aware insights tuned to individual hitters  
• Supports baseball use cases such as trades, scouting, and lineup decisions

---

## Key Features  
• Rolling 3-, 7-, and 100-day trend captures  
• Delta features for xwOBA and launch speed  
• Hierarchical Bayesian structure (Pyro)  
• GMM priors encoding hitter archetypes  
• Full posterior predictive sampling  
• CI coverage evaluation and calibration plotting  
• Robust to sparse monthly data and recoverable post-injury performance

---

## Workflow Overview  

### Data Preprocessing  
Cleans, aggregates, and aligns Statcast features with monthly performance data.

### Feature Engineering  
• Rolling OPS  
• xwOBA deltas  
• Launch speed trends  
• Player-specific baseline deviations  
• Hot/cold streak indicators

### Modeling  
• Hierarchical Bayesian model implemented in Pyro  
• GMM-derived informative priors for OPS+ expectations  
• Posterior sampling and inference  
• Calibration analysis and interval evaluation

### Evaluation  
• RMSE for point predictions  
• CI coverage metrics  
• Residual analysis  
• Top-25 and bottom-25 comparison plots

---

## Baseball Use Cases  

### Trade Valuation  
Identify trending players whose improvements are statistically meaningful, not noise.

### Scouting & Player Development  
Track minor-league progress, evaluate call-ups, and spot actionable mechanical trends.

### Matchup Planning  
Use credible intervals to determine risk-adjusted lineup decisions.

### Recovery & Variance Management  
Model gracefully handles sparse data, making it well-suited for injury-return evaluation.

---

## Limitations  
• Players with limited recent data may be excluded unless inferred from priors alone.  
• Monthly aggregation may smooth over game-level volatility; a daily model is possible but computationally intensive.  
• Some elite players (e.g., Judge, Acuña) are missing due to data filtering constraints. This affects top-OPS+ calibration.

---

## Future Improvements  
• Add pitcher-adjusted context for matchup-specific predictions  
• Incorporate injury trajectories, age curves, or team-effect priors  
• Expand to multi-output predictions (e.g., OBP, SLG separately)  
• Explore daily-level Bayesian updating for more granular inference  

---

## Author  
**John Grier**  
MS Data Science Candidate, Illinois Tech  
[github.com/J-Grier](https://github.com/J-Grier)


