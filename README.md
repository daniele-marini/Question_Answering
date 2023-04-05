# Question_Answering
Project work for the "Natural Language Processing" course of the Artificial Intelligence Master's Degree at University of Bologna.

Given a context, the Question Answering task include:
* understanding of some questions related to the context
* providing relevant answers

and in order to do this, it is necessary to extract relevant informations from the given source and generate appropriate responses.

# Authors
* Daniele Marini
* Davide Brescia
* Iulian Zorila

# Dataset
For the project we used the  CoQA (Conversational Question Answering) dataset.
Each element of the dataset contains a text (e.g. an article) and a set of conversations (question/answers). The main challenge of the dataset is that some questions don't refer directly to the context but to the previous conversations (which will be referred to as history).
Here an example of conversation:
![image](https://github.com/DANIELEMARINI99/Question_Answering/blob/main/CoQa-conversation.png)

# Models
We levereged on the HuggingFace library to use Transformers, composing an Encoder-Decoder architecture. In particular we employed:
* Bert-tiny
* DistilRoBERTa base
After loading the pretrained models, they were fine-tuned for 3 epochs using the Colab GPU. Bert-tiny required around 30 minutes, while DistilRoBERTa being significantly heavier in terms of paramaters (Encoder: 82,118,400 | Decoder: 96,353,625 vs Bert-tiny Encoder: 4,385,920 | Decoder: 4,549,306), takes more than 2 hours.

# Evaluation
The models were evaluated using the SQUAD-F1 metric:
* Bert-tiny reached:
    * Without history: 0.1843 Test set - 0.1823 Validation set
    * With history:    0.1915 Test set - 0.1848 Validation set
* DistilRoBERTa base reached:
    * Without history: 0.4596 Test set - 0.4472 Validation set
    * With history:    0.5105 Test set - 0.4918 Validation set
Whereby history includes the last 3 conversations (3 question/answer pairs).

# Conclusion
Despite the models being inadequate for Seq2Seq generation, as they are designed to work better as encoders, rather than decoders, we still obtained acceptable results with DistilRoBERTa, although we fine-tuned only for 3 epochs.
