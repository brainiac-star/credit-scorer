# Methodology Document – Finance Credit Scoring System

##  Objective
Build an AI-powered, explainable credit scoring model for Compound V2 wallets. Each wallet receives a score from 0 to 100 based solely on raw transaction behavior—no labels, schemas, or pretrained models are used.


##  Dataset & Preprocessing
Source: Compound V2 raw transaction-level data (JSON)
Files Used: 4 largest JSON files from the dataset
Transactions Covered: `deposit`, `borrow`, `repay`, `withdraw`, `liquidate`
Rows Flattened: ~180,000 transactions processed and cleaned



## Feature Engineering

### Wallet-Level Aggregates:
Transaction counts: deposit, borrow, repay, withdraw, liquidate
Financial stats: total USD moved, average USD value
Temporal behavior: first/last activity, active days

### Derived Behavioral Ratios:
`repay_borrow_ratio` = repay count / (borrow count + 1)
`deposit_withdraw_ratio` = deposits / (withdrawals + 1)
`liquidation_rate` = liquidations / (borrows + 1)
`activity_score` = normalized active span

### Advanced Features:
`borrow_no_repay`: binary flag (1 if borrowed but never repaid)
`unique_tokens`: number of different tokens used
`repay_usd_ratio`: total USD repaid / (USD borrowed + 1)



## Rule-Based Scoring Formula

score = (
30 * min(repay_borrow_ratio, 1)

25 * tanh(deposit_withdraw_ratio)

20 * activity_score

25 * liquidation_rate

10 * borrow_no_repay

10 * tanh(unique_tokens / 5)

10 * tanh(repay_usd_ratio)
)

# Explaination-

Each wallet gets a score out of 100 using a rule-based formula based on their transaction behavior:

+30 for repaying what they borrow (capped at a ratio of 1)

+25 for depositing more than they withdraw

+20 for being active over a long time

−25 penalty if the wallet gets liquidated

−10 penalty if the wallet borrows but never repays

+10 for using many different tokens (wallet diversity)

+10 for repaying close to the borrowed USD amount

We use tanh() to smooth out high values and avoid letting extreme numbers affect the score too much.

Produces a score between 0 and 100  
Fully explainable using symbolic logic  
Penalizes bad debt, rewards good engagement


##  Unsupervised AI: KMeans Clustering

### Clustering Setup:
Scaled features: `repay_borrow_ratio`, `deposit_withdraw_ratio`, `liquidation_rate`, `activity_score`, `avg_usd`
Algorithm: KMeans (`k=4`)
Silhouette Score: 0.617 (indicating strong cluster separation)

### Cluster Score Mapping:
We also use KMeans clustering (k=4) to group wallets by behavior. Each group gets a trust score:

Cluster 0 → 90: Very active and responsible users

Cluster 1 → 70: Stable and moderate usage

Cluster 2 → 40: Risky or mixed patterns

Cluster 3 → 50: Low activity or bot-like behavior



## Final Hybrid Score

hybrid_score = 0.6 * credit_score + 0.4 * cluster_score



Balances rule-based transparency with AI-based behavior grouping  
Reduces outlier bias and improves score fairness



##  Outputs Generated
`wallet_scores_hybrid.csv`: Top 1000 wallets with scores
`wallet_behavior_analysis.csv`: 10-wallet summary (5 high, 5 low)


## Summary
This system merges symbolic behavioral scoring with unsupervised ML to produce credit scores for DeFi users. No labels or external tools were used, and all logic was developed from raw protocol logs.
