---
layout: mathjax
math: mathjax
# date:   2025-01-01 10:05:58 +0800
title: Developing Credit Risk Scorecard Using Logistic Regression
# categories: credit risk
---

# Developing Credit Risk Scorecard Using Logistic Regression
Logistic regression is a statistical model that is commonly used for binary classification tasks. It's elegance lies in its simplicity and interpretability, making it suitable for credit risk models such as PD model. 

This section explains the basic mechanics behind logistic regression, use it to develop a predictive model, and convert it into a scorecard.

## Understanding the mathematical formulation
The foundation of logistic regression lies in its ability to estimate probabilities using a logistic function, which is an S-shaped curve also known as the sigmoid function. The logistic function models the probability that the dependent variable belongs to a particular category.

For a binary classificationt ask, let $$Y$$ represents a binary target where $$Y$$ is either $$1$$ $$(True)$$ or $$0$$ $$(False)$$, and $$X$$ represents the features or predictor variables, a logistic regression model predicts the probability $$P(Y=1\|X)$$ as:

$$P(Y = 1 | X) = \frac{1}{1 + e^{-(f(x))}}$$

where

$$f(x)=\beta_0 + \beta_1 X_1 + \beta_2 X_2 + \ldots + \beta_k X_k$$

, $$\beta_0,\beta_1,\beta_2,...,\beta_k$$ are the model coefficients, and $$e$$ is the natural logiarithm base. The model coffecients are learnt during the model training, which is basically solving an optimization problem of the following function:

$$\beta^* = \arg \min_{\beta} -\left[ \sum_{i=1}^n \left( y_i \log \left(\frac{1}{1 + e^{-\beta^T x_i}}\right) + (1 - y_i) \log \left(1 - \frac{1}{1 + e^{-\beta^T x_i}}\right) \right) \right]
$$

where $$y_i$$ is the observed binary outcome of the $$i$$-th observation (either 1 or 0), $$x_i$$ is the vector predictor variables  for the $$i$$-th observation, and $$\beta$$ is the model coefficients.

Let's leave the optimization problem and focus on the logistic regression formula. You can see from the relationship between $$P(Y=1\|X)$$ and $$f(x)$$ that extremly high value of $$f(X)$$ will make the $$P(Y=1\|X)$$ close to 1, and extremly low value of $$f(X)$$ will make the $$P(Y=1\|X)$$ close to 0. In fact, $$X$$ is linear to to the log-odd probability of $$Y$$. Or we can also at least the relationship between $$X$$ and $$P(Y=1\|X)$$ is monotonic. This is the first assumption of logistic regression model. Unfortunately, in reality, this is often not the case. Therefore, we need to transform the input variables before we can feed them into the logisti regression model for more optimum result.

The second assumption of the logistic regression model is that the predictors are independent. i.e, the values between predictors, $$x_0,x_1,...,x_n$$, should not be correlated. You can see from $$f(X)$$ that each predictor $$x_i$$ has its own beta coefficient $$\beta_i$$, and the result of $$f(X)$$ is basically the summation of $$\beta_ix_i$$. High correlation between predictor variables can lead to difficulties in estimating the model coefficients because it becomes hard to disentangle the effect of each variable.

There are also other reasonable assumption in logistic regression model such as there should be no combination of predictor variables that can perfectly predicts the binary output (quasi-complete separation), and the observation $$i,i+1,i+2,...,n$$, should be independent eachother. Quasi-complete separation can to problems in the estimation process, typically resulting in extremely large coefficient estimates or failure to converge.

## Feature importance in logistic regression
The most straightforward method to assess feature importance in logistic regression is by examining the magnitude and sign of the model coefficients. In logistic regression, each coefficient represents the change in the log odds of the outcome for a one-unit change in the corresponding feature, assuming other variables are held constant. 

In the case of coefficient's magnitude, larger absolute values of coefficients indicate a greater impact of the corresponding feature on the outcome. A larger positive coefficient increases the log odds of the outcome, suggesting a strong positive association with the dependent variable. Conversely, a larger negative coefficient decreases the log odds, indicating a strong negative influence. 

For the sign of the coefficient (positive or negative), it indicates the direction of the association between the feature and the outcome. Positive coefficients increase the probability of the outcome occurring, while negative coefficients decrease it.

To compare the relative importance of variables that are on different scales, it is useful to look at standardized coefficients. Standardizing involves scaling the coefficients by their standard errors, which adjusts for the scale of the variables and allows for a more direct comparison across different features. This can be particularly important when dealing with variables that vary in units or range, such as comparing age in years to income in thousands of dollars.

Standardization, scaling, or transformation can also be done at the predictor level before their inclusion in the model. This will ensure every predictor has the same range. A notable method for this purpose is the Weight of Evidence (WoE) transformation, which is extensively used in credit risk modeling. WoE transformation does not only standardize the predictors. It also handles outliers, convert categorical variables into numbers, and effectively solve issues on moderate target imbalance which is commonly found in PD model development.

## Regularization in logistic regression
Regularization is a technique used in the context of predictive models to prevent overfitting and enhance model generalizability. In the case of logistic regression, there are three types regularizations: L1, L2, and elastic net.

### L1 Regularization (Lasso)
L1 regularization adds a penalty equivalent to the absolute value of the magnitude of coefficients to the objective function. This can lead to some coefficients being zeroed out, making it useful for feature selection in models with many features. The regularization term for L1 is given by:

$$Penalty_{L1} = \lambda \sum_{j=1}^{p} |\beta_j|$$

hence the (simplified) objective function becomes:


$$\beta^* = \arg \min_{\beta} (-\left[ \sum_{i=1}^{n} \left( y_i \log(\hat{p}_i) + (1-y_i) \log(1-\hat{p}_i) \right) \right] + \lambda \sum_{j=1}^{p} |\beta_j|)$$


where $$\lambda$$ is the L1 regularization strength, $$\beta$$ is the predictor, and $$P$$ is the number of predictors. As you can see from the penalized objective function, bigger the $$\beta$$ coefficients give bigger penalty to the function that should  be minimized by the solver.

### L2 egularization (Ridge)
L2 regularization adds a penalty equivalent to the square of the magnitude of coefficients. This effectively shrinks the coefficients and helps to handle multicollinearity by keeping all variables in the model but penalizing their values if they are too large. The regularization term for L2 is

$$Penalty_{L2} = \lambda \sum_{j=1}^{p} \beta^2_j$$

. As you can see from the regularization term, there is a quadratic term that produce stronger effect, especially when value of $$\beta$$ is high. 

### Elastic Net
Elastic Net combines the penalties of L1 and L2 regularization. Elastic Net aims to enjoy the benefits of both Ridge and Lasso regularization. The regularization term is

$$Penalty_{L1+L2} = r\lambda \sum_{j=1}^{p} |\beta_j| + (1-r)\lambda \sum_{j=1}^{p} \beta^2_j$$

where $$r$$ is the regularization ratio between L1 and L2.

## Strength and weaknesses of logistic regression model
One of the logistic regression's primary strengths is its interpretability; the output of a logistic regression model is a probability that gives clear insight into the relationship between the independent variables and the outcome. This interpretability extends to its coefficients, which represent the change in the log odds of the dependent variable per unit change in the predictor. This aspect makes logistic regression valuable in fields like finance, medicine, and social sciences, where understanding the influence of variables is crucial.

Another advantage of logistic regression is its simplicity and efficiency in terms of computation, particularly when compared to more complex models like neural networks or ensemble methods (including random forest and gradient boosted trees). It doesn't require high computational resources, making it suitable for situations with constrained computational capacity. The independency between features also helps the data scientists when they need to exclude a particular feature due to unwanted behavior.

However, logistic regression also has its limitations. The assumption of linearity between the logit of the outcome and each predictor can be a drawback, as it restricts the model's ability to capture more complex relationships in the data. Additionally, as logistic regression assumes between-predictors independency, the model struggles to capture interraction between predictors.

Logistic regression also struggles with problems of multicollinearity among predictors, where high correlations between variables can destabilize the coefficient estimates, making them difficult to interpret. Another weakness is the impact of outliers and influential points, which can disproportionately affect the model due to the model's reliance on maximum likelihood estimation.

Logistic regression, while robust and widely utilized, does not incorporate boosting, a technique often employed in more modern ensemble models like gradient boosted trees. Boosting is a powerful method that enhances model performance by iteratively focusing on the portions of the data where prediction errors are high. This targeted improvement helps in refining the model's accuracy over successive iterations.

Ensemble models that use boosting are particularly adept at handling large datasets and can effectively incorporate a greater number of predictors without a corresponding loss in performance. This capability allows these models to adapt more flexibly to complex datasets and capture subtle patterns that may be missed by simpler models like logistic regression.

In contrast, logistic regression's performance is generally constrained by its linear nature and the absence of mechanisms to iteratively refine predictions based on previous errors. As a result, while logistic regression is valuable for its interpretability and efficiency, it may not achieve the same level of accuracy as boosted ensemble models when dealing with complex or large-scale data environments. This distinction is crucial for practitioners to consider when selecting the appropriate modeling approach for their specific data and analytical needs. 

At last, developing predictive models using logistic regression usually involves more manual steps compared to developing predictivemodels using ensemble models like gradient boosted trees. Some common manual steps include introducing feature interraction, transforming predictors to align with the log-odd linearity wth the outcome, limitting the predictor variables by selecting only the best performing ones, etc. The subsequent sections explain how we can deal with the logistic regression's limitation trough manual feature interraction, WoE transformation, and feature selection.

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

## Converting logistic regression model into a scorecard
Placeholder

## Monitoring the model
Placeholder
