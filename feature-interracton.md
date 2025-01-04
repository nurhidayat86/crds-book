---
layout: mathjax
math: mathjax
# date:   2025-01-01 10:05:58 +0800
title: Step 3 - Manual Feature Interraction
# categories: credit risk
nav_order: 7
---

# Manual feature interraction
Manual feature interaction involves creating new features based on combinations of existing features in the data, aiming to uncover relationships that might enhance the predictive power of our predictive models. This can be particularly useful when the interaction between variables might influence the outcome in ways not captured by the individual features alone. For example, in the case of predicting payment default, income data can be combined with the existing loan amount, forming loan to income ratio (LTI). Including LTI to the model is usually make logistic regression performs better compared to including both income and existing loan amount alone to the model. 

There are several ways to introduce new features based on interraction, the method employed varies according to the type of data involved. For numerical data, new variables can be created by applying basic mathematical operations such as multiplication, division (to calculate ratios), addition, and subtraction among variables. Additionally, some practitioners employ more complex functions, such as the quadratic expression $$(a+b)^2$$, to generate new features, where $$a$$ and $$b$$ represent existing numerical variables. It is crucial, however, to select mathematical operations that are coherent with the underlying business logic. This ensures that the newly introduced features are not only statistically significant but also meaningful within the specific business context.

For categorical data such as cities, blood type, races, etc, creating new feature from interraction typically achieved by concatenation and grouping. For instance, consider a dataset with separate columns for "City" and "Ethnicity." By concatenating these columns, entries like "Singapore" from the City column and "Caucasian" from the Ethnicity column can be merged to form a new category, "Singapore_Caucasian". Following this concatenation, categories containing few data points can be grouped together. This approach helps in reducing the granularity of the data, making the dataset more manageable and potentially enhancing model performance.

[Previous: Feature Engineering](./feature-engineering.md) | [Next: Data Splitting](./data-splitting.md)