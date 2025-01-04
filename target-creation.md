---
layout: mathjax
math: mathjax
# date:   2025-01-01 10:05:58 +0800
title: Creating Groundtruth Labels
# categories: credit risk
nav_order: 5
---

# Target label creation
Creating target labels for binary prediction may appear straightforward, but the process can be not trivial in reality. For example, in A-score modeling, determining the definition of the ground truth label for default, such as the number of days late that constitutes default, requires careful consideration. A very short gap between the payment due date and the default designation may make the label overly sensitive, where borrowers might just forget to pay or be waiting for payday before settling their loan. Conversely, a too-wide gap can result in an imbalanced label. In summary, this process involves balancing trade-offs.

Additionally, deciding on the how long the observation window is also not trivial. Target labels are typically determined after borrowers have been on the books for a while. Many financial institutions employ a two-year performance window, meaning that ground truth labels are only confirmed 24 months after the initial snapshot of the features. This approach, while common, might not be suitable for everyone. A significant gap between the time when feature data is captured and when target labels are determined can lead to outdated or irrelevant feature data, undermining the accuracy of the model. 

## Rollrate analysis
Roll rate analysis is a technique used in credit risk management to understand how loans transition between various delinquency, i.e. days past due (DPD), stages over time. This method involves defining categories such as 'Current', '1-30 DPD', '31-60 DPD', and further stages up to 'written-off'. By collecting historical payment data, analysts create transition matrices for consecutive periods, each showing the percentage of accounts moving from one delinquency status to another. These matrices reveal patterns of account stability, deterioration, and recovery. For instance, high percentages remaining in the same category ('Current' to 'Current') indicate stable accounts, while shifts towards more severe delinquency suggest increasing credit risk. By analyzing these patterns, financial institutions can identify at what delinquency stage accounts rarely recover, establishing a data-driven definition of 'default'.

Placeholder for exaample

## Vintage analysis
One method to determine the performoce window is to use vintage analysis. Vintage analysis is an analytical technique used in credit risk modeling to assess the performance of loans across different time periods, known as vintages. A vintage in this context refers to a group of loans issued within a specific time frame, often within a particular month. The primary goal of vintage analysis is to evaluate how loans from each vintage perform over their lifetime, allowing financial institutions to determine the optimal performance window for assessing default risks. The analysis focuses on the 'loss curve' which plots the cumulative percentage of defaults or losses against the age of the loan. By examining these curves, analysts can determine how long it typically takes for the performance of a vintage to stabilize. This stabilization point is critical as it indicates when the data becomes predictive and representative of the ultimate performance of the loans.

Placeholder for example

## Overall best predictive labels
Model evaluation can also be used to determine the optimal combination of performance windows, rather than relying solely on vintage analysis to achieve a stable default rate. This approach involves training models using different performance windows, such as 4 months on book with 90 days past due (4 MOB DPD 90), 6 MOB DPD 90, 12 MOB DPD 90, and so on. By comparing the overall performance of models across these variations, the ground truth label that produces the best-performing model is selected. The rationale behind this method is that using labels with the most stable vintage does not necessarily guarantee the best model performance. Instead, optimizing model evaluation ensures a more reliable and effective outcome.

## Data Exclusion
It is crucial to exclude certain data during model development to avoid bias and undesirable model behavior. First, unless data availability is a significant issue, it is recommended to exclude borrowers with a Maturity of Book (MoB) less than the performance window of the label. For example, if utilizing a 24 MoB 90 DPD (days past due) criterion, borrowers with less than 24 MoB should be excluded. This helps mitigate bias from borrowers who are early in their MoB but may default later. Second, it is advisable to exclude data from periods of economic downturn, as during such times, borrowers who would normally not default may become defaulters. It is important to note that the criteria for data exclusion can vary among financial institutions. Therefore, always discuss any potential exclusions with the end users to ensure appropriateness and accuracy in the modeling process.

[Previous: Understanding Logistic Regression](./logistic-regression-modelling.md) | [Next: Feature Engineering](./feature-engineering.md)