# Bias Evaluation in Synthetic Test Evaluation

## Experimental Setup

### Factors

#### Query
- __Query Words (QW)__: Number of words in query which indicate if a query is long or short
- __APL__: Average passages length for each query based on the qrels
- __QT__: Query type that indicate what is the source of the guqery generation: (1) human, (2) T5, (3) GPT4

#### Model
- __LLM__: Model Type
- __isLLM__: referes to if the pipeline contains an LLM in its model
    - This factor is highly correlated with LLM or model type factor and should not be considered.

- __No. of Model Variants:__ Referes to the number of different models in the proposed pipeline (e.g., BM25 for retriveal, GPT-4 for ranking)

#### Document
- __PW__: Document Lenght: The number of tokens/words in a passage/doc

### Files
- __query_to_info__: a file from qid to query charactrsitcs
- __document_to_info__: a file from docid to passage charactristics
- __model_to_info__: a file form models to model pipeline information

## Run Evaluation

- Evaluation per query per run: We have different systems and different evaluation per query
- Based on NDCGEVAL file we can create a file that contains run_id, qid, NDCG@10, query_inof, doc_info

## Discussion with Emine
- Perofrmance differecnes factor evaluation:
    - We cannot compute the performance differences on synthetic vs real queries, coz they are different
    - Can be only done on real quereis with synthetic vs nist judgments (Case 1)
    - Can be only done on synthetic quereis with synthetic vs nist judgments (Case 2)
- Plot for QL -> Box plot
- Query Difficulty based on the system performance

## Judgment Analysis
- Wrong judgments -> Query length and document length
- __Needs to be Double-Checked__:LLM prefers to give higher scores to documents that have higher length, the ones LLM prefers to give lower scores are shorter in length. This happens to both real and synthetic quereis, where the average length for when LLM prefer lower score than NIST is 20.01 and when LLM prefer higher score that NIST is 51.00.

...

## Experiments on LLMJudge Dataset Challenge

Submission (Labeler)        |       LLM Type      |
--------------------------- | ------------------- |
llmjudge-simple3.txt        | GPT-4               | 
llmjudge-thomas3.txt        | GPT-4               | 
NISTRetrieval-instruct0.txt | Llama-3-8B-Instruct | 
Olz-exp.txt                 | GPT-4o              |  
Olz-gpt4o.txt               | GPT-4o              | 
RMITIR-llama70B.txt         | LLAMA70B-Instruct   | 
TREMA-4prompts.txt          | Llama-3-8B-Instruct | 
TREMA-direct.txt            | FLAN-T5-large       |
TREMA-rubric0.txt           | FLAN-T5-large       |