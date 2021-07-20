# Social Capital
## Predicting the Return on Investment (ROI) of Crowd-Funded Loans

#### 2021 Update:

Effective December 31, 2020, Lending Club has retired the loan investment platform for individual investors. As a result, the models trained here can no longer be integerated with API calls to programmatically invest in new loans and no new data will be released. However, I will be continuing to use this dataset to experiment and expand my machine learning expertise. Some of the ideas I'm currently exploring:

* Writing custom, asymmetric loss functions to penalize models more for overprediction than underprediction of ROI in the hopes of seeing improved portfolio performance

* New boosting model types, including CatBoost and LightGBM

* Ensembling of boosting models

* SHAP value analysis for model interpretability

* GPU acceleration, both for model training and SHAP analysis


_________________________

## Table of Contents
_________________________

1. [Background](#background)
2. [Loan Data](#data)


## Background

The stock market has it's purpose, but wouldn't you enjoy investing your money in real people? That is the goal of crowd-funded loans issued by [LendingClub](https://www.lendingclub.com/). Here's how it works:

> Bob comes to Lending Club with \\$20,000 in credit card debt. He's paying an interest rate of 40% on this debt. However, Lending Club's non-traditional credit model decides Bob can be loaned money at 15% instead. Lending Club offers Bob a $20,000 loan to pay off his credit card debt. However, this loan is not funded by the company itself. This loan will be crowd-funded by investors.

Investors on the Lending Club platform can "invest" to fund Bob's loan. You invest by funding a portion of the loan, and then you receive payments as he pays off the loan. However, if he defaults on his loan you lose your portion of the unpaid balance.

This scenario is a win for both the borrower and the investors. Bob gets to pay off his debt at a lower interest rate, saving thousands in interest payments and penalties. Investors win by (hopefully) earning a significant return on their investment.

Investors don't want to lose money though, so can we train a machine learning algorithm to predict the return on investment of a LendingClub loan? This would allow us to avoid loans that are going to offer low or negative returns. 

## Loan Data

Lending Club had previously made all of their loan issuance and loan payments data public. 

Lending Club changed their credit model in response to loan defaults caused by "The Great Recession" in 2008. As a result, I have chosen to use only those loans issued in January 2010 or later. I have also chosen to exclude 60 month loans and focus on the 36 month loans, as there are more completed loans available to train on. In the future I will expand this analysis to include 60 month loans. 

This results in:

* 1,894,891 total loans
* 

| Feature Name        | Description                                                                          |
|---------------------|--------------------------------------------------------------------------------------|
| `loan_amnt`           | The amount being borrowed.                                                           |
| `int_rate`            | Interest rate of the loan.                                                           |
| `grade`               | What grade (A-F) has Lending Club's internal credit model assigned to this borrower? |
| `emp_length`          | How long has the borrower been employed at their current job?                        |
| `home_ownership`      | Does the borrower rent or own their home?                                            |
| `annual_inc `         | What is the borrower's annual income?                                                |
| `verification_status` | Has the borrower's self-reported income information been verified?                   |
| `purpose `            | What is the purpose of the loan?                                                     |
| `dti`                 | What is the borrower's debt-to-income ratio?                                         |
| `installment `        | Monthly payment due from borrower.                                                   |

Please see the [data dictionary](https://docs.google.com/spreadsheets/d/1d73eTwcifrFPEeMyrTd-3TjjvdDummkDu0tn_G-s7UY/edit?usp=sharing) for a full list of available features.

![Models](img/model_comparison.png)


![ROI](img/balance_vs_roi.png)
