# Bias Evaluation in Synthetic Test Evaluation

## Experimental Setup

### Dataset
TREC Deep Learning Track 2023

### Factors

#### Query Level: 'infos/query_to_info.txt'
- __qid__: Query ID
- __Query Length (QL)__: Indicate if query is long (1, no. of words > 10) or short (0, num. of words <= 10)
- __Query Difficulty Real (QDR)__: Qeury difficulty for real query
- __Query Difficulty Synthetic (QDS)__: Qeury difficulty for synthetic query
- __Query Word (QW)__: Number of words in the query -- indicating query length
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

## Notebooks
- [creating-files.ipynb](creating-files.ipynb): To create factors data for linear mixed-effect model analysis.
- [query-analysis.ipynb](#): To analyse the queries characteristics
- [judgement-analysis.ipynb](#): To create Bland-Altman plot
- [labels-analysis.ipynb](#): To analyse the judgements distrubutions based on the level of judge and the source
- [mixed-effect-analysis.ipynb](#):

## Cite
```
TBA
```