# Yeast Multilabel Classifier

## Introduction

In contrast to multi-class classification in which instances can only belong to a single class, in multi-label classification1 problems instances can belong to
more than one class at a time. For example, an image might be classified as containing all of mountains, sky, and a house or a piece of music might be classified as belonging to both the rock and jazz genres. A selection of multi-label classification approaches based on ensemble methods exist in the literature.
In this project, we have implemented a selection of multi-label classification approaches. scikit-learn base estimator implementations (e.g. decision trees, logistic regression, or support vector machine models) have been used, however, the ensemble methods have been implemented from scratch.

## Dataset

The Yeast dataset is formed by micro-array expression data and phylogenetic profiles with 2,417 included. There are 103 descriptive features per gene. Each gene is associated with a set of functional classes. In this version of the dataset there are 14 functional classes and a gene can be associated with any number of these.

The folder "data" in this repository contains the dataset in the form of a CSV file.

## Binary Relevance Classifier

A Binary Relevance Classifier has been implemented in which independent base classifiers are implemented for each label.
This uses a one-vs-all approach to generate the training sets for each base classifier. Implement

## Binary Relevance Classifier with Under-Sampling

One of the issues with the one-vs-all approach to generating training datasets used in the binary relevance algorithm is that the training
datasets for base classifiers can be very imbalanced.
The Binary Relevance Classifier is implemented with under sampling to overcome imbalance in the training data.

## Classifier Chains

One of the criticisms of the simple binary relevance classifier approach is that it does not take advantage of associations between labels in a multilabel classification scenario. For example, the presence of sea in an image increases the likelihood of a boat also being present, but decreases the likelihood of a giraffe being present.
The classifier chains algorithm is an effective multi-label classification algorithm that takes advantage of label associations. A classifier chain model generates a chain of binary classifiers each of predicts the presence or absence of a specific label. The in input to each classifier in the chain, however, includes the original descriptive features plus the outputs of the classifiers so far in the chain.[1]
This allows label associations to be taken into account.

## Reflection

Consider BR=Binary Relevance Classifier, BRUS=Binary Relevance Classifier with Under Sampling, CC=Classifier Chains.

From the above experiment we can conclude that:

BR works much better than BRUS. This is because with undersampling, relevant training samples may be lost which affect the accuracy.
BRUS gives better F1 scores for all the base models as compared to BR. Lower F1 score is an indication that the data is highly biased which means high precision and low recall. So when the data gets more balanced after undersampling, we achieve better F1 scores.
CC works better than BR and BRUS because it takes label dependency into consideration while making predictions. BR on the other hand fits and predicts independently of other labels. To my surprise, in this experiment we can obseve that CC outperforms BR only in case of RandomForest as the base model.
The performance of CC depends on the label order as while making current predictions, we consider the results and labels of previous predictions. To experiment with label ordering, random 20 label orders were used in grid search. To my observation, the results accross different runs are inconsistent pertaining to label orders. (plots included in the notebook)
In terms of complexity, BR is simple and faster as compared to CC. In terms of performance, CC has better performance than BR due to reasons mentioned above.
While dealing with the Yeast Dataset, CC works slightly better than BR which is a surprise. So, while dealing with Yeast Dataset, we can use BR as an adequate model if complexity and speed is a concern.

**Links:** [Dataset]() | [Jupyter Notebook]()

## References

[1] Read, Jesse, et al. "Classifier chains for multi-label classification." Available At: https://link.springer.com/content/pdf/10.1007/s10994-011-5256-5.pdf

NOTE: The project is WIP