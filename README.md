# GDELT-data-4language-specific-M
pre dataset buiding work for MISCADA dissertation with OW. parallel news data in 4 target languages (en, spa, zh, er) selected from GDELT database gkg, events, and mentions which allow Google BigQuery to manipulate


## 5.7

## 4.30 GCAM tags of articles
**(Consider using one-hot encoding)**
Recession, economic downturn
Growth and development vocabulary
Financial crisis-related terms
inflation
deflation
Terminology related to the stock market
Business confidence
Consumer confidence
Interest rates, rate hikes, interest rate cuts
Unemployment-related
Trade, import and export, customs duties
Investment, speculation, capital markets
Taxation and fiscal policy
Policy changes, regulatory changes
Subsidies, government intervention
Debt crisis, sovereign debt, default
Corruption, economic misconduct
Banking, loans
Regulatory, legal
Income disparity, wealth disparity

suggest: 
1. Instead of predicting GCAM, it is better to directly replace the GCAM function - use LLM embedding + classification to make a smarter emotion recognizer
2. Run summarisation on different language versions of the same article, then analyse what varies — is it just word choice or is there deeper bias or content difference?
3. Construct parallel data for classification model stability -->it is more important to summarize the differences in language alignment in the task
