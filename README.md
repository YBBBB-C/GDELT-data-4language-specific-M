# GDELT-data-4language-specific-M
pre dataset buiding work for MISCADA dissertation with OW. parallel news data in 4 target languages (en, spa, zh, er) selected from GDELT database gkg, events, and mentions which allow Google BigQuery to manipulate

## 5.7，5.14

#### todo：literature review included 3 documents -- due 23 May
1. a Literature review and Project plan, which should be in total no more than 8 pages,
2. the Ethical Assessment form (if needed for the particular project), and
3. the Risk Assessment form(discuss with supervisor)

I plan to construct a multilingual parallel corpus with a specific structure to enable more granular comparative analysis. For each source-language record, collect multiple translations in other languages. 
For example, collect 8,000 original records in Chinese (A), 8,000 in English (B), 8,000 in Spanish (C), and 8,000 in Arabic (D). Each of these source-language datasets is supposed to have translation versions in the other three languages when doing query:
	•	A (Chinese originals) will have corresponding translations:
		A1: English
	  A2: Spanish
		A3: Arabic
	•	B (English originals) will have:
		B1: Chinese
  	B2: Spanish
		B3: Arabic
	•	C (Spanish originals) will have:
		C1: Chinese
		C2: English
		C3: Arabic
	•	D (Arabic originals) will have:
		D1: Chinese
		D2: English
		D3: Spanish

From this, create derived translation sets for each language. e.g. the “translated Chinese” dataset will consist of B1, C1, and D1 (Chinese translations of content originally written in English, Spanish, and Arabic). 

This dataset is distinct from the original Chinese dataset (A) and will allow for comparative experiments.

Therefore, when storing data from each source language, I will not only retain the original text but also explicitly record its translations into other languages. 

In sum, we will generate two types of datasets for any target language like Chinese:
	1.	A native-language dataset (e.g., original Chinese texts).
	2.	A translated-language dataset (e.g., Chinese texts translated from English, Spanish, and Arabic).

idea: 
These two datasets can then be used as separate training sets for language models, allowing me to conduct experiments to analyze differences between models trained on native vs. translated text — effectively introducing an additional axis for comparison in my multilingual LLM research.


#### porblem faced and solved 
The previous Chinese and Spanish datasets set the time stamp from 2022.1.1 to 2025.1.1. When building the anchor dataset, especially for Arabic translation. 
Solution 1. dump Arabic 2. rebuild data set, set restrict 




## 4.30GCAM tags of articles
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
