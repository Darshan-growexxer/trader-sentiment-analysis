# Trader Behavior vs. Market Sentiment Analysis

**Primetrade.ai Data Science Intern - Round 0 Assignment**

## Objective
This project analyzes how Bitcoin's market sentiment (Fear vs. Greed) influences trader behavior and profitability on the Hyperliquid platform. The goal is to uncover behavioral patterns to inform smarter, automated trading strategies and risk-management protocols.

## Repository Structure
* `data_needed/` : Contains the two datasets (`fear_greed_index.csv` and `historical_data.csv`).
* `analysis.ipynb` : The main Jupyter Notebook containing data cleaning, feature engineering, analysis, and visualizations.
* `requirements.txt` : Python dependencies required to run the notebook.
* `README.md` : Project summary and findings.

## Setup & How to Run
To ensure full reproducibility, please follow these steps:
1. Clone this repository to your local machine.
2. Ensure you have Python 3.8+ installed.
3. Install the required packages by running:
   ```bash
   pip install -r requirements.txt
   
## Methodology
1. **Data Cleaning & Alignment:** Loaded the daily Fear/Greed index and Hyperliquid historical trade data. Simplified sentiment into 'Fear', 'Greed', and 'Neutral'. Converted precise trade timestamps (IST) into a standardized daily format to merge with the sentiment data.
2. **Feature Engineering:** Since explicit leverage wasn't provided, `Size USD` was used as a proxy for trade risk/leverage. Calculated daily metrics per trader: `Daily PnL`, `Win Rate`, `Total Trades`, `Average Trade Size`, and `Long/Short Ratio`.
3. **Segmentation:** Grouped traders into distinct archetypes to observe varying reactions to market sentiment:
   * **Frequency:** Frequent (>5 trades/day) vs. Infrequent.
   * **Consistency:** Consistent (Profitable on >50% of active days) vs. Inconsistent.

---

## Key Insights

**1. Performance vs. Sentiment: Fear pays the few, Greed pays the many.**
While the average win rate remains stable across all sentiments (~61%), the *average* Daily PnL per trader is highest on "Fear" days (~$5,185) compared to "Greed" days (~$4,144). However, the *median* PnL is higher on Greed days. This indicates that Fear days create massive, volatile outlier wins for specific traders, while Greed days offer steady, smaller wins for the majority.

**2. Behavior vs. Sentiment: Fear induces hyperactivity and risk-taking.**
Traders change their behavior drastically based on sentiment. During "Fear" days, the average number of trades per user jumps by ~35% (105 trades/day vs 76 on Greed days). Furthermore, their average trade size spikes to over $8,500 during Fear (compared to ~$5,900 during Greed), indicating a desperate "catch the falling knife" mentality.

**3. Segmentation: Consistent traders capitalize on panic.**
Our "Consistent" trader segment generates their highest average PnL during Fear regimes, successfully extracting value from market panic. Conversely, our "Inconsistent" segment makes the bulk of their money during Greed days, relying on easy, upward-trending markets to survive.

---

## Actionable Strategy Recommendations

Based on the findings above, here are two proposed platform strategies:

**Strategy 1: "Volatility Hunter" Capital Allocation (Algo/Copy Trading)**
* **The Rule:** Dynamically shift capital allocation toward "Consistent" and "High-Frequency" trader segments when daily sentiment shifts into "Fear."
* **Why:** The data proves this segment is highly capable of navigating and profiting from high-volatility, fearful markets, whereas standard trend-followers (Inconsistent segment) lose their edge. 

**Strategy 2: Automated "Panic-Button" Risk Control (Retail UI)**
* **The Rule:** During "Extreme Fear" days, implement a UI warning or a soft leverage cap for retail users (specifically in the "Inconsistent" segment) if their daily average trade size suddenly spikes by >50%. 
* **Why:** The data shows average traders excessively increase their trade size and long-bias during Fear to try and recover losses. This automated intervention would protect users from over-leveraging into liquidation spirals.
