---
layout: mathjax
math: mathjax
# date:   2025-01-01 10:05:58 +0800
title: Weight of Evidence (WoE) Transformation
# categories: credit risk
nav_order: 7
---

# Weight of Evidence (WoE) transformation
The Weight of Evidence (WoE) is a data transformation used primarily in predictive modeling, particularly in the field of credit scoring and risk management. It quantifies the predictive strength of an individual predictor by comparing the distribution of goods (positive outcomes) to the distribution of bads (negative outcomes) within a categorical variable. The process involves segmenting the data into different groups based on the predictor, calculating the proportion of positive and negative outcomes for each group, and then evaluating how these proportions relate to each other across the groups.

To calculate the Weight of Evidence (WoE), you can follow a systematic process beginning with data grouping. For categorical variables, utilize the existing categories and consider combining those with a low number of observations into a single category. For numerical variables, the data should be binned into discrete intervals, selecting intervals that not only maximize predictive power but also maintain monotonicity to enhance model stability. Next, calculate the proportions of non-default outcomes (goods) and default outcomes (bads) within each group. Finally, compute the odds of positive outcomes relative to negative outcomes for each group, and use the mathematical formula below to determine the WoE:

$$\text{WoE} = \ln\left(\frac{\frac{G_i}{\sum G}}{\frac{B_i}{\sum B}}\right)$$

where $$G_i$$ is the number of goods in $$i$$-th group, $$G$$ is the total number of goods accross all groups, $$B_i$$ is the number of bads in $$i$$-th group, and $$B$$ is the total number of bads accross all groups. This formulation transforms the categorical predictor (the group) into a continuous variable that reflects the logarithm of the ratio of the likelihood of positive outcomes to negative outcomes for each category. The resulting WoE values are typically used to replace the original categorical values in the dataset, providing a numerical scale that is often more informative for logistic regression.

WoE offers several advantages. Firstly, it enhances predictive power by transforming categorical variables into a continuous scale that accurately reflects the strength of each predictor. This transformation is particularly beneficial in building powerful and interpretable logistic regression models. Additionally, WoE effectively handles missing values by assigning them to a unique category, allowing them to be analyzed for their predictive strength as with any regular category.

WoE addresses the challenge of rare events by calculating the log of odds, providing a robust method for dealing with categories that have few observations, which might otherwise be problematic in different encoding types. It ensures a monotonic relationship between the independent variables and the logarithm of odds of the dependent variable, a feature that enhances the effectiveness of logistic regression models.

WoE also comest with some disadvantages. One significant drawback is the potential loss of informative variations within the data, especially when many categories are merged into fewer groups, leading to information loss. Additionally, the success of WoE is heavily dependent on the binning strategy; poorly chosen bins can result in misleading WoE values and negatively impact model performance.

Another challenge is handling a large number of categories in a categorical variable can be challenging and computationally intensive when using WoE, as it requires careful consideration on how best to bin and combine these categories. There is also a risk of introducing bias with WoE, particularly if the distribution of goods and bads is not well represented across all categories, which can skew the model's outcomes. 

Additionally, while WoE is highly beneficial for logistic regression, it might not be as effective or suitable for other types of models, such as tree-based models, which inherently manage categorical variables and their interactions more effectively. These limitations highlight the need for careful implementation and consideration when using WoE in modeling scenarios.

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

## Hyperparameter tuning
Placeholder

## Evaluation

## Converting logistic regression model into a scorecard
Placeholder

[Previous: Manual Feature Interraction](./feature-interraction.md) | [Next: Feature Selection](./feature-selection.md)
