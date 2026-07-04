# Trader Performance vs Market Sentiment Analysis
## Data Science/Analytics Internship Project

---

## Executive Summary

This analysis examines the relationship between Bitcoin market sentiment (Fear/Greed Index) and trader behavior/performance on Hyperliquid using 211,224 trades from 32 traders across 6 sentiment-classified days. The study reveals **significant behavioral and performance differences** between Fear and Greed sentiment periods, identifies four distinct trader archetypes, and provides actionable strategy recommendations.

---

## Part A: Data Preparation

### Datasets Overview

| Dataset | Rows | Columns | Date Range | Key Fields |
|---------|------|---------|------------|------------|
| Fear/Greed Index | 2,644 | 4 | Feb 2018 - May 2025 | timestamp, value, classification, date |
| Historical Trades | 211,224 | 16 | Mar 2023 - Jun 2025 | Account, Coin, Execution Price, Size USD, Side, Closed PnL, Direction |

### Data Quality
- **Missing Values**: 0 in both datasets
- **Duplicates**: 0 in both datasets
- **Date Overlap**: 6 days with both trade and sentiment data

### Key Metrics Created (Daily per Trader)
| Metric | Description |
|--------|-------------|
| `daily_pnl` | Sum of realized PnL per day |
| `win_rate` | Percentage of profitable trades |
| `daily_trades` | Number of trades executed |
| `avg_trade_size` | Mean trade size in USD |
| `long_ratio` | Percentage of long-direction trades |
| `total_volume` | Daily trading volume |
| `is_profitable_day` | Binary flag for profitable days |

---

## Part B: Analysis & Findings

### B1. Performance: Fear vs Greed Days

| Metric | Fear Days | Greed Days | Difference | Statistical Significance |
|--------|-----------|------------|------------|------------------------|
| **Avg Daily PnL** | **$209,028** | $90,916 | +$118,112 | p = 0.135 (not sig.) |
| **Median Daily PnL** | **$81,251** | $20,926 | +$60,325 | - |
| **Avg Win Rate** | **86.9%** | 73.2% | +13.7 pp | **p = 0.047** |
| **Avg Trade Frequency** | **4,180** | 1,167 | +3,013 | **p = 0.004** |
| **Profitable Days %** | **93.8%** | 78.4% | +15.4 pp | - |
| **Avg Trade Size** | $5,922 | $5,667 | +$255 | Not sig. |
| **Avg Volume** | **$22.0M** | $4.2M | +$17.8M | - |
| **PnL per Trade** | $50.01 | **$77.91** | -$27.90 | - |

**Key Finding**: Traders are significantly more active on Fear days (3.6x more trades) with higher win rates and a greater likelihood of ending profitable. However, Greed days show higher efficiency per trade ($77.91 vs $50.01).

### B2. Behavior Changes by Sentiment

| Behavior Metric | Fear Days | Greed Days | Insight |
|-----------------|-----------|------------|---------|
| **Trade Frequency** | 4,180/day | 1,167/day | Traders are 3.6x more active during Fear |
| **Long/Short Ratio** | 50.2% long | 56.0% long | Slightly more long-biased during Greed |
| **Median Trade Size** | $790 | $1,000 | Smaller median position size during Fear |
| **Total Fees Paid** | $4,526 | $840 | 5.4x more fees during Fear (due to volume) |
| **Daily Volume** | $22.0M | $4.2M | 5.2x more volume during Fear |

**Key Insight**: Fear triggers hyperactivity - traders trade more frequently but in smaller individual sizes. Greed leads to fewer, more selective trades with higher per-trade profitability.

### B3. Trader Segmentation

#### By Trade Frequency
| Segment | Count | Avg Daily PnL | Avg Win Rate | Avg Daily Trades |
|---------|-------|---------------|--------------|-----------------|
| **High Frequency** | 16 | **$224,125** | 80.5% | 5,301 |
| **Low Frequency** | 16 | $68,234 | 79.8% | 624 |

High-frequency traders earn 3.3x more on average despite similar win rates, suggesting volume-based strategies can be profitable on Hyperliquid.

#### By Consistency
| Segment | Count | Avg Daily PnL | Avg Win Rate |
|---------|-------|---------------|--------------|
| **Consistent Winners** | 23 | $149,180 | 88.4% |
| **Moderate** | 8 | $156,402 | 64.2% |
| **Inconsistent** | 1 | -$4,617 | 35.4% |

72% of traders (23/32) are consistent winners with >75% profitable days.

---

## Part C: Key Insights

### Insight 1: Fear = Volume, Greed = Efficiency
During Fear days, traders generate 3.6x more trades and 5.2x more volume, but earn less per trade ($50 vs $78). This suggests Fear drives reactionary trading, while Greed enables more calculated, higher-conviction positions.

### Insight 2: High-Frequency Traders Dominate
The top 16 traders by frequency earn 3.3x more than low-frequency peers ($224K vs $68K daily). This suggests algorithmic or systematic strategies are highly effective on Hyperliquid, especially during volatile Fear periods.

### Insight 3: Win Rate is the Differentiator
Consistent winners (72% of traders) maintain 88%+ win rates. The key differentiator is not trade size or frequency alone, but disciplined execution that maintains high win rates across sentiment regimes.

