---
layout: mathjax
math: mathjax
# date:   2025-01-01 10:05:58 +0800
title: Step 4 - Data Splitting
# categories: credit risk
nav_order: 8
---

# Data Splitting
When developing a probability of default (PD), e.g. A-score model, splitting the data into different subsets such as training, validation, test, and out-of-time samples—is crucial for several reasons:

1. Training Set: This is the main dataset used to build and train your model. It includes input-output pairs where the inputs are the features (e.g., borrower's credit score, loan amount, etc.) and the output is the target variable (e.g., default or no default). The model learns the relationship between the features and the target in this subset.

2. Validation Set: This subset is used to tune the model's hyperparameters and make decisions about which model variants (e.g., different features, different machine learning algorithms) perform best. It helps in avoiding overfitting to the training set, ensuring that the model not only learns the patterns in the training data but also generalizes well to new, unseen data.

3. Test Set: After a model has been trained and validated, the test set is used to assess its performance. This is critical because it provides an unbiased evaluation of a final model fit on the training dataset. It’s used only once, to test the model before it goes into production. This helps stakeholders understand how the model is expected to perform in the real world.

4. Out-of-Time Sample: This is a dataset collected from a different time period than the one used for the training, validation, and test datasets. The purpose of the out-of-time sample is to test the model’s performance against data shifts due to the economic environment or borrower behavior that may not be captured in the initial data splits. This is particularly important in the financial sector, where economic conditions can change rapidly, impacting the accuracy of predictions.

Splitting your dataset in these ways helps ensure that your A-score model is robust, accurate, and generalizable. It guards against overfitting (where the model performs well on the data it was trained on but poorly on any new data), and it helps in assessing the model’s effectiveness over time and across different economic conditions.

[Previous: Manual Feature Interraction](./feature-interraction.md) | [Next: Weight of Evidence (WOE) Transformation](./weight-of-evidence.md)
