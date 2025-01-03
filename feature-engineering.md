---
layout: mathjax
math: mathjax
# date:   2025-01-01 10:05:58 +0800
title: Developing Predictive Model Using Logistic Regression
# categories: credit risk
nav_order: 4
---

# Developing ABC Score Using Logistic Regression
Developing a credit risk model with logistic regression involves numerous manual steps, as logistic regression does not inherently handle categorical features, lacks feature interaction, and can accommodate fewer features compared to more advanced models like gradient boosted trees. This section explains the process of building a predictive model using logistic regression, and subsequently converting it into a scorecard.

The steps to develop a model using logistic regression are outlined as follows:

1. Target label creation
2. Featue engineering
3. Manual fetaure interraction.
3. Feature transformation using Weight of Evidence (WoE).
4. Identify the most impactful features to include in the model (feature selection).
5. Adjust the model parameters to optimize performance (Hyperparameter tuning).
6. Evaluation.
7. Scorecard Creation.

Each of these steps is crucial for effectively leveraging logistic regression in predictive modeling, ensuring that the final model is both accurate and practical.

## Target label creation
Creating target labels for binary prediction may appear straightforward, but the process can be not trivial in reality. For example, in probability of default (PD) modeling, determining the definition of the ground truth label for default, such as the number of days late that constitutes default, requires careful consideration. A very short gap between the payment due date and the default designation may make the label overly sensitive, where borrowers might just forget to pay or be waiting for payday before settling their loan. Conversely, a too-wide gap can result in an imbalanced label. In summary, this process involves balancing trade-offs.

Deciding on the how long the observation window is also not trivial. Target labels are typically determined after borrowers have been on the books for a while. Many financial institutions employ a two-year performance window, meaning that ground truth labels are only confirmed 24 months after the initial snapshot of the features. This approach, while common, might not be suitable for everyone. A significant gap between the time when feature data is captured and when target labels are determined can lead to outdated or irrelevant feature data, undermining the accuracy of the model. 

### Rollrate analysis
Roll rate analysis is a technique used in credit risk management to understand how loans transition between various delinquency stages over time. This method involves defining categories such as 'Current', '1-30 days past due', '31-60 days past due', and further stages up to 'written-off'. By collecting historical payment data, analysts create transition matrices for consecutive periods, each showing the percentage of accounts moving from one delinquency status to another. These matrices reveal patterns of account stability, deterioration, and recovery. For instance, high percentages remaining in the same category ('Current' to 'Current') indicate stable accounts, while shifts towards more severe delinquency suggest increasing credit risk. By analyzing these patterns, financial institutions can identify at what delinquency stage accounts rarely recover, establishing a data-driven definition of 'default'.

Placeholder for exaample

### Vintage analysis
One method to determine the performnce window is to use vintage analysis. Vintage analysis is an analytical technique used in credit risk modeling to assess the performance of loans across different time periods, known as vintages. A vintage in this context refers to a group of loans issued within a specific time frame, often within a particular month. The primary goal of vintage analysis is to evaluate how loans from each vintage perform over their lifetime, allowing financial institutions to determine the optimal performance window for assessing default risks. The analysis focuses on the 'loss curve' which plots the cumulative percentage of defaults or losses against the age of the loan. By examining these curves, analysts can determine how long it typically takes for the performance of a vintage to stabilize. This stabilization point is critical as it indicates when the data becomes predictive and representative of the ultimate performance of the loans.

Placeholder for example

## Feature engineering
Feature engineering involves preparing data for model training. For structured or tabular data, feature engineering can be done by transforming raw data into a format where each row corresponds to one ground truth label. This process involves aggregating values to summarize data points effectively. For numerical data, operations such as calculating the mean, median, count, sum, minimum, and maximum are common. These are often performed over specific time windows—like the last 30 days, last six months, or even the most recent values. For categorical data, we can use aggregation function such as the most recent values, the most frequent category in the last n days, the count of particular category in the last 6 months, etc. We can always be creative with how we aggragate the data.

When engineering features from data, it is crucial to avoid creating leaking features. Leaking features involve using information from ground truth labels or future data, which can falsely make the model appear highly accurate when it is not. To prevent this, ensure that the timestamp of the data used for features strictly precedes the label data snapshot. For instance, in developing a Probability of Default (PD) model for a scoring system, features should be derived from data available before the application time, while the payment default flag should only be determined after the borrowers have had some history with the lender. I also tend to avoid aggregating features from the entire lifetime of the data as it could skew the model's performance. For instance, using the total sum of expenditures on a pay-later product over its entire lifetime might not be indicative of current spending behavior, as it could reflect outdated trends.

## Manual feature interraction
Manual feature interaction involves creating new features based on combinations of existing features in the data, aiming to uncover relationships that might enhance the predictive power of our predictive models. This can be particularly useful when the interaction between variables might influence the outcome in ways not captured by the individual features alone. For example, in the case of predicting payment default, income data can be combined with the existing loan amount, forming loan to income ratio (LTI). Including LTI to the model is usually make logistic regression performs better compared to including both income and existing loan amount alone to the model. 

There are several ways to introduce new features based on interraction, the method employed varies according to the type of data involved. For numerical data, new variables can be created by applying basic mathematical operations such as multiplication, division (to calculate ratios), addition, and subtraction among variables. Additionally, some practitioners employ more complex functions, such as the quadratic expression $$(a+b)^2$$, to generate new features, where $$a$$ and $$b$$ represent existing numerical variables. It is crucial, however, to select mathematical operations that are coherent with the underlying business logic. This ensures that the newly introduced features are not only statistically significant but also meaningful within the specific business context.

For categorical data such as cities, blood type, races, etc, creating new feature from interraction typically achieved by concatenation and grouping. For instance, consider a dataset with separate columns for "City" and "Ethnicity." By concatenating these columns, entries like "Singapore" from the City column and "Caucasian" from the Ethnicity column can be merged to form a new category, "Singapore_Caucasian". Following this concatenation, categories containing few data points can be grouped together. This approach helps in reducing the granularity of the data, making the dataset more manageable and potentially enhancing model performance. 

## Weight of Evidence (WoE) transformation
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

[Previous: Understanding Logistic Regression](./logistic-regression-modelling.md) | [Next: Developing Predictive Model Using Logistic Regression](./modelling-lr.md)
