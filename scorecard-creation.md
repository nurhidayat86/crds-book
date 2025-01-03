---
layout: mathjax
math: mathjax
# date:   2025-01-01 10:05:58 +0800
title: Creating Scorecard From Logistic Regression Model
# categories: credit risk
nav_order: 11
---

# Scorecard Creation
Given the complexity of statistics behind the logistic regression model, explaining feature importance directly to end users may not be the most effective approach. Instead, the model is transformed into a point-based system, known as a scorecard, which is more intuitive for users. In a scorecard, each variable is assigned a point value based on its contribution to the model, depending on its specific value. These points are then summed across all predictors included in the model to calculate the final score, making the model's output easier to understand and apply.

Converting a logistic regression model into a scorecard starts with the logistic regression formula, where the log-odds of the outcome (e.g., default vs. non-default) are modeled as a linear combination of the input features. To create a scorecard, the coefficients are rescaled into discrete points, typically by defining a base score (e.g., 600) and a scaling factor linked to a doubling or halving of odds, e.g., 50 points for doubling the odds (PDO). Each feature's contribution to the score is calculated by dividing its coefficient by the scaling factor and rounding to create scorecard-friendly values. The intervals used to calculate WoE are given specific points based on their respective coefficients. The final score for a user, as mentione dbefore, is calculated as the sum of the points from all feature contributions added to the base score. This transformation retains the predictive power of the logistic regression model while making it easier to interpret and use in decision-making.

In summary, the formulae to convert logistic regression model into a scorecard is shown as follow:

Placeholders

[Previous: Model Evaluation](./model-evaluation.md)