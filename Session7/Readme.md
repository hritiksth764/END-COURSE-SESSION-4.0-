# Evaluation Metrics

# 1.  Precision for Imbalanced Classification?
Precision is a metric that quantifies the number of correct positive predictions made.

Precision, therefore, calculates the accuracy for the minority class.

It is calculated as the ratio of correctly predicted positive examples divided by the total number of positive examples that were predicted.



# 2. Precision for Binary Classification?
In an imbalanced classification problem with two classes, precision is calculated as the number of true positives divided by the total number of true positives and false positives.

-   Precision = TruePositives / (TruePositives + FalsePositives)

The result is a value between 0.0 for no precision and 1.0 for full or perfect precision.

Let’s make this calculation concrete with some examples.

Consider a dataset with a 1:100 minority to majority ratio, with 100 minority examples and 10,000 majority class examples.

A model makes predictions and predicts 120 examples as belonging to the minority class, 90 of which are correct, and 30 of which are incorrect.

The precision for this model is calculated as:

-   Precision = TruePositives / (TruePositives + FalsePositives)
-   Precision = 90 / (90 + 30)
-   Precision = 90 / 120
-   Precision = 0.75

The result is a precision of 0.75, which is a reasonable value but not outstanding.

You can see that precision is simply the ratio of correct positive predictions out of all positive predictions made, or the accuracy of minority class predictions.

Consider the same dataset, where a model predicts 50 examples belonging to the minority class, 45 of which are true positives and five of which are false positives. We can calculate the precision for this model as follows:

-   Precision = TruePositives / (TruePositives + FalsePositives)
-   Precision = 45 / (45 + 5)
-   Precision = 45 / 50
-   Precision = 0.90

						

# 3. Recall

In information retrieval, recall is the fraction of the relevant documents that are successfully retrieved.

recall = | { relevant documents } ∩ { retrieved documents } | | { relevant documents } | {\displaystyle {\text{recall}}={\frac {|\{{\text{relevant documents}}\}\cap \{{\text{retrieved documents}}\}|}{|\{{\text{relevant documents}}\}|}}}

![{\displaystyle {\text{recall}}={\frac {|\{{\text{relevant documents}}\}\cap \{{\text{retrieved documents}}\}|}{|\{{\text{relevant documents}}\}|}}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/43a4548e95fde15433d8e3cd3c80ced433f54abe)

For example, for a text search on a set of documents, recall is the number of correct results divided by the number of results that should have been returned.

In binary classification, recall is called [sensitivity](https://en.wikipedia.org/wiki/Sensitivity_and_specificity#Sensitivity "Sensitivity and specificity"). It can be viewed as the probability that a relevant document is retrieved by the query.

It is trivial to achieve recall of 100% by returning all documents in response to any query. Therefore, recall alone is not enough but one needs to measure the number of non-relevant documents also, for example by also computing the precision.


# 4. BLEU

`torchtext.data.metrics.``bleu_score`(_candidate_corpus, references_corpus, max_n=4, weights=[0.25, 0.25, 0.25, 0.25]_)

-   **candidate_corpus** – an iterable of candidate translations. Each translation is an iterable of tokens
    
-   **references_corpus** – an iterable of iterables of reference translations. Each translation is an iterable of tokens
    
-   **max_n** – the maximum n-gram we want to use. E.g. if max_n=3, we will use unigrams, bigrams and trigrams
    
-   **weights** – a list of weights used for each n-gram category (uniform by default)

**BLEU** (**bilingual evaluation understudy**) is an algorithm for [evaluating](https://en.wikipedia.org/wiki/Evaluation_of_machine_translation "Evaluation of machine translation") the quality of text which has been [machine-translated](https://en.wikipedia.org/wiki/Machine_translation "Machine translation") from one [natural language](https://en.wikipedia.org/wiki/Natural_language "Natural language") to another. Quality is considered to be the correspondence between a machine's output and that of a human: "the closer a machine translation is to a professional human translation, the better it is" – this is the central idea behind BLEU.[[1]](https://en.wikipedia.org/wiki/BLEU#endnote_Papineni2002a) BLEU was one of the first [metrics](https://en.wikipedia.org/wiki/Metric_(mathematics) "Metric (mathematics)") to claim a high [correlation](https://en.wikipedia.org/wiki/Correlation "Correlation") with human judgements of quality,[[2]](https://en.wikipedia.org/wiki/BLEU#endnote_Papineni2002a)[[3]](https://en.wikipedia.org/wiki/BLEU#endnote_Coughlin2003a) and remains one of the most popular automated and inexpensive metrics.

Scores are calculated for individual translated segments—generally sentences—by comparing them with a set of good quality reference translations. Those scores are then averaged over the whole [corpus](https://en.wikipedia.org/wiki/Text_corpus "Text corpus") to reach an estimate of the translation's overall quality. Intelligibility or grammatical correctness are not taken into account.

BLEU's output is always a number between 0 and 1. This value indicates how similar the candidate text is to the reference texts, with values closer to 1 representing more similar texts. Few human translations will attain a score of 1, since this would indicate that the candidate is identical to one of the reference translations. For this reason, it is not necessary to attain a score of 1. Because there are more opportunities to match, adding additional reference translations will increase the BLEU score.[[4]](https://en.wikipedia.org/wiki/BLEU#endnote_Papineni2002a)


# 5. BERT SCORE
BERTScore leverages the pre-trained contextual embeddings from BERT and matches words in candidate and reference sentences by cosine similarity. It has been shown to correlate with human judgment on sentence-level and system-level evaluation. Moreover, BERTScore computes precision, recall, and F1 measure, which can be useful for evaluating different language generation tasks.

For an illustration, BERTScore recall can be computed as [![](https://github.com/Tiiiger/bert_score/raw/master/bert_score.png "BERTScore")](https://github.com/Tiiiger/bert_score/blob/master/bert_score.png)
