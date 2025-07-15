# Bayesian OPS+ Forecasting for Baseball Players

This project implements a probabilistic model for predicting player-level OPS+ using rolling Statcast and performance features. The model is built for practical baseball applications such as trade evaluation, matchup planning, and scouting decisions.

## 🔍 Project Objective
To build a **Bayesian forecasting model** that:
- Predicts player OPS+ with uncertainty intervals
- Incorporates rolling monthly metrics and Statcast data
- Provides interpretable, variance-aware forecasts
- Supports use cases like **trade decisions** and **game-by-game scouting**

## ⚾ Key Features
- **Rolling 3-day and 100-day anchors**: Capture short- and long-term trends
- **Delta features**: Track deviations in xwOBA and launch speed vs baseline
- **Hierarchical Bayesian Model (Pyro)**: Predicts OPS+ with 95% credible intervals
- **CI Coverage Evaluation**: Achieved ~72% coverage for 95% CI
- **Model is robust to sparse data**, can be adapted for partial seasons or injury-recovery cases

## 🛠️ Workflow
1. **Data Preprocessing**: Cleans and rolls monthly-level performance and Statcast data
2. **Feature Engineering**:
   - Rolling OPS, xwOBA, launch speed
   - Player-specific baselines and deltas
3. **Modeling**:
   - Bayesian Neural Network with Pyro
   - he Bayesian model uses informative priors derived from a Gaussian Mixture Model (GMM) trained on historical OPS+ distributions. This allows the model to encode player-type-level expectations (e.g., power hitter, contact hitter, replacement level) and regularize predictions in the presence of noisy or sparse monthly data.
   - Full posterior predictive sampling
4. **Evaluation**:
   - RMSE and CI coverage against test season (2022 held out)
   - Visualized residuals and top-25 predictions

## 💡 Use Cases
- **Trade Valuation**: Estimate future offensive contribution of trade targets
- **Scouting Decisions**: Prioritize call-ups or platoon usage based on predictive confidence
- **Matchup Planning**: Align lineups around short-term hot/cold indicators

## 📂 File Structure
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

## 🚧 Limitations
- Players with too little data (e.g. injured stars) may be excluded unless specifically recovered
- Model assumes monthly aggregation — can be adapted to game-level with daily anchoring

> ⚠️ **Player Coverage Note**:  
> Star players like Aaron Judge and Ronald Acuña Jr. do not appear in the dataset due to data availability or filtering steps. This affects the top end of the OPS+ distribution, and model evaluation should be interpreted in that context.


## 📈 Future Improvements
- Incorporate pitcher-adjusted context for matchup-specific forecasts
- Add injury, age, or team effect priors
- Expand to multi-output predictions (e.g., OBP, SLG separately)

## 👨‍💻 Author
John Grier  
MS Data Science Candidate, Illinois Tech  
[github.com/J-Grier](https://github.com/J-Grier)
