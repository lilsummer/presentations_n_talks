---
layout: post
image: images/regression.png
title: A Regression Approach to Estimate Price Elasticity
sitemap: false
permalink: projects/regression
# All dates must be YYYY-MM-DD format!
date: 2019-12-01 10:02:20 +0700
keywords: "python, regression, operational research"
#   - python
#   - regression
#   - operational research
# summary: Use regression model to estimate price elsaticity -- a important indicator for dynamic pricing.
---

<p align="center"><img src="../images/regression_1.png"></p>

#### Tech stack: operational research, regression, python, dask, pyspark

Price elasticity is an economic concept widely used to measure the **change of customers’ demand in response to price changes**. I used real world customer data (sales, searches, etc) to approximate the real demand, and estimated price elasticity in regression models. Several data transformation methods were compared. By assessing price elasticity at different level of complexity, we are able to identify price-sensitive customer segments and products. The robustness and feasibility of the selected price elasticity model prototypes were evaluated. In one level, our finding resonate with the **downward-sloping assumption about price elasticity and price differentiation families (cheaper products are more elastic compared with high-end products)**. We concluded that using a specific transformation model to estimate price elasticity shows promising results and can be applied for price optimization, opportunity sizing, and product development.  
