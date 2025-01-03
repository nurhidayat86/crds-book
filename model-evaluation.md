---
layout: mathjax
math: mathjax
# date:   2025-01-01 10:05:58 +0800
title: Model Evaluation
# categories: credit risk
nav_order: 11
---

# Model Evaluation
When evaluating PD model, including A-score, we must, at least, consider two factors: predictive power and stability. Two most common used metrics are gini coefficient (or AUROC) for evaluating predictive  power and Population Stability Index (PSI) for evaluating the population stability. 

## Gini coefficient
Gini coefficient is basically just a different scale  of AUROC metric where

$$\text{Gini coefficient}=2*\text{AUROC}-1$$

which means when the AUROC is between 0 and 50, the gini coefficient is negative. This is very intuitive since negative gini means that the model is actually predicting the reverse direction compared to the groundtruth label.

## Population stability index
Placeholder


[Previous: Hyperparameter Tuning](./hyperparameter-tuning.md) | [Next: Creating Scorecard From Logistic Regression Model](./scorecard-creation.md)