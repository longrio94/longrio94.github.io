---
title: 'Predict Company Default'
date: 2024-07-31
permalink: /posts/2024/07/blog-post-5/
tags:
  - CreditRiskModel
  - MachineLearning
  - VariableSelection
---

This is a binary classification problem to predict company bankruptcy using data from the Taiwan
Economic Journal for the years 1999–2009. The dataset is highly imbalanced, a common characteristic
for default/bankruptcy prediction problems. All predictors in this dataset are numeric, primarily
consisting of financial indicators from financial statements. There are no missing values in this dataset.



The dataset can be accessed  [HERE]([url](https://www.kaggle.com/datasets/fedesoriano/company-bankruptcy-prediction/data))


You can access my solution [HERE]([url](https://github.com/longrio94/Company-Default-Prediction/blob/main/Bankruptcy_Prediction.pdf))



The full dataset comprises 6,819 observations with 96 predictors, which poses a "Curse of
Dimensionality" problem. Therefore, my goal is to develop a powerful model that distinguishes between
events (bankruptcies) and non-events while ensuring a robust set of variables through a comprehensive
variable selection process. I aim to achieve a model with an AUC-ROC greater than 90% on the test set
using fewer than 10 final predictors. This approach adheres to the principle of "Parsimony" and avoids
the "Curse of Dimensionality."


My Plan for Variable Selection:


1. Screening: Remove near-zero variance (NZV) and zero variance (ZV) predictors, and eliminate highly
correlated variables to reduce redundancy.

2. Filtering Method: Use automatic Weight of Evidence (WoE) binning via Decision Trees and drop
variables based on Information Value (IV).

3. Wrapper Method: Apply Recursive Feature Elimination (RFE) to perform an initial broad reduction of
the feature set. RFE quickly eliminates a large number of irrelevant features based on their
importance scores from an estimator.

4. Performance-Oriented Method: Use Backward Trimming (BART) to ensure that the final feature set is
optimized for performance, potentially addressing any multicollinearity issues or feature interactions
that RFE might not fully capture.


After the variable selection process, I will use a Random Forest classifier with hyperparameter tuning to
train the model.



In the end, the final model with only 10 variables achieved an AUC-ROC of 92% on the test set. 

The AUC-ROC on the training set was 93.45%, indicating no significant overfitting when comparing the test set and training set.
