---
layout: post
image: images/conversion.jpg
title: Conversion Rate Prediction by Two-layered Stacking Model + GPU
permalink: projects/conversion
sitemap: false
# All dates must be YYYY-MM-DD format!
date: 2020-01-30 10:02:20 +0700
keywords: "machine learning, GPU, catboost"
summary: Supercharge conversion rate prediction on large volume itineraries.
---
<p align="center"><img src="../images/conversion_1.jpg"></p>
<p align="center"><img src="../images/conversion_2.jpg"></p>

#### Tech stack: python, parallel computing, GPU, pyspark

Conversion rate is essential for search content optimization. The search engine ranks the candidate items by the probability of them being clicked, which is provided by a online machine learning model that does the hard work. Predicting on millions of items within few seconds is no trivial task since both model performance and model scalability are considered. Following [**a classic design published by Facebook**](https://colab.research.google.com/drive/1B276T_uFwyqkiqyP4ha4pwdaeoNXS1N0?usp=sharing) in 2014, I took the challenge of reconstructing a model that can be used for providing such important features for the search items. 

The model is a two-layered ensemble with first gradient boosting decision tree layer and second logistic regression layer. Such design confers several advantages in creating a offline-training - online inferencing scheme: logistic regression is small sized and allows rapid inferencing, while gradient boosting tree ensures the model performance by using a large dataset in the offline training mode. In between two layers, there was a encoder to vectorize the categorical features. 

In the face of growing data size for the search items (20-30 TB/day with 20% annual increase), I chose to implement it in Catboost library on top of a Tesla P100 GPU. Catboost also enables multi-GPU mode in case there was a need to upscale the training process. To avoid the "[**curse of dimensionality**](https://en.wikipedia.org/wiki/Curse_of_dimensionality#:~:text=The%20curse%20of%20dimensionality%20refers,was%20coined%20by%20Richard%20E.)" and to reduce the training time, I also used feature selection and downsampling. Different size of training data (forward chaining cross validation) were used to ensure performance. The stacked model took about 20mins to train on a day worth of data and about 20mins to predict on the entire set of data in one hour (on a scale of 10E8 observations). The ensemble model performs better than single tree model in that the it learns both linear and non-linear relationship; it also ensures two models complement each other in some way by summing up all weights to fine a better fit (logistic regression looks for global optimal weights, while GBDT looks for local optimal weights while ensure the total loss is below a certain threshould). 

I gave a talk on this project in PyDen meetup, 2020. You can find the colab demo [**here**](https://colab.research.google.com/drive/1B276T_uFwyqkiqyP4ha4pwdaeoNXS1N0?usp=sharing), slides [**here**](https://docs.google.com/presentation/d/1WAkqvZGWKqCXzUpcMnUk0nEpHa1SnwzTlyA_1__wnwo/edit?usp=sharing).



