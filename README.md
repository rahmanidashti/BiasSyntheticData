# Bias Evaluation in Synthetic Test Evaluation

## Experimental Setup

### Factors

#### Query Level: 'infos/query_to_info.txt'
- __qid__:
- __Query Length (QL)__: indicate if query is long (1, no. of words > 10) or short (0, num. of words <= 10)
- __Query Difficulty Real (QDR)__:
- __Query Difficulty Synthetic (QDS)__:
- __Query Word (QW)__: number of words in the query -- indicating query length
- __Document Length (DL)__: Average passages length for each query based on the qrels
- __Synthetic__: 1 if query is synthetic (T5 or GPT-4 generated quereis)
- __isGPT4__: it is 1 if the query is GPT4-generated

#### Model Level: 'infos/model_to_info.txt'
- __ST__: System Type
- __isLLM__: referes to if the pipeline contains an LLM in its model
    - This factor is highly correlated with LLM or model type factor and should not be considered.
- __MN__: No. of Model Variants, referes to the number of different models in the proposed pipeline (e.g., BM25 for retriveal, GPT-4 for ranking)

#### Passage Level: 'infos/pass_to_info.txt'
- __PW__: Passage Lenght: The number of tokens/words in a passage

## Run Evaluation
- Evaluation per query per run: We have different systems and different evaluation per query
- Based on NDCGEVAL file we can create a file that contains run_id, qid, NDCG@10, query_inof, doc_info

## Judgment Analysis
- Wrong judgments -> Query length and document length
- __Needs to be Double-Checked__:LLM prefers to give higher scores to documents that have higher length, the ones LLM prefers to give lower scores are shorter in length. This happens to both real and synthetic quereis, where the average length for when LLM prefer lower score than NIST is 20.01 and when LLM prefer higher score that NIST is 51.00.