# Logistic Regression for Binary Classification
Logistic regression is a statistical model that is commonly used for binary classification tasks. It's elegance lies in its simplicity and interpretability, making it suitable for credit risk models such as PD model. This sectione explains the mechanics behind logistic regression model including the understanding of its mathematical formula, strength and weaknesses, and why it is widely used for credit risk modelling.

## Understanding the mathematical formulation
The foundation of logistic regression lies in its ability to estimate probabilities using a logistic function, which is an S-shaped curve also known as the sigmoid function. The logistic function models the probability that the dependent variable belongs to a particular category.

For a binary classificationt ask, let $Y$ represents a binary target where $Y$ is either $1$ $(True)$ or $0$ $(False)$, and $X$ represents the features or predictor variables, a logistic regression model predicts the probability $P(Y=1|X)$ as:

$$P(Y = 1 | X) = \frac{1}{1 + e^{-(f(x))}}$$

where

$$f(x)=\beta_0 + \beta_1 X_1 + \beta_2 X_2 + \ldots + \beta_k X_k$$

, $\beta_0,\beta_1,\beta_2,...,\beta_k$ are the model coefficients, and $e$ is the natural logiarithm base. The model coffecients are learnt during the model training, which is basically solving an optimization problem of the following function:

$$\beta^* = \arg \min_{\beta} -\left[ \sum_{i=1}^n \left( y_i \log \left(\frac{1}{1 + e^{-\beta^T x_i}}\right) + (1 - y_i) \log \left(1 - \frac{1}{1 + e^{-\beta^T x_i}}\right) \right) \right]
$$

where $y_i$ is the observed binary outcome of the $i$-th observation (either 1 or 0), $x_i$ is the vector predictor variables  for the $i$-th observation, and $\beta$ is the model coefficients.

Let's leave the optimization problem and focus on the logistic regression formula. You can see from the relationship between $P(Y=1|X)$ and $f(x)$ that extremly high value of $f(X)$ will make the $P(Y=1|X)$ close to 1, and extremly low value of $f(X)$ will make the $P(Y=1|X)$ close to 0. In fact, $X$ is linear to to the log-odd probability of $Y$. Or we can also at least the relationship between $X$ and $P(Y=1|X)$ is monotonic. This is the first assumption of logistic regression model. Unfortunately, in reality, this is often not the case. Therefore, we need to transform the input variables before we can feed them into the logisti regression model for more optimum result.

The second assumption of the logistic regression model is that the predictors are independent. i.e, the values between predictors, $x_0,x_1,...,x_n$, should not be correlated. You can see from $f(X)$ that each predictor $x_i$ has its own beta coefficient $\beta_i$, and the result of $f(X)$ is basically the summation of $\beta_ix_i$. High correlation between predictor variables can lead to difficulties in estimating the model coefficients because it becomes hard to disentangle the effect of each variable.

There are also other reasonable assumption in logistic regression model such as there should be no combination of predictor variables that can perfectly predicts the binary output (quasi-complete separation), and the observation $i,i+1,i+2,...,n$, should be independent eachother. Quasi-complete separation can to problems in the estimation process, typically resulting in extremely large coefficient estimates or failure to converge.

## Strength and weaknesses of logistic regression model
One of the logistic regression's primary strengths is its interpretability; the output of a logistic regression model is a probability that gives clear insight into the relationship between the independent variables and the outcome. This interpretability extends to its coefficients, which represent the change in the log odds of the dependent variable per unit change in the predictor. This aspect makes logistic regression valuable in fields like finance, medicine, and social sciences, where understanding the influence of variables is crucial.

Another advantage of logistic regression is its simplicity and efficiency in terms of computation, particularly when compared to more complex models like neural networks or ensemble methods (including random forest and gradient boosted trees). It doesn't require high computational resources, making it suitable for situations with constrained computational capacity.

However, logistic regression also has its limitations. The assumption of linearity between the logit of the outcome and each predictor can be a drawback, as it restricts the model's ability to capture more complex relationships in the data. Additionally, as logistic regression assumes between-predictors independency, the model struggles to capture interraction between predictors.

Logistic regression also struggles with problems of multicollinearity among predictors, where high correlations between variables can destabilize the coefficient estimates, making them difficult to interpret. Another weakness is the impact of outliers and influential points, which can disproportionately affect the model due to the model's reliance on maximum likelihood estimation.

## Feature importance in logistic regression
The most straightforward method to assess feature importance in logistic regression is by examining the magnitude and sign of the model coefficients. In logistic regression, each coefficient represents the change in the log odds of the outcome for a one-unit change in the corresponding feature, assuming other variables are held constant. 

In the case of coefficient's magnitude, larger absolute values of coefficients indicate a greater impact of the corresponding feature on the outcome. A larger positive coefficient increases the log odds of the outcome, suggesting a strong positive association with the dependent variable. Conversely, a larger negative coefficient decreases the log odds, indicating a strong negative influence. 

For the sign of the coefficient (positive or negative), it indicates the direction of the association between the feature and the outcome. Positive coefficients increase the probability of the outcome occurring, while negative coefficients decrease it.

To compare the relative importance of variables that are on different scales, it is useful to look at standardized coefficients. Standardizing involves scaling the coefficients by their standard errors, which adjusts for the scale of the variables and allows for a more direct comparison across different features. This can be particularly important when dealing with variables that vary in units or range, such as comparing age in years to income in thousands of dollars.

Standardization, scaling, or transformation can also be done at the predictor level before their inclusion in the model. This will ensure every predictor has the same range. A notable method for this purpose is the Weight of Evidence (WoE) transformation, which is extensively used in credit risk modeling. WoE transformation does not only standardize the predictors. It also handles outliers, convert categorical variables into numbers, and effectively solve issues on moderate target imbalance which is commonly found in PD model development.

## Hyperparameter tuning and regularization in logistic regression
As with many predictive models including logistic regression, achieving the optimal model performance often involves fine-tuning various settings or parameters. These settings, known as hyperparameters. Hyperparameters are not directly learned from the training data, but are set prior to the learning process and affect the training process and model behavior. One part of hyperparameter tuning is determining the regularization type and strength. 

Regularization is one specific technique used in the context of predictive models to prevent overfitting and enhance model generalizability. In the case of logistic regression, there are three types regularizations: L1, L2, and elastic net.

### L1 Regularization (Lasso)
L1 regularization adds a penalty equivalent to the absolute value of the magnitude of coefficients to the objective function. This can lead to some coefficients being zeroed out, making it useful for feature selection in models with many features. The regularization term for L1 is given by:

$$Penalty_{L1} = \lambda \sum_{j=1}^{p} |\beta_j|$$

,hence the (simplified) objective function becomes

$$J(\beta) = -\left[ \sum_{i=1}^{n} \left( y_i \log(\hat{p}_i) + (1-y_i) \log(1-\hat{p}_i) \right) \right] + \lambda \sum_{j=1}^{p} |\beta_j|$$

where $\lambda$ is the L1 regularization strength, $\beta$ is the predictor, and $P$ is the number of predictors.

### L2 egularization (Ridge)
L2 regularization adds a penalty equivalent to the square of the magnitude of coefficients. This effectively shrinks the coefficients and helps to handle multicollinearity by keeping all variables in the model but penalizing their values if they are too large. The regularization term for L2 is

$$Penalty_{L2} = \lambda \sum_{j=1}^{p} \beta^2_j$$

### Elastic Net
Elastic Net combines the penalties of L1 and L2 regularization. Elastic Net aims to enjoy the benefits of both Ridge and Lasso regularization. The regularization term is

$$Penalty_{L1+L2} = r\lambda \sum_{j=1}^{p} |\beta_j| + (1-r)\lambda \sum_{j=1}^{p} \beta^2_j$$

where $r$ is the regularization ratio between L1 and L2.