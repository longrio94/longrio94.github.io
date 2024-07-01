---
title: 'Feature Engineering: From Groundwork to Greatness'
date: 2024-06-30
permalink: /posts/2024/07/blog-post-4/
tags:
  - CreditRiskModel
  - MachineLearning
  - FeatureEngineering
---

⏳   Work in Progress  ⏳ 
⏳     Coming Soon     ⏳



We often talk about "data-driven" models, but what does it really mean? Personally, I believe it's about leveraging the information hidden within data to build predictive and insightful models. While we often focus on the algorithms themselves, the true power of these models lies in the quality and representation of the data they learn from.


Feature engineering is the art and science of transforming raw data into meaningful features that enhance the performance, accuracy, and interpretability of machine learning models. It involves selecting, cleaning, creating, and transforming features to better represent the underlying problem and unlock the full potential of your data.


In data processing and feature engineering, we often categorize variables as numerical or categorical. This distinction enables us to apply specialized preprocessing techniques tailored to each variable type, optimizing model performance and ensuring robust predictions. 

In Python, we can streamline these processes using 'Pipeline', which facilitate seamless integration of preprocessing steps with model training, making the entire workflow more efficient and reproducible. My favourite tutorial about Pipeline in Python is [here]([url](https://www.youtube.com/watch?v=h1BnRBzYjYY&t=30s))


In this blog post, I will discuss about feature engineering techniques and the treatment:

1.  Missing Imputation
2.  Outliers (for continuous variables)
3.  Cardinality (for categorical variables)
4.  Variable Encoding
5.  Scaling
6.  Transformation
7.  (extra) Feature Creation
8.  Binning
   


# 1.  Missing Imputation


In credit risk models, or any machine learning model dealing with tabular datasets, we frequently encounter the challenge of missing data. But what exactly is missingness, and why does it matter? What are the different types and their unique characteristics? Most importantly, how can we effectively address this issue to ensure the accuracy and reliability of our models?


Missingness refers to the absence of data values in a dataset, and it can manifest in various forms. Broadly, missing data can be categorized as either ***informative*** or ***non-informative***, indicating whether the absence of data itself carries meaningful information. Within these categories, there are three specific types of missingness: ***MCAR (Missing Completely at Random)***, ***MAR (Missing at Random)***, and ***MNAR (Missing Not at Random)***. The summary table to understand more about Missingness in Credit Risk context:


![image](https://github.com/longrio94/longrio94.github.io/assets/37896699/39287277-b61c-43fb-9398-cf96596e3c54){: .align-middle width="1000px"}



***Non-Informative Missing***: The absence of data is unrelated to the underlying value. A random typo in a credit report and data entry errors wouldn't necessarily reflect the borrower's likelihood and ability to repay a loan.

***Informative Missing***: The absence of data itself provides valuable information about the missing value. For instance, in credit risk, borrowers who anticipate default might intentionally omit negative financial information. This missingness is related to the borrower's creditworthiness.

***MCAR (Missing Completely at Random)***: The missingness is entirely random and unrelated to any observed or unobserved variables. Think of a survey respondent accidentally skipping a question on their income.

***MAR (Missing at Random)***: The missingness depends on observed data but not on the missing values themselves. For example, younger borrowers might be less likely to have a long credit history, resulting in missing values for certain credit-related variables.

***MNAR (Missing Not at Random)***: The missingness is related to the missing values themselves. In credit risk, borrowers with a history of default might be less likely to report it.


Different types of missingness demand tailored approaches, based on their unique characteristics, to ensure the integrity and accuracy of your credit risk models. Let's explore the  treatments and the reasoning behind them:


### Non-Informative Missing (MCAR): K-Nearest Neighbors (KNN) Imputation

KNN imputation leverages the power of similarity to fill in missing values. It works by identifying the 'k' most similar complete instances (neighbors) to the one with missing data, based on the values of other features. The missing value is then estimated as a weighted average or the most frequent value (for categorical data) of its neighbors. For instance, if k=10, KNN will use the information from the 10 nearest neighbors to fill in the missing value.


Since MCAR missingness is random, the missing values are assumed to be similar to the observed values in the same feature. KNN imputation effectively exploits this assumption by borrowing information from similar (nearest) instances.



### Missing at Random (MAR): MissForest Imputation

MissForest is a non-parametric imputation method that employs random forests to predict missing values. It is also known as Regression imputation. It iteratively builds multiple random forest models, using the observed data to predict the missing values and then using the imputed values to improve the predictions in subsequent iterations.


MissForest's strength lies in its ability to capture complex relationships and interactions between variables, making it suitable for MAR scenarios where the missingness depends on observed data.


### Missing Not at Random (MNAR): Multiple Imputation by Chained Equations (MICE)


MICE is a flexible and powerful imputation method that handles missing data by creating multiple plausible imputed datasets. Each dataset is then analyzed separately, and the results are combined to account for the uncertainty due to missingness. MICE shows advantages for its flexibility in handling missing data, reducing bias estimate, and enhancing parameter estimate accuracy.


MICE is well-suited for MNAR scenarios where the missingness mechanism is complex and depends on the missing values themselves. By creating multiple imputations, MICE captures the variability and uncertainty associated with the missing data, leading to more robust and reliable estimates.







⏳ (TBC) ⏳
