---
id: w04-bugatha2-lasso-correlated-predictors
title: "Lasso Selection with Correlated Predictors"
author: "Krishay Bugatha (bugatha2)"
---

Suppose two predictors are highly correlated and both contain useful information for predicting the response. When fitting a lasso regression, one sample selects the first predictor and sets the second coefficient to zero, while another similar sample does the opposite. Despite this, the two models have nearly identical prediction error. Why can lasso behave this way with correlated predictors, and why does this not necessarily mean the model is unreliable for prediction?
