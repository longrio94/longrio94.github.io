---
title: 'Uncertainty Quantification in Machine Learning: From Point to Interval'
date: 2024-06-20
permalink: /posts/2024/06/blog-post-3/
tags:
  - UncertaintyQuantification
  - CreditRiskModel
  - MachineLearning
---

⌛ coming soon Work in Progress ⌛

Uncertainty Quantification: From Point to Interval
======

Uncertainty is a crucial factor in decision-making that needs more attention when using machine learning models. In machine learning, where uncertainty is inherent and can significantly impact decision-making, Quantile Regression (QR), Conformal Prediction (CP), and Conformalized Quantile Regression (CQR) offer valuable tools to enhance model reliability and interpretability. These techniques help machine learning models evolve from providing point estimates to delivering interval estimates that capture and quantify uncertainty, thereby supporting more robust decision-making processes.

Let's explain conformal prediction in simple terms, using a real-life example that might remind you of your favorite childhood game show in Vietnam, "Hãy chọn giá đúng" (Choose the Correct Price). Remember how you had to guess the exact price of a product to win? It was a fun challenge, but wouldn't it be easier to give a price range instead? If you guessed 100,000 VND but the actual price was 102,500 VND, you'd lose. However, if you could say the price was between 100,000 VND and 105,000 VND, you'd be much more likely to win!


The model, just like us, prefers to give a range of predicted values rather than a single, absolute value. This is where the benefit of prediction intervals comes into play for decision-making. In essence, moving from point estimates to interval estimates can provide a more informative and reliable prediction.



1.Quantile Regression with LightGBM
-------

Quantile Regression (QR) is an extension of Ordinary Least Squares (OLS) linear regression. While OLS focuses on modeling the mean value of the target variable, QR goes further by modeling its entire conditional distribution. This allows QR to provide a richer and more informative picture of the relationship between variables, moving beyond the limitations of predicting only the average value.

Unlike OLS, QR focuses on different quantiles (percentiles) of the distribution, not just the mean. This makes it more robust to outliers and violations of the normality assumption, which are often present in real-world data. Consequently, QR can provide more trustworthy estimates than mean regression, making it a valuable tool for Uncertainty Quantification. In essence, QR allows us to explore the full spectrum of possible outcomes, rather than just the most likely outcome, leading to a more comprehensive understanding of uncertainty in predictive models.

For instance, imagine you're studying housing prices. OLS regression would give you the average expected price of a house based on factors like size, location, and number of bedrooms. QR, on the other hand, could tell you the expected price at different quantiles, such as the 10th percentile (representing cheaper houses) or the 90th percentile (representing more expensive houses). This is particularly valuable when making decisions that depend on understanding the full range of possible outcomes, not just the average.

LightGBM, a popular gradient boosting framework, offers a convenient way to implement quantile regression. This allows you to estimate different quantiles (e.g., 10th, 50th, 90th percentiles) of the target variable, providing a more comprehensive view of its distribution compared to traditional regression models.

**Train a quantile regression model for the 90th percentile in Python:**

model = lgb.LGBMRegressor(objective='quantile', alpha=0.9)



2.Conformal Prediction to measuring uncertainty
-------

Conformal Prediction (CP) focuses on creating reliable prediction intervals with guaranteed coverage, while Quantile Regression (QR) models the entire distribution of possible outcomes. CP's model-agnostic and distribution-free nature, meaning it can be applied to any machine learning algorithm and doesn't rely on assumptions about the underlying data distribution, makes it particularly well-suited for the diverse and often complex datasets encountered in machine learning. Thus, CP is a powerful technique for quantifying uncertainty in machine learning algorithms. Given an input, conformal prediction produces a prediction interval for regression problems, estimating a range within which the true value is likely to fall with a high probability. For classification problems, CP generates a set of possible classes, again with a high probability of containing the true class.

Imagine you're a trying to predict the selling price of a house. You've collected data on various features of houses in your area, such as square footage, number of bedrooms, and location, along with their actual selling prices. You use this data to train a machine learning model to predict house prices. Traditionally, your model might give you a single price estimate for the house, like €350,000. But with CP, you get something more informative: a prediction interval. For example, your CP model might say, "I'm 90% confident that the house will sell for between €325,000 and €375,000." This means that based on similar houses it has seen before, the model is fairly certain the true selling price falls within this range.




3.Combining Conformal Prediction and Quantile Regression (Confomalized Quantile Regression)
-------

(tbc)