### Insight 4: Long Bias Doesn't Guarantee Success
Short-biased winners (29.7% long ratio) actually outperform long-biased winners (84.2% long ratio) with $116K vs $72K daily PnL. This suggests contrarian short strategies may be underappreciated.

---

## Part D: Strategy Recommendations

### Strategy 1: Adaptive Frequency Scaling
**Rule of Thumb**: During Fear days, increase trade frequency by 2-3x for high-frequency traders; maintain or reduce frequency for manual traders.

| Segment | Fear Day Action | Greed Day Action |
|---------|----------------|-----------------|
| High-Frequency (algorithmic) | Scale up 2-3x, maintain tight stops | Reduce frequency, focus on high-conviction setups |
| Low-Frequency (manual) | Maintain discipline, avoid FOMO | Increase size selectively |

**Rationale**: High-frequency traders already capitalize on Fear-day volatility. Manual traders risk overtrading and paying excessive fees ($4,526 avg vs $840 on Greed days).

### Strategy 2: Short-Bias Contrarian Strategy
**Rule of Thumb**: During Extreme Greed days, increase short exposure to 60-70% of portfolio.

**Rationale**: 
- Short-biased traders earn 62% more than long-biased traders ($116K vs $72K)
- Extreme Greed often precedes corrections
- Only 2 of 32 traders are already exploiting this systematically

### Strategy 3: Fee-Conscious Trading on Fear Days
**Rule of Thumb**: Set a daily fee budget of <$2,000 during Fear days to prevent overtrading erosion.

**Rationale**: Average fees on Fear days are $4,526 vs $840 on Greed days. With PnL per trade at only $50 during Fear (vs $78 during Greed), excessive trading can erode profits rapidly.

---

## Bonus: Trader Archetypes (Clustering)

Using K-Means clustering on 6 behavioral features, we identified 4 distinct trader archetypes:

| Archetype | Count | Avg PnL | Win Rate | Key Trait |
|-----------|-------|---------|----------|-----------|
| **Short-Biased Winners** | 12 | $116,122 | 87.3% | 70% short ratio, high consistency (97% profitable days) |
| **Long-Biased Winners** | 10 | $71,768 | 87.3% | 84% long ratio, moderate frequency |
| **Balanced Traders** | 8 | $152,619 | 58.3% | Mixed direction, highest trade size ($9.7K avg) |
| **High-Frequency Elite** | 2 | $672,819 | 88.5% | 19,722 trades/day, exceptional performers |

---

## Bonus: Predictive Model

A Random Forest classifier was trained to predict next-day profitability buckets (Loss / Small Profit / Big Profit) using sentiment + behavior features.

**Model Performance**: 47.6% accuracy (baseline: 33%)

**Feature Importance Ranking**:
1. **Total Fees (25.6%)** - Most predictive of profitability
2. **Avg Trade Size (24.6%)** - Position sizing matters
3. **Daily Trades (23.1%)** - Frequency is a key signal
4. **Long Ratio (14.1%)** - Directional bias has moderate impact
5. **Sentiment Value (10.1%)** - Raw sentiment score
6. **Sentiment Binary (2.6%)** - Fear/Greed alone is least predictive

**Key Takeaway**: Behavioral features (fees, size, frequency) are 10x more predictive than sentiment alone. Trading behavior is a stronger signal than market sentiment.

---

## Methodology

1. **Data Cleaning**: Converted timestamps, removed non-trading events (dust conversions, liquidations), validated data quality
2. **Feature Engineering**: Created daily aggregates per trader (PnL, win rate, trade frequency, long/short ratio, volume, fees)
3. **Alignment**: Merged trade data with Fear/Greed index on date field, resulting in 77 trader-day observations across 6 sentiment-classified days
4. **Statistical Testing**: Used independent t-tests to compare Fear vs Greed metrics
5. **Segmentation**: Applied median splits and performance thresholds to identify distinct trader groups
6. **Clustering**: K-Means (k=4) on standardized behavioral features with PCA visualization
7. **Predictive Modeling**: Random Forest with 5 behavioral + 2 sentiment features, 70/30 train/test split

---

## Deliverables

| File | Description |
|------|-------------|
| `analysis.ipynb` | Full analysis notebook with all code |
| `REPORT.md` | This comprehensive report |
| `charts/01_performance_comparison.png` | Fear vs Greed performance metrics |
| `charts/02_trader_segmentation.png` | Trader segmentation analysis |
| `charts/03_deep_dive.png` | Deep dive: sentiment impact on behavior |
| `charts/04_trader_archetypes.png` | K-Means clustering / archetypes |
| `charts/05_predictive_model.png` | Feature importance & confusion matrix |

---

## Limitations

1. **Sample Size**: Only 6 overlapping days with sentiment data limits statistical power
2. **Snapshot Bias**: Trade data appears to be from specific snapshot days rather than continuous
3. **No Leverage Data**: Explicit leverage values were not available in the dataset
4. **Causality**: Correlation does not imply causation - sentiment may reflect rather than drive behavior

---

*Analysis completed using Python (pandas, numpy, scikit-learn, matplotlib, seaborn). All code is reproducible and available in the accompanying notebook.*
