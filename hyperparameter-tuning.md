---
layout: mathjax
math: mathjax
# date:   2025-01-01 10:05:58 +0800
title: Model Training and Hyperparameter Tuning
# categories: credit risk
nav_order: 10
---

# Model Training and Hyperparameter tuning
Model training is the process of learning the model coefficients by iteratively adjusts the parameters to better fit the model to the data. This fit is assessed by how well the predicted probabilities match the actual outcomes in the training data. Metrics like the log-loss or cross-entropy loss are commonly used to quantify the model's accuracy during training, where lower values indicate a better fit.

Hyperparameter tuning is the process of optimizing the parameters of a machine learning (ML) model that are not learned from the training data but set before the training process begins. It involves fine-tuning the model to achieve the best possible performance. Hyperparameter tuning is applicable to most ML models, including logistic regression. In complex ensemble models like bagging trees or gradient-boosted trees, the number of hyperparameters available for tuning can be large, necessitating advanced optimization techniques such as Bayesian optimization or random search to make the process efficient.

In contrast, logistic regression has a relatively small set of hyperparameters to tune, primarily related to regularization, such as the strength of L1, L2, or elastic-net penalties. Due to the limited number of options, it is feasible to test all possible combinations of hyperparameter values systematically. This approach is known as grid search, where every combination of predefined values is evaluated to identify the set of hyperparameters that yields the best model performance. While grid search is computationally intensive, it is manageable for models like logistic regression with fewer hyperparameters.

To perform grid search, we should also incorporates cross-validation to ensure the selected hyperparameters generalize well across different subsets of the data. In this process, the dataset is divided into multiple folds, and the model is trained and validated on these folds for each hyperparameter combination. The evaluation scores are averaged across the folds to account for variability and reduce the risk of overfitting to a specific subset of the data. 

Noted that, eventhough model training and hyperprameter tuning are two different concepts, both process can be done simultanously. Also, this process must be done on a train and validation set only.

[Previous: Feature Selection](./feature-selection.md) | [Next: Model Evaluation](./model-evaluation.md)