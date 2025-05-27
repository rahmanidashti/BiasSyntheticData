# Bias Evaluation in Synthetic Test Evaluation

## Experimental Setup

### Factors

#### Query Level
- __Query Words (QW)__: Number of words in query which indicate if a query is long or short
- __APL__: Average passages length for each query based on the qrels
- __QT__: Query type that indicate what is the source of the guqery generation: (1) human, (2) T5, (3) GPT4

#### Model Level
- __ST__: System Type
- __isLLM__: referes to if the pipeline contains an LLM in its model
    - This factor is highly correlated with LLM or model type factor and should not be considered.
- __MN__: No. of Model Variants, referes to the number of different models in the proposed pipeline (e.g., BM25 for retriveal, GPT-4 for ranking)

#### Document Level
- __PW__: Document Lenght: The number of tokens/words in a passage/doc

#### Factors Files
- __query_to_info__: a file from qid to query charactrsitcs
- __document_to_info__: a file from docid to passage charactristics
- __model_to_info__: a file form models to model pipeline information

## Run Evaluation
- Evaluation per query per run: We have different systems and different evaluation per query
- Based on NDCGEVAL file we can create a file that contains run_id, qid, NDCG@10, query_inof, doc_info

## Judgment Analysis
- Wrong judgments -> Query length and document length
- __Needs to be Double-Checked__:LLM prefers to give higher scores to documents that have higher length, the ones LLM prefers to give lower scores are shorter in length. This happens to both real and synthetic quereis, where the average length for when LLM prefer lower score than NIST is 20.01 and when LLM prefer higher score that NIST is 51.00.