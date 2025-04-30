# GDELT-data-4language-specific-M
pre dataset buiding work for MISCADA dissertation with OW. parallel news data in 4 target languages (en, spa, zh, er) selected from GDELT database gkg, events, and mentions which allow Google BigQuery to manipulate


## GCAM tags of articles
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


## to do 
what to do with GCAM tag
1. Train a multi-label classifier to predict sentiment classification with GCAM
2. Constructing a Trend Chart of Sentiment Changes (Time Series)
3. Federated modeling with summary content: GCAM + Content Embedding + Summary
4. ** Calculate differences in economic discourse bias between different languages** 
