This analysis highlights 5 high-scoring and 5 low-scoring wallets based on the final hybrid credit score.

# Top 5 Wallets – Responsible Users
These wallets show strong repayment behavior, active participation, zero liquidations, and diverse token use.

`Wallet	        Score	                   Key Behavior`
0x1954...2380	78.70	Repaid loans, used 7 tokens, long activity span, zero liquidation
0xd84e...4f0d	78.55	Full repayment, stable usage, moderate token diversity
0x89ff...ca7	77.99	Active user, repayment matches borrow, high deposit/withdraw ratio
0x03e3...ba2e7	77.67	Engaged wallet, consistent repayments, high value transfers
0x7ef5...5be4	77.59	Clean usage, no risk flags, healthy ratios

# Wallet Proof Examples
Wallet: 0x1954c8cd151de0d0946fcc1e8a97545f711e2380
Repaid loans: repay_borrow_ratio = 1.0

Used multiple tokens: unique_tokens = 7

Activity over 27 days: activity_score = 0.065534

Zero liquidations: liquidation_rate = 0.0

Hybrid Score: 78.70

Bottom 5 Wallets – Risky or Inactive Users
These wallets borrowed without repaying, lacked engagement, or appeared bot-like.

`Wallet	        Score	              Key Behavior`
0x0442...4651c	16.00	Borrowed, never repaid, no token diversity
0xa8bc...1301	16.00	Only borrowed, single token, never repaid
0x67e5...1bfa	16.00	Borrow-only activity, no engagement after
0x1781...acd4	16.21	High value borrow, no repayment, slight token variation
0x967c...bc4	16.71	No repayments, limited interaction, flagged risky

This shows high scores correlate with healthy, engaged usage low scores catch wallets with no repayment or shallow behavior

The model fairly identifies good vs. risky users using both rule logic and AI

## Reason that top wallet Score Around 78
Even though the top wallets show excellent behavior — full repayments, long-term activity, zero liquidations, and multi-token engagement — they do not receive a perfect score of 100 due to the following reasons:

# Soft Capping with tanh()
Metrics like deposit/withdraw ratio and token diversity are scaled using the tanh() function. This avoids giving outsized influence to any single feature and keeps the score fair for all users.

# Capped Ratios
Ratios such as repay_borrow_ratio are capped at a maximum of 1, meaning that repaying more than borrowed doesn’t continue boosting the score infinitely.

# Cluster Score Weighting
The final score is a blend of the rule-based score and a cluster score. Even the best-performing cluster is assigned a maximum of 90, not 100, to leave room for variability and reduce overconfidence in model predictions.
 
# A high Score of 78 Mean-
A score in the high 70s or low 80s represents elite performance under a strict and explainable scoring system. It ensures fairness, avoids inflation, and distinguishes truly exceptional behavior from simply good behavior — which is important in a trust-sensitive financial system.

