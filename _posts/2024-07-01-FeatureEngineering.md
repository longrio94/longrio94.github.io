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


In this blog post, I will discuss about feature engineering techniques and their treatment:

1.  Missing Imputation
2.  Outliers (for continuous variables)
3.  Cardinality (for categorical variables)
4.  Variable Encoding
5.  Scaling
6.  Transformation
7.  (extra) Feature Creation
   


⏳ (TBC) ⏳

# 1.  Missing Imputation


In credit risk models, or any machine learning model dealing with tabular datasets, we frequently encounter the challenge of missing data. But what exactly is missingness, and why does it matter? What are the different types and their unique characteristics? Most importantly, how can we effectively address this issue to ensure the accuracy and reliability of our models?


Missingness refers to the absence of data values in a dataset, and it can manifest in various forms. Broadly, missing data can be categorized as either ***informative*** or ***non-informative***, indicating whether the absence of data itself carries meaningful information. Within these categories, there are three specific types of missingness: ***MCAR (Missing Completely at Random)***, ***MAR (Missing at Random)***, and ***MNAR (Missing Not at Random)***.
