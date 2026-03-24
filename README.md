# RFM Analysis

Customer segmentation project using the **RFM (Recency, Frequency, Monetary)** methodology on the Online Retail dataset.

## Project structure

```
data/
    cleaned_online_retail.csv   # Cleaned transaction data
    rfm_segments.csv            # Computed RFM scores and segments
first_cleaning.ipynb            # Data cleaning and preprocessing
rfm.ipynb                       # RFM score computation and segmentation
rfm_visualization.ipynb         # Charts and business interpretation
main.py                         # Entry point (optional CLI execution)
```

## Methodology

1. **Data cleaning** — remove cancellations, nulls, and negative quantities/prices.
2. **RFM scoring** — compute Recency, Frequency, and Monetary values per customer, then assign scores from 1 to 5 using quintiles.
3. **Segmentation** — combine scores to assign each customer to a named segment (Baleines, Clients fidèles actifs, Nouveaux clients, À risque, Clients perdus, Autres).
4. **Visualization** — histograms, heatmap (R × F → average spend), bar chart of segment sizes, and scatter plot (Frequency vs Monetary coloured by Recency).

## Segments

| Segment | Criteria | Strategy |
|---|---|---|
| Baleines | R ≥ 4, F ≥ 4, M ≥ 4 | Premium loyalty programme, early access |
| Clients fidèles actifs | R ≥ 4, F ≥ 3 | Cross-sell, upsell, referral programme |
| Nouveaux clients | R ≥ 4, F ≤ 2 | Onboarding sequence, 2nd-purchase coupon |
| À risque | R ≤ 2, F ≥ 3 | Early re-engagement offer |
| Clients perdus | R ≤ 2, M ≥ 4 | Win-back campaign, satisfaction survey |
| Autres | — | Standard communications |

## Getting started

```bash
# Create and activate a virtual environment
python -m venv .venv && source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt   # or: pip install pandas matplotlib seaborn

# Run notebooks in order
jupyter lab
```
