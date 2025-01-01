---
layout: mathjax
math: mathjax
# date:   2025-01-01 10:05:58 +0800
title: Introduction to ABC Scores and Stress Testing
# categories: credit risk
---

# Introduction to ABC Scores and Stress Testing

## ABC Scores
In credit risk terms, ABC scores refer to models that assess the creditworthiness of potential or existing borrowers at three different point of time. Application score (A) is the initial score used to decide whether the loan application of potential borrowers will be approved or rejected based on their data that is available at the time of application such as applicant's credit history, income, employment status, and other relevant financial information. The data usually originates from credit bureau, government organization, and even other third party data vendors. 

A score, is typically derived from a logistic regression model that predicts whether the borrowers will have payment defaults in a spevified time horizon or not. This type of model is known as a Payment Default (PD) model. Once the model is trained, it is then transformed into an easy-interpretable scorecard. Nowadays, due to the advancement of technology that supports data science including increased data size and better computational power, machine learning (ML) models such as random forest and gradient boosted trees are also commonly used to develop A score model.

The Behavior (B) score, like A score, is also part of Payment Default (PD) model. While the A score is used during the initial credit application process, the B score is used once a line of credit has been granted. It serves to continually monitor and assess the borrower's creditworthiness as they manage their account. This includes tasks such as adjusting credit limits, modifying interest rates, or proposing alternative payment options to prevent defaults.

Furthermore, B scores are also commonly used in the Expected Credit Loss (ECL) calculation, marketing efforts and cross-selling, tailoring collection strategies, and ensuring regulatory compliance and reporting. Due to these diverse applications, the B score is frequently updated to reflect the most recent data snapshot, ensuring that it provides a current and accurate measure of credit risk.

The collection (C) score is used for accounts with payment delinquency. This score helps financial institutions prioritize their collection efforts based on the likelihood of recovering debts. Accounts with a higher likelihood of payment can be treated with less aggressive and costly collection strategies, while those with lower scores might need more focused attention.

The C score, which is also another output of predictive model, is more closely aligned with the Loss Given Default (LGD) model rather than the Payment Default (PD) model. We will explore LGD model in more details in the section dedicated to the ECL.

## ECL calculation
One of the latest development of credit risk management is the adoption of ECL calculation, particularly under IFRS 9 standards. ECL calculation is used by the financial institutions to estimate the credit loss of their financial assets such as loans and bonds. The output of ECL calculation can be used as an early recognition of credit losses or to estimate profitability. Additionally, the result of ECL is also reported to the regulator and can influence the proportion of assets that financial institutions are permitted to loan out, impacting their lending capacity either positively or negatively.

ECL calculation, according to the IFRS 9 standards, consist of three main components: Probability of Defualt (PD), Lost Given Default (LGD), and Exposure at Default (EAD). The PD model predict the probability of a borrower will within a given time horizon. In order to calculate ECL, usually two time horizons are used depending on the asset's risk level: 12 months PD and lifetime PD.

LGD model estimates the economic loss if the default occurs, considering the recovery rates on collateral or other credit enhancements. LGD is expressed as a percentage and represents the loss rate on an exposure if a default occurs. It is calculated as the difference between the total exposure at the time of default and the recovery amount (post-recovery costs), divided by the total exposure at default.

EAD model estimates the amount that a financial institution is exposed to when a default occurs. It includes not only the outstanding balance at the time of default but also any additional amounts that may be drawn down before the default occurs, such as undrawn credit lines or committed but undrawn loans.

## Stress testing
In credit risk management, stress testing is a method to evaluate how financial instituion's operations and portfolios respond to severe but plausible adverse economic scenarios. These tests are designed to simulate the impact of various extreme conditions, such as economic downturns, market crashes, or other disruptive events. The financial institutions use stress testing to understand potential vulnerabilities and prepare for unexpected losses. 

Regulators in many countries require  financial institutions to perform regular stress tests to ensure that they can withstand economic shocks. Additionally, from the perspective of financial institutions, stress testing helps the management to make informed decisions regarding capital planning, risk appetite, and growth strategies.

[Previous: Introduction](./index.md) | [Next: Understanding Logistic Regression](./logistic-regression-modelling.md)