1. DATA COLLECTION METHOD:

Transaction data for each wallet address is retrieved from the Compound V2 or V3 protocol using on-chain data APIs (e.g., Etherscan, DeBank, or DefiLlama).

For each wallet, the following on-chain details are collected:

Total number of transactions (deposits, borrows, repayments, liquidations).

Loan-to-Value (LTV) ratio over time.

History of liquidations or near-liquidation events.

Borrowed vs. supplied asset values (collateralization).

Age of wallet and active participation in DeFi lending pools.

The data is then aggregated and stored in a structured format (e.g., JSON or CSV) for further feature engineering.

2. FEATURE SELECTION RATIONALE:

We selected features that strongly correlate with wallet reliability and risk:

Transaction Frequency – Higher frequency of deposits/repayments indicates healthier wallet activity.

Total Collateral Supplied – Higher collateral shows commitment and lower risk.

Borrow Utilization Ratio – Calculated as borrowed_amount / collateral_amount. A lower ratio indicates better risk management.

Liquidation Events – Any liquidation drastically reduces the wallet score.

Wallet Age – Older wallets with consistent activity are considered less risky.

Unique Asset Diversity – A diversified portfolio of assets reduces exposure risk.

3. SCORING METHOD:

Each feature is normalized to a 0–1 range using Min-Max scaling:

Score=1000*(value-min/max-min)
​
Weighted scoring is applied:

30% – Collateral Value

25% – Borrow Utilization Ratio (inverse scoring: lower is better)

20% – Transaction Frequency

15% – Wallet Age

10% – Asset Diversity

Penalties:

-300 points if liquidation history > 0.

-100 points for extremely high borrow utilization (>90%).

4. JUSTIFICATION OF RISK INDICATORS:

Collateralization & LTV are core risk metrics in lending protocols, as low collateral or high borrow utilization indicates potential default risk.

Transaction frequency shows active and healthy repayment behavior.

Liquidation events are a direct sign of past risky behavior.

Wallet age adds trust since long-standing wallets with no liquidations are less likely to be bots or exploit accounts.

THIS REPOSITORY CONTAINS THE WALLET_RISK_SCORE CODE AND THE WALLET SCORES WITH THE WALLET SCORES IN THE CSV FILE
