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

In Python, we can streamline these processes using 'Pipeline', which facilitate seamless integration of preprocessing steps with model training, making the entire workflow more efficient and reproducible. My favourite tutorial about Pipeline in Python is [here](https://youtu.be/h1BnRBzYjYY?si=S_nJoyggROd7vNsw)


In this blog post, I will discuss about feature engineering techniques and the treatment:

1.  Missing Imputation
2.  Outliers (for continuous variables)
3.  Cardinality (for categorical variables)
4.  Binning (Manual & Automatic)
5.  Variable Encoding
6.  Scaling
7.  Transformation
8.  (extra) Feature Creation

   


# 1.  Missing Imputation
-------


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




Here is an example of Python code to implement a robust missing imputation using a custom-built pipeline in Python:



![image](https://github.com/longrio94/longrio94.github.io/assets/37896699/f978a499-1e88-4fd4-980b-fee0ae9dd88d){: .align-middle width="800px"}<br />




# 2.  Outliers 
-------

Outliers in continuous variables are a critical consideration in data preparation and feature engineering for both credit risk and general machine learning models. Outliers are extreme or unusual values that deviate significantly from the typical patterns in the dataset. They can arise from data entry errors, rare but valid events (a billionaire's net worth), or genuine but atypical observations (a pensioner has no income but high assets).


In linear regression, outliers can severely violate the assumptions of normality and homoscedasticity (constant variance of errors). This can lead to biased parameter estimates, incorrect standard errors, and unreliable predictions, especially for new data points similar to the outliers. While machine learning models might not rely on these strict assumptions, outliers can still significantly affect their performance. Outliers can distort the patterns the model learns, leading to biased predictions, reduced ability to generalize to new data, and misleading feature importance rankings. For instance, an outlier like a billionaire's net worth could disproportionately influence a model's understanding of the relationship between wealth and credit risk. Outliers can also worsen the risk of overfitting, particularly in complex models because model may try to memorize these outliers instead of learning the generalizable patterns in the data.


To mitigate these issues, various techniques like removal, capping, and transformations can be employed. However, let's focus on two capping techniques— ***Winsorization*** and ***Robust Scaling*** —for now, as these methods maintain the number of data rows. Transformations will be discussed in a separate session.<br />



### Winsorization: 

Winsorization is a technique for handling outliers by capping them at specific percentiles, such as the 95th and 5th percentiles. Extreme values are replaced with the corresponding percentile values, retaining their relative position but potentially sacrificing information about their true magnitude. This method offers a simple way to mitigate the influence of outliers while preserving the overall dataset size.

Pseudo code of Winsorization :

if value < lower_percentile_value -> winsorized_value = lower_percentile_value <br>
else if value > upper_percentile_value -> winsorized_value = upper_percentile_value <br>
else -> winsorized_value = value <br>


Or you can use *Winsorization* from *scipy.stats*: [here](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.mstats.winsorize.html)



### Robust Scaling:

Robust scaling, on the other hand, standardizes data based on the median and interquartile range (IQR), making it less sensitive to outliers. It involves subtracting the median from each data point and then dividing by the range of IQRs (for example p75 and p25). This approach avoids discarding any data points, making it robust against extreme values without removing data points.


Pseudo code of Robust Scaling: Robust Scaling Value = (value - median) / (p75 - p25) <br>


In Python, you can use method *RobustScaler* directly from *sklearn.preprocessing*.  [here](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.RobustScaler.html)


# 3.  Cardinality 
-------
In feature engineering, high cardinality refers to categorical variables that have a large number of distinct categories or unique values. High cardinality can pose the problems of sparse data (many categories might have very few observations) and problems in subsequent steps when one-hot encoding is performed (generating many extra features).



# 4.  Binning 
-------


### Weight of Evidence (WoE) - Manual Binning



### Monotonic Optimal Binning (MoB) - Automatic Binning



⏳ (TBC) ⏳
