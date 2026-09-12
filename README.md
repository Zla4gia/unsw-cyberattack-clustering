# The Scaling Trap: Clustering Real Cyberattack Traffic

Can an unsupervised algorithm spot cyberattacks in network traffic without ever being shown a labeled example? 
This notebook runs that experiment on the real **UNSW-NB15** cybersecurity dataset (175,000+ network connections) — 
and finds that the most impressive-looking result was also the least trustworthy one.

**Full write-up:**
[Read the article on Medium]
(https://medium.com/@zlaforgia/the-scaling-trap-how-i-got-a-misleadingly-perfect-clustering-score-on-real-cyberattack-data-137bcf2b1143?postPublishedType=initial)

## What's in this notebook

Four experiments, same data, same algorithm (K-Means), one variable changed each time:

| Experiment | What changed | Silhouette Score | Trustworthy? |
|---|---|---|---|
| A | No feature scaling | ~0.68 (looks great) | No — driven by an irrelevant TCP field |
| B | Added `StandardScaler` | ~0.31 (looks worse) | Yes — a real, if partial, attack-enriched cluster |
| C | Added protocol/service/state features | ~0.31 (unchanged) | Same as B — more features, no more insight |
| D | Asked for 9 groups instead of 2 | ~0.38 (modest) | Yes — two genuinely clean clusters (96% pure "Generic" attacks, 95% pure Normal traffic) |

## Key takeaway

The best-looking number in this project was the least trustworthy one. Scaling the data correctly, and being willing to ask a richer question than a forced binary split, mattered more than the algorithm itself.

## Limitations (read before drawing conclusions)

This is a curated research dataset (68% of it is labeled an attack — nothing like real-world traffic), K-Means finds statistical similarity rather than "maliciousness," and this is not a deployable intrusion detection system. See the notebook's own Limitations section for the full list.

## Running it yourself

Requires `pandas`, `numpy`, `matplotlib`, `seaborn`, and `scikit-learn`. Open `UNSW_Clustering_jpynb.ipynb` in Jupyter and run all cells — no GPU or special setup needed.
