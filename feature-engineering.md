---
layout: mathjax
math: mathjax
# date:   2025-01-01 10:05:58 +0800
title: Feature Engineering
# categories: credit risk
nav_order: 5
---

# Feature engineering
Feature engineering involves preparing data for model training. For structured or tabular data, feature engineering can be done by transforming raw data into a format where each row corresponds to one ground truth label. This process involves aggregating values to summarize data points effectively. For numerical data, operations such as calculating the mean, median, count, sum, minimum, and maximum are common. These are often performed over specific time windows—like the last 30 days, last six months, or even the most recent values. For categorical data, we can use aggregation function such as the most recent values, the most frequent category in the last n days, the count of particular category in the last 6 months, etc. We can always be creative with how we aggragate the data.

When engineering features from data, it is crucial to avoid creating leaking features. Leaking features involve using information from ground truth labels or future data, which can falsely make the model appear highly accurate when it is not. To prevent this, ensure that the timestamp of the data used for features strictly precedes the label data snapshot. For instance, in developing a Probability of Default (PD) model for a scoring system, features should be derived from data available before the application time, while the payment default flag should only be determined after the borrowers have had some history with the lender. I also tend to avoid aggregating features from the entire lifetime of the data as it could skew the model's performance. For instance, using the total sum of expenditures on a pay-later product over its entire lifetime might not be indicative of current spending behavior, as it could reflect outdated trends.

[Previous: Target Creation](./target-creation.md) | [Next: Feature Interraction](./feature-interraction.md)
