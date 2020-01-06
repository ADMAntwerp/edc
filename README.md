# Heuristic best-first search algorithm for finding Evidence Counterfactuals (SEDC)

The SEDC algorithm is a model-agnostic heuristic best-first search algorithm for finding Evidence Counterfactuals, which are instance-level explanations for explaining model predictions of any classifier. It returns a minimal set of features so that removing these features results in a predicted class change. Removing means setting the corresponding feature value to zero. SEDC has been originally proposed [in this paper](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2282998){:target="_blank"} for explaining document classifications.

At the moment, SEDC supports binary classifiers built on high-dimensional, sparse data where a zero feature value corresponds to the absence of the feature. For instance, for behavioral data such as web browsing data, visiting an URL would set the feature value to 1, else 0. The nonzero value indicates that the behavior is present. Setting the feature value to zero would remove this evidence from the browsing history of a user. Another example is text data, where each token is represented by an individual feature. Setting the feature value (term frequency, tf-idf, etc.) to zero would mean that the corresponding token is removed from the document. 

# Explaining positively predicted instances 
An important sidenote is that the current implementation can only be used to explain positively predicted instances classified by a binary classification model. In other words, the instance you want to explain should have a probability or score that exceeds a certain threshold value (eg, 0.5 for logistic regression or 0 for SVMs).

We are currently working on a more general implementation where also the opposite is possible: explaining negatively predicted instances. For now, if you want to do so, you can use the multi-class implementation and use two binary classifiers (one for each target class). If you do this, then you can immediately explain negatively predicted instances.

# Linear implementation for finding Evidence Counterfactuals (lin-SEDC)

There is also a model-specific implementation of the algorithm for linear models: edc_linear.py. This version is more efficient than the model-agnostic implementation, however, it is less flexible to use.

# Multi-class classification tasks

We have also written an implementation that can be used for multi-class problems (e.g., problems where the target variable has more than two classes). Here, we explain why an instance is classified as a certain class. The counterfactual explanation shows the set of features that, when set to zero, the predicted class would change to another class. It is important to note that we use a one-vs-rest approach. More specifically, when there are three different classes, then we assume there are three binary trained classifier (one classifier for each target class).

# Installation

To use the SEDC explanation algorithm, save the sedc_algorithm.py and function_edc.py in the same directory and run them in an IDE of preference. Note that the default settings apply branch-and-bound in the search and return an explanation once one has been found. The feature names, classification function and threshold have to be entered by the user manually. 

To use the linear implementation, use edc_linear.py. 

To use the multi-class implementation, use SEDC_agnostic_multiclass.py and function_edc.py (same directory and run them in IDE of preference). 

# Demonstration

For an example of using the SEDC explanation algorithm on a classification model built from a behavioral data set, consider the following notebook: [Gender prediction from Movielens data](https://yramon.github.io/tutorials/Tutorial_BehavioralData_SEDC.html){:target="_blank"}.

# Licence

The SEDC explainer is patented in US US9836455B2.
