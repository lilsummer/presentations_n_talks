---
layout: post
image: images/m5accuracy.png
title: Kaggle competition - M5 Forecasting Accuracy
sitemap: false
permalink: projects/m5accuracy
# All dates must be YYYY-MM-DD format!
date: 2020-05-20
# labels:
#   - Time series forecasting
#   - GBM
#   - Feature engineering
# summary: Kaggle solution for M5 Accuracy competition
---
<p align="center"><img src="../images/pricing.jpg"></p>

#### Tech stack: time series forecasting, GBM, feature engineering 


The goal of [**this Kaggle Competition**](https://www.kaggle.com/c/m5-forecasting-accuracy) is to use the daily sales of each goods from Walmart during 2016-2019 to predict the daily sales of next 28 days. The level of categorization including: 3 states and 3 goods categories (each category has 3 subcategory). The data provided includes prices of goods and calendar information. To identify what factors impact the sales, I explored the data by asking the following questions: 

* Interplay of prices, demands and sales
* How did feastivities and holidays impact sales? (To better understand the impact of holidays, I made a [**visualization**](https://www.kaggle.com/lilsummer877/visualize-the-effect-of-events-and-festivities))
* What kind of features can be generated to make such prediction?

After learning from other kernels, I narrowed down to several action items:

* Feature engineering on target related features (lags and rolling window lags)
* Price related features
* Calendar features

The initial analysis showed that lags and windows are particular important for the prediction. I compared the best windows and lags in this [**notebook**](https://www.kaggle.com/lilsummer877/comparison-of-rolling-window-and-lags-catboost). I then used a catboost regressor to train on the data with a 'fake' validation set (randomly sampled dataset without the consideration of time). Random search was also used to fine tuning the hyperparameters. I tested three models on the public LB and took the one with the the smallest standard deviation of the LB score for the final submission (16% final performance).

[**This post**](https://www.kaggle.com/c/m5-forecasting-accuracy/discussion/163684) outline the 1st place solution. The winning solution used similar features and light GBM with tweedie objective function. [**Tweedie**](https://arxiv.org/pdf/1811.10192.pdf) is a popular method of optimization for unbalanced and zero-inflated data. Recursive features were also used and it was proved to be robust. The idea of recursive feature generation is:

1. Use data containing lag and rolling window features from day 0, 1, ...100 to predict day 101
2. Use prediction of day 101 to generate lag and rollowing features for day 102, and predict day 102
3. Use prediction of day 102 to generate features for day 103, ... etc

