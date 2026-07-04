Trader Performance vs Market Sentiment Analysis
Overview
This project analyzes how Bitcoin market sentiment (Fear/Greed Index) relates to trader behavior and performance on Hyperliquid. Using 211,224 trades from 32 traders across 6 sentiment-classified days, we uncover actionable patterns for smarter trading strategies.

Project Structure
.
├── README.md                          # This file
├── REPORT.md                          # Full analysis report with insights
├── analysis.ipynb                     # Jupyter notebook with all code
├── fear_greed_index.csv               # Fear/Greed sentiment data
├── historical_data.csv                # Hyperliquid trade data
└── charts/
    ├── 01_performance_comparison.png  # Fear vs Greed performance
    ├── 02_trader_segmentation.png     # Trader segments
    ├── 03_deep_dive.png               # Sentiment impact deep dive
    ├── 04_trader_archetypes.png       # K-Means clustering
    └── 05_predictive_model.png        # Feature importance & confusion matrix
Setup & How to Run
Prerequisites
Python 3.8+
pip
Install Dependencies
pip install pandas numpy matplotlib seaborn scikit-learn scipy
Run the Analysis
jupyter notebook analysis.ipynb
Or run all cells in order to reproduce the full analysis.

Run Specific Parts
The notebook is organized into 7 cells:

Imports - Load all required libraries
Load Data - Read CSV files
Data Preparation - Clean, merge, create metrics
Fear vs Greed - Statistical comparison
Segmentation - Trader grouping by frequency
Clustering - K-Means behavioral archetypes
Predictive Model - Random Forest profitability prediction
Key Findings (Quick Summary)
Metric	Fear Days	Greed Days	Insight
Avg Daily PnL	$209,028	$90,916	Fear days 2.3x more profitable
Win Rate	86.9%	73.2%	+13.7pp on Fear days (p=0.047)
Trade Frequency	4,180	1,167	3.6x more trades on Fear days
Profitable Days	93.8%	78.4%	+15.4pp on Fear days
Top 3 Insights
Fear drives volume, Greed drives efficiency - Traders are 3.6x more active during Fear but earn less per trade
High-frequency traders dominate - 3.3x higher PnL than low-frequency peers ($224K vs $68K)
Behavior > Sentiment for prediction - Trading patterns (fees, size, frequency) are 10x more predictive than sentiment alone
Strategy Recommendations
Adaptive Frequency Scaling - Scale up 2-3x on Fear days (for algos); maintain discipline (for manual traders)
Short-Bias Contrarian - During Extreme Greed, increase short exposure to 60-70%
Fee Budget Cap - Limit daily fees to <$2,000 on Fear days to prevent overtrading erosion
Methodology
Data Cleaning - Timestamp conversion, non-trading event removal
Feature Engineering - Daily aggregates per trader (PnL, win rate, frequency, long/short ratio)
Alignment - Merged trade data with Fear/Greed index by date
Statistics - Independent t-tests for Fear vs Greed comparisons
Segmentation - Median splits and performance thresholds
Clustering - K-Means (k=4) with PCA visualization
Predictive Modeling - Random Forest (100 estimators, max_depth=5)
Data Sources
Fear/Greed Index: Alternative.me Crypto Fear & Greed Index (daily, Feb 2018 - May 2025)
Hyperliquid Trades: On-chain perp DEX trading data (Mar 2023 - Jun 2025)
Dependencies
Package	Version
pandas	>=1.3
numpy	>=1.21
matplotlib	>=3.4
seaborn	>=0.11
scikit-learn	>=1.0
scipy	>=1.7
Notes
The analysis covers 6 days with overlapping sentiment and trade data
Statistical significance: *p<0.05 considered significant
All monetary values in USD
Leverage data was not available in the dataset
Author
Data Science/Analytics Internship Project
