---
layout: mathjax
math: mathjax
# date:   2025-01-01 10:05:58 +0800
title: Step 6 - Feature Selection
# categories: credit risk
nav_order: 10
---

# Feature selection
Limiting the number of features in logistic regression is crucial for several reasons. firstly is to prevent overfitting. Overfitting occurs when a model is too complex, having too many parameters relative to the number of observations. This potentially makes the model to fit the noise in the training data rather than the actual underlying pattern, leading to poor generalization on new, unseen data. Secondly, having too many features can lead to multicollinearity, where features are highly correlated with each other. This correlation can distort the true relationship between features and the outcome, making the their interpretation difficult. Third, some features may cost real money. As an example, credit risk application model doesn't only rely on internal data, but also external data especially credit bureau. Therefore, limitting the number of features to the best performer ones can save operational cost.

There are various approaches to selecting meaningful features in data analysis, broadly categorized into two types: univariate and multivariate feature selection. Univariate feature selection evaluates each feature independently, using a single statistical metric to assess its performance in relation to the target label. Common techniques include: Information Value (IV), and univariate Area Under the Receiver Operating Characteristic (AUROC).

Multivariate feature selection methods assess the performance gain of a feature when it is considered in combination with other features within a model.Examples of such methods include Recurring Feature Addition (RFA) and Recurring Feature Elimination (RFE). Notably, RFA is akin to what is known in logistic regression models as stepwise logistic regression, indicating that both methods share similar methodologies. This section explores three most commonly used feature selection techniques in logistic regression model: Information Value (IV), Area Under the Receiver Operating Characteristic (AUROC), and stepwise logistic regression. Noted that,  similar to WoE transformation, the process of feature selection must be done on the train set only. This will prevent the model to overfit. Additionally, in reality, we will never be able to know the future data (under out of time sample).

## Information values (IV)
IV quantifies the predictive power of a feature in relation to the target variable, i.e. default/no default. The IV is calculated by taking each category or bin of a feature, determining the proportion of good and bad outcomes within each category, and then measuring how much each category contributes to distinguishing between these outcomes across the entire range of the feature. The formulae is written as follow:

$$IV = \sum_{i=1}^{n} (P_{G,i} - P_{B,i}) \cdot \log \left(\frac{P_{G,i}}{P_{B,i}}\right)$$

Where $$P_{G,i}$$ is the proportion of positive (good) outcomes in the $$i$$-th group,
$$P_{B,i}$$ is the proportion of negative (bad) outcomes in the $$i$$-th group,
and $$n$$ is the total number of groups or bins the variable has been divided into. The result is a value in the range of 0 to 1, where higher values indicate greater predictive power. An IV less than 0.02 suggests that the feature has little predictive power, while a value above 0.3 indicates a strong predictive feature.

## Area Under the Receiver Operating Characteristic (AUROC)
AUROC is area under the curve for the following plot: True Positive Rate (TPR, also known as sensitivity) on the Y-axis against the False Positive Rate (FPR, 1 - specificity) on the X-axis at various threshold settings. AUROC provides a single scalar value that summarizes the overall ability of the test to discriminate between those cases that have the condition and those that do not across all thresholds. An AUROC value of 0.5 suggests no discriminative power (equivalent to random guessing), while a value of 1.0 indicates perfect discrimination and 0.0 indicates the opposite prediction. Values between 0.5 and 1.0 indicate varying degrees of accuracy, with values closer to 1.0 demonstrating higher effectiveness of the model in distinguishing between the positive class and the negative class, and values between 0.0 to 0.5 indicates varies degrees of accuracy, with values closer to 0.0 indicates the complete opposite prediction. The AUROC is particularly useful because it is independent of the class distribution and the decision threshold, making it a powerful metric to compare the performance of different models on the same problem or for evaluating models on problems where the class distribution may shift over time.

Placeholder, AUROC graph

## Stepwise logsitic regression
Stepwise logistic regression is a method of determining the most relevant predictors for a logistic regression model. This technique iteratively adds or removes predictors based on specific criteria and tests whether these changes improve the model's performance. The most commonly used criterias are the change of AUROC or log-likelihood, correlation or Variance Inflation Factor (VIF) constrains, adjusted R-squared, etc. The stepwise method typically uses one of three approaches: forward selection, backward elimination, or a combination of both known as bidirectional elimination.

In forward selection, the process starts with no variables in the model, and adds them one by one. For each step, the variable that provides the most significant improvement to the model (often measured by the highest increase in a fit statistic like AUROC, plus a constraint like maximum correlation with other existing features) is added. This continues until adding new variables no longer provides a statistically significant improvement.

Backward elimination starts with all potential predictors in the model. At each step, the least significant variable (i.e., the one with the lowest change in AUROC) is removed from the model. This is repeated until only variables that have a statistically significant contribution to the model remain.

The goal of using stepwise logistic regression in feature selection is to produce a parsimonious model that has better generalization capabilities by including only those variables that have a significant impact on the response variable. This helps in improving the model's predictive performance.

[Previous: Weight of Evidence (WoE) Transformation](./weight-of-evidence.md) | [Next: Model Training and Hyperparameter Tuning](./hyperparameter-tuning.md)
