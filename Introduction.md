# Introduction
Welcome to the Credit Risk Data Science - Manual Book, your essential guide to the credit risk modelling. As the financial service industry evolves rapidly, employing data-driven approaches to assess credit risk has become more critical. This book aims to help you understand the data science techniques used in credit risk today, especially for developing ABC scores, ECL models, and also stress testing.

## ABC Scores
In credit risk terms, ABC scores refer to models that assess the creditworthiness of potential or existing borrowers at three different point of time. Application score (A) is the initial score used to decide whether the loan application of potential borrowers will be approved or rejected based on their data that is available at the time of application such as applicant's credit history, income, employment status, and other relevant financial information. The data can come from credit bureau, government organization, or other third party data vendors.

Once the credit is granted, behaviour (B) score comes into play. B score is mainly used to monitor and assess the borrower's creditworthiness for managing their accounts, for example by adjusting credit limits, changing interest rates, or offering alternative payment arrangements before defaults occur. B scores are also commonly used for marketing and cross selling, adjusting collection strategy, and regulatory compliance and reporting. B scores are also part of expected credit loss (ECL) model. We will go into details of ECL later.

The collection (C) score is used for accounts with payment delinquency. This score helps financial institutions prioritize their collection efforts based on the likelihood of recovering debts. Accounts with a higher likelihood of payment can be treated with less aggressive and costly collection strategies, while those with lower scores might need more focused attention.

## ECL calculation
One of the latest development of credit risk management is the adoption of ECL calculation, particularly under IFRS 9 standards. ECL calculation is used by the financial institutions to estimate the credit loss of their financial assets such as loans and bonds. The output of ECL calculation can be used as an early recognition of credit losses or to estimate profitability. Additionally, the result of ECL is also reported to the regulator.

ECL calculation, according to the IFRS 9 standards, consist of three main components: Probability of Defualt (PD), Lost Given Default (LGD), and Exposure at Default (EAD). The PD model predict the probability of a borrower will within a given time horizon. In order to calculate ECL, usually two time horizons are used depending on the asset's risk level: 12 months PD and lifetime PD.

LGD model estimates the economic loss if the default occurs, considering the recovery rates on collateral or other credit enhancements. LGD is expressed as a percentage and represents the loss rate on an exposure if a default occurs. It is calculated as the difference between the total exposure at the time of default and the recovery amount (post-recovery costs), divided by the total exposure at default.

EAD model estimates the amount that a financial institution is exposed to when a default occurs. It includes not only the outstanding balance at the time of default but also any additional amounts that may be drawn down before the default occurs, such as undrawn credit lines or committed but undrawn loans.

## Stress testing
In credit risk management, stress testing is a method to evaluate how financial instituion's operations and portfolios respond to severe but plausible adverse economic scenarios. These tests are designed to simulate the impact of various extreme conditions, such as economic downturns, market crashes, or other disruptive events. The financial institutions use stress testing to understand potential vulnerabilities and prepare for unexpected losses. 

Regulators in many countries require  financial institutions to perform regular stress tests to ensure that they can withstand economic shocks. Additionally, from the perspective of financial institutions, stress testing helps the management to make informed decisions regarding capital planning, risk appetite, and growth strategies.
