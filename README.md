# GDELT-data-4language-specific-M
pre dataset buiding work for MISCADA dissertation with OW. news dataset in 4 target languages (en, spa, zh, er) selected from GDELT database gkg, events, and mentions which allow Google BigQuery to manipulate


## 6.20
As suggested in the last meeting, the t-SNE figure is not performing well, needs a manual check
（Loads two sets of sentence embeddings — one for the translated Chinese text (label = 0), and one for the original English text (label = 1).
Stacks the two embedding arrays into a single array for comparison.Calculates the pairwise cosine distance between all embeddings. The diagonal is set to infinity to avoid comparing a sentence with itself.

1.change machine translation model to facebook/nllb-200-distilled-600M (the former one has bias issue)

|Extractive Summarization |vs|       Abstractive Summarization|
|https://arxiv.org/abs/1908.08345  ：Text Summarization with Pretrained Encoders||
|BERTSUM|T5, BART, PEGASUS|




## 6.3  6.11
code see zh_en.ipynb

Used LaBSE (sentence transformer) instead of the XLM model for embedding 

Evaluate whether machine translation contents have a **deviation** from the original English news in the semantic space
| group | content         | language  | source         | purpose                |
| -- | --------- | -- | ----------- | ------------------ |
| A  | original en news    | en | en sourse article    | baseline/semantic distribution  |
| B  | zh->en  | en | chinese news+machien translation | Check for distribution drift |

1.  Helsinki-NLP/opus-mt-zh-en model for translation 
2.  Generate English semantic embeddings for two groups
3.  Merge them into one dataframe
4.  Dimensional reduction + visual analysis【Can use: ·t-SNE / UMAP for embedding dimensionality reduction · Use color = source to visualize "whether it is divisible" If it can be separated (A and B gather in different regions) 】

c if the model detects that the semantic distribution of the machine-translated corpus and the native corpus is different ➝ Existing bias

### files
zh7k5_with_clean_content.csv
zh7k5_with_embeddings.parquet
。。。

### tbd
abstract 1. generative abstract 2. extractive (no training)

## 5.28

Based on the completed data acquisition, I have obtained four cleaned datasets: 
1. es7k5_with_content.csv
2. ar7k5_with_clean_content.csv
3. en7k5_with_clean_content.csv
4. zh7k5_with_clean_content.csv.
 The next steps involve generating semantic embeddings and evaluating cross-lingual similarity.  I plan to use the XLM-RoBERTa Base model (from sentence-transformers) for its robust multilingual capabilities across 100+ languages, suitable for sentence-level embeddings.

·Planned Workflow:
1. Embedding Generation:
Load each dataset (Chinese, English, Spanish, Arabic).
Use sentence-transformers/xlm-r-bert-base-nli-stsb-mean-tokens to encode news content into embeddings.
2. Semantic Similarity Measurement:
Compute cosine similarity between embeddings across languages.
Test case: Select a Chinese news article, find the most similar Spanish article, and manually verify semantic alignment.
Reverse test: Start with an Arabic article and identify the closest English article.
3. Validation Experiments (plan）:
E1: Rank top-5 similar Chinese-Spanish article pairs by embedding similarity and manually assess content similarity.
E2: Check if articles with shared themes (e.g., “stock market decline”) cluster closely across languages in the embedding space. --KNN
E3: Compare XLM-RoBERTa Base results with LaBSE to evaluate consistency in language-agnostic semantic encoding.
Per Prof. Philip’s advice: “Encode articles from different languages and check if they land near each other in vector space.” This suggests directly encoding all articles, measuring embedding proximity, and validating semantic similarity by reviewing original content.

Next
Implement embedding generation with XLM-RoBERTa **Base**.
Conduct similarity tests and validation experiments.
Prepare findings for discussion, focusing on whether embeddings capture language-agnostic semantics.



















## 5.7，5.14


IDEA-CCNL/Erlangshen-Roberta-110M-Sentiment

shibing624/text2vec-base-chinese
#### todo：literature review included 3 documents -- due 23 May
1. a Literature review and Project plan, which should be in total no more than 8 pages,
2. the Ethical Assessment form (if needed for the particular project), and
3. the Risk Assessment form(discuss with supervisor)

I plan to construct a multilingual parallel corpus with a specific structure to enable more granular comparative analysis. For each source-language record, collect multiple translations in other languages. 
For example, collect 8,000 original records in Chinese (A), 8,000 in English (B), 8,000 in Spanish (C), and 8,000 in Arabic (D). Each of these source-language datasets is supposed to have translation versions in the other three languages when doing query:
1. A (Chinese originals) will have corresponding translations:
		A1: English
	  A2: Spanish
		A3: Arabic
2. B (English originals) will have:
		B1: Chinese
  	B2: Spanish
		B3: Arabic
3. C (Spanish originals) will have:
		C1: Chinese
		C2: English
		C3: Arabic
4. D (Arabic originals) will have:
		D1: Chinese
		D2: English
		D3: Spanish

From this, create derived translation sets for each language. e.g. the “translated Chinese” dataset will consist of B1, C1, and D1 (Chinese translations of content originally written in English, Spanish, and Arabic). 

This dataset is distinct from the original Chinese dataset (A) and will allow for comparative experiments.

Therefore, when storing data from each source language, I will not only retain the original text but also explicitly record its translations into other languages. 

In sum, we will generate two types of datasets for any target language like Chinese:
	1.	A native-language dataset (e.g., original Chinese texts).
	2.	A translated-language dataset (e.g., Chinese texts translated from English, Spanish, and Arabic).
 
## strategy shift
idea: 
These two datasets can then be used as separate training sets for language models, allowing me to conduct experiments to analyze differences between models trained on native vs. translated text — effectively introducing an additional axis for comparison in my multilingual LLM research.

idea quit & alt ~_~, because the free token of BigQuery was used up.

The initial plan was to construct a parallel multilingual dataset — collecting news articles about the same event in four languages (Chinese, English, Spanish, Arabic) — to evaluate the cross-lingual performance of language-agnostic LLMs.

However, after querying GDELT, it was found that the number of events covered in all four languages is extremely limited, even with a broad time range and relaxed filters. GDELT stores different reports on the same event, but they are not guaranteed to be translations or semantically equivalent across languages.

Given this limitation, the focus will shift to building balanced, domain-consistent datasets for each language separately (e.g., 8,000 finance-related articles per language). 
This allows for fair comparison of classification, summarization, and embedding behavior across languages, without relying on exact parallel content.

Parallel examples may still be used for small-scale qualitative analysis, but will not be the main dataset structure.



#### porblem faced and solved 
The previous Chinese and Spanish datasets set the time stamp from 2022.1.1 to 2025.1.1. When building the anchor dataset, especially for Arabic translation. 
Solution 1. dump Arabic 2. rebuild dataset see ‘8k’






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
