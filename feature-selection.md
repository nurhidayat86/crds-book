---
layout: mathjax
math: mathjax
# date:   2025-01-01 10:05:58 +0800
title: Feature Engineering
# categories: credit risk
nav_order: 5
---

## Feature selection
Limiting the number of features in logistic regression is crucial for several reasons. firstly is to prevent overfitting. Overfitting occurs when a model is too complex, having too many parameters relative to the number of observations. This potentially makes the model to fit the noise in the training data rather than the actual underlying pattern, leading to poor generalization on new, unseen data. Secondly, having too many features can lead to multicollinearity, where features are highly correlated with each other. This correlation can distort the true relationship between features and the outcome, making the their interpretation difficult. Third, some features may cost real money. As an example, credit risk application model doesn't only rely on internal data, but also external data especially credit bureau. Therefore, limitting the number of features to the best performer ones can save operational cost.

There are various approaches to selecting meaningful features in data analysis, broadly categorized into two types: univariate and multivariate feature selection. Univariate feature selection evaluates each feature independently, using a single statistical metric to assess its performance in relation to the target label. Common techniques include: Information Value (IV), and univariate Area Under the Receiver Operating Characteristic (AUROC).

Multivariate feature selection methods assess the performance gain of a feature when it is considered in combination with other features within a model.Examples of such methods include Recurring Feature Addition (RFA) and Recurring Feature Elimination (RFE). Notably, RFA is akin to what is known in logistic regression models as stepwise logistic regression, indicating that both methods share similar methodologies. This section explores three most commonly used feature selection techniques in logistic regression model: Information Value (IV), Area Under the Receiver Operating Characteristic (AUROC), and stepwise logistic regression. 

### Invormation values (IV)
Placeholder

### Area Under the Receiver Operating Characteristic (AUROC)
Placeholder

### Stepwise logsitic regression
Placeholder

[Previous: Weight of Evidence (WoE) Transformation](./weight-of-evidence.md) | [Next: Hyperparameter Tuning](./hyperparameter-tuning.md)
