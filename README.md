# BIOptimus: Pre-training an Optimal Biomedical Language Model with Curriculum Learning for Named Entity Recognition.

This repo provides our paper's model: 
BIOptimus: Pre-training an Optimal Biomedical Language Model with Curriculum Learning for Named Entity Recognition (BioNLP workshop @ ACL 2023). 
[HuggingFace](https://huggingface.co/rttl-ai/BIOptimus)
BIOptimus is a new pre-trained biomedical language model pre-trained using contextualized weight distillation and Curriculum Learning. 

![alt text](https://github.com/rttl-ai/BIOptimus/blob/main/fig2.png?raw=true)

Contextualization of tokens' embeddings leverages the ability of the BERT model to create domain-specific word embeddings that align with the corpus where they were found. 
Contextualization is performed with our resource-efficient and performant qik-find tool written in the Rust programming language. Qik-find is a purpose-built tool that finds tokens of interest and extracts corresponding sentences from a large corpus exploiting the native capability of the Rust programming language for efficient multiprocessing. 
(link to Qik-find repository).

Curriculum Learning is an easy-to-hard strategy that helps to guide the model's learning process more smoothly. We formulate our curriculum strategy from the perspective of the complexity of the prediction task. 

| v.  | **Phases** | **Masking strategy** | **Masking rate** | **Corruption strategy** |
|-----|:----------:|:--------------------:|:----------------:|:-----------------------:|
| 0.1 |   phase 1  |        tokens        |       0.15       |     with corruption     |
| 0.2 |   phase 2  |          WWM         |       0.15       |     with corruption     |
| 0.3 |   phase 3  |          WWM         |      **0.2**     |     with corruption     |
| 0.4 |   phase 4  |          WWM         |      **0.2**     |    **no corruption**    |

Different training techniques like masking rate and masking strategies help to broaden the model's experience, gain more diversified knowledge of textual input, speed up pre-training, and enhance performance on downstream tasks like NER.

Table 5
