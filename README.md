# WSDM Full Paper

## Experimental Setup

### Factors

#### Query
- __Query Length (QL)__: Short or long query (TREC DL 2021 Overview Paper): Queries were split into two strata based on their length, where queries containing more than or equal to 10 words were put into the stratum corresponding to long queries and the rest of the queries were put into the stratum corresponding to short queries
- __Query Difficulty (QDx)__: Can we define it based on the number of relevant docs per query?
    - Number of Highly Relevant Passages: Count the number of passages with high relevance scores (e.g., score of 3). Fewer highly relevant passages suggest higher difficulty. 
        - The number of relevant passage / The number of qrels for the qid: higer -> low difficulty, higher -> high difficulty
        - high_relevance_count = df[df['score'] == 3].groupby('qid').size().reset_index(name='high_relevance_count')
    - Average Relevance Score: Calculate the average relevance score of all passages for a query. A lower average score indicates higher difficulty.
        - average_relevance = df.groupby('qid')['score'].mean().reset_index(name='average_score')
    - Based on real qrels (QDR)
    - Based on synthetic qrels (QDS)
- __Query Words (QW)__: Number of words in query
- __DL__: Average documents length for each query based on the qrels
- __isGPT4__ indicating if a query is generated using GPT-4 model -> updated to
    - This factor might not make sense as we are splitting the data into real vs synthetic queries, so when we are fitting the model for the analysis the factor has the same value for all the cases.
- __Synthetic__ indicates if a query is synthetic query, generated using T5 + GPT4

#### Model
- __LLM__: Model Type
- __isLLM__: referes to if the pipeline contains an LLM in its model
    - This factor is highly correlated with LLM or model type factor and should not be considered.
- __Model Params__: None!
- __No. of Model Variants:__ Referes to the number of different models in the proposed pipeline (e.g., BM25 for retriveal, GPT-4 for ranking)

#### Document
- [x] Document Lenght: The number of tokens/words in a passage/doc

### Files
- __query_to_info__: a file from qid to query charactrsitcs
- __document_to_info__: a file from docid to passage charactristics
- __model_to_info__: a file form models to model pipeline information

## Run Evaluation

- Evaluation per query per run: We have different systems and different evaluation per query
- Based on NDCGEVAL file we can create a file that contains run_id, qid, NDCG@10, query_inof, doc_info

### Discussion with Emine
- Perofrmance differecnes factor evaluation:
    - We cannot compute the performance differences on synthetic vs real queries, coz they are different
    - Can be only done on real quereis with synthetic vs nist judgments (Case 1)
    - Can be only done on synthetic quereis with synthetic vs nist judgments (Case 2)
- Plot for QL -> Box plot
- Query Difficulty based on the system performance

### Judgment Analysis

- Wrong judgments -> Query length and document length
- LLM prefers to give higher scores to documents that have higher length, the ones LLM prefers to give lower scores are shorter in length. This happens to both real and synthetic quereis, where the average length for when LLM prefer lower score than NIST is 20.01 and when LLM prefer higher score that NIST is 51.00.

## Mixed-Effect Model Analysis

- Real vs. Synthetic Judgments:
    - \+ isGPT4 (1)
    - \+ isGPT4 \+ isGPT4 * C(LLM, other) (2)

qid | isGPT4 | Score | the other factors |
--- | ------ | ----- | ----------------- |
qid1|    0   |   s1  |         XXX       |
qid2|    0   |   s2  |         XXX       |
...
qid52|   1   |   s52 |         XXX       |
qid53|   1   |   s53 |         XXX       |
...

