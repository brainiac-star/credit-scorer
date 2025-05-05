# Compound V2 Wallet Credit Scoring

## Overview

This project builds a decentralized, AI-powered credit scoring model for Ethereum wallets interacting with the Compound V2 protocol. The system assigns scores (0–100) to wallets based solely on raw transaction behavior — no external data or labels used.

**Good behavior** → Higher score (e.g., repayments, activity, token diversity)
**Risky or exploitative usage** → Lower score (e.g., borrowing without repaying, inactivity)



##  Key Features

- Rule-based scoring using wallet activity, repayments, and liquidation patterns
- KMeans clustering for unsupervised behavior segmentation
- Hybrid scoring = rule-based + cluster-adjusted insights
- Top 1,000 scored wallets saved to CSV
- Visual analysis of score distributions and clusters
- Clean, self-contained pipeline — no external models or schema


##  Project Files
|------------------------------------------------------------------------------------------|
| File                       |                     Description                             |
|----------------------------|-------------------------------------------------------------|
| `credit_score.ipynb`       | Main notebook: data prep, features, scoring, and clustering |
| `wallet_scores_hybrid.csv` | Top 1,000 scored wallets with hybrid credit scores          |
| `methodology.md`           | Scoring logic, clustering approach, and rationale           |
| `wallet_analysis.md`       | Behavior insights for high/low scoring wallets              |
| `README.md`                | Overview and instructions                                   |
|------------------------------------------------------------------------------------------|

## Output Preview

wallet_address hybrid_score
0x1954c8cd151de0d0946fcc1e8a975... 78.69
0xd84e11bee5d555ccd905817cb8cbb... 78.55

---

## Score Distribution Insights

Rule-Based Scores: Left-skewed; most wallets are inactive or risky
Hybrid Scores: More balanced, cluster-aware, and robust

Clusters help surface trustworthy wallets while accounting for natural behavior variance.



## Deliverables Checklist

Raw transaction ingestion
Feature engineering for wallet behavior
Rule-based and cluster-based hybrid credit scoring
Top 1,000 scores exported to CSV
Markdown docs with scoring methodology and wallet analysis
Visualizations of score spread and cluster consistency

-
