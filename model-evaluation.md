---
layout: mathjax
math: mathjax
# date:   2025-01-01 10:05:58 +0800
title: Step 8 - Model Evaluation
# categories: credit risk
nav_order: 12
---

# Model Evaluation
When evaluating PD model, including A-score, we must, at least, consider two factors: predictive power and stability. Two most common used metrics are gini coefficient (or AUROC) for evaluating predictive  power and Population Stability Index (PSI) for evaluating the population stability. 

## Gini coefficient
Gini coefficient is basically just a different scale  of AUROC metric where

$$\text{Gini coefficient}=2*\text{AUROC}-1$$

which means when the AUROC is between 0 and 50, the gini coefficient is negative. This is very intuitive since negative gini means that the model is actually predicting the reverse direction compared to the groundtruth label.

## Population stability index
PSI, or Population Stability Index (or ), is a statistical measure used to determine the stability of data by comparing the distribution of the data used in development to its distribution in a more recent, typically operational data. This comparison helps to detect shifts or changes in the underlying population over time, which can affect the model's performance.

The PSI is calculated by segmenting the data into bins (for predictor, typically the same segments as used in WoE for variable are used) and comparing the distribution in each bin between the two datasets. For each bin, the proportion of total observations in each dataset is calculated. The PSI for each bin is then calculated by taking the difference in these proportions and multiplying it by the natural logarithm of the ratio of these proportions. The total PSI is the sum of these individual values across all bins.

The formula for PSI is:

$$PSI = \sum_{i=1}^{n} (P_{\text{actual}, i} - P_{\text{expected}, i}) \times \log\left(\frac{P_{\text{actual}, i}}{P_{\text{expected}, i}}\right)$$

Where $$𝑃_\text{actual},i$$ is the proportion of observations in bin $$i$$ in the recent or operational dataset, $$𝑃_\text{expected},i$$ is the proportion of observations in bin $$i$$ in the development dataset, and $$n$$ is the number of bins.

A PSI value close to 0 indicates no significant change in the distribution, suggesting that the model is stable. Higher values indicate changes and potential instability. Values below 0.1 typically indicate stable distributions, values between 0.1 and 0.25 suggest moderate changes, and values above 0.25 indicate significant shifts.

Note that other factors such as experimentation and marketing campaigns can influence the PSI. PSI serves as an early indicator, and shifts in data do not necessarily mean that the model will fail. Therefore, high PSI values should be interpreted with caution and considered thoughtfully.

[Previous: Model Training and Hyperparameter Tuning](./hyperparameter-tuning.md) | [Next: Creating Scorecard From Logistic Regression Model](./scorecard-creation.md)