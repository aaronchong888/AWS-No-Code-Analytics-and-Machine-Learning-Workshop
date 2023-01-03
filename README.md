# AWS - No-code Analytics and Machine Learning Workshop

Business users that want to do analytics and machine learning do not need to start learning a coding class: Amazon Web Services provides no-code tools and technology to allow for data preparation, model training, and data visualization - without writing a single line of code. In this workshop, we will go through the workflow of a business analysts, from applying ETL to data, to training and analyzing the model, to visualizing prediction in a BI dashboard.

## Overview

In this lab, we assume the role of a marketing analyst in the marketing department of a mobile phone operator. We have been tasked with identifying customers that are potentially at risk of churning. We have access to service usage and other customer behavior data, and want to know if this data can help explain why a customer would leave. If we can identify factors that explain churn, then we can take corrective actions to change predicted behavior, such as running targeted retention campaigns, etc.

## Architecture

![architecture](/static/shared/architecture.png)

## Dataset

For our dataset, we use a synthetic dataset from a telecommunications mobile phone carrier. You can download it: [here](https://sagemaker-sample-files.s3.amazonaws.com/datasets/tabular/synthetic/churn.csv).

This sample dataset contains 5,000 records, where each record uses 21 attributes to describe the customer profile. The attributes are as follows:

| Field      | Description |
| ----------- | ----------- |
| **State**      | The US state in which the customer resides, indicated by a two-letter abbreviation; for example, OH or NJ     |
| **Account Length**  | The number of days that this account has been active        |
| **Area Code** | The three-digit area code of the customer’s phone number        |
| **Phone** | The remaining seven-digit phone number       |
| **Int’l Plan** | Whether the customer has an international calling plan (yes/no)       |
| **VMail Plan** | Whether the customer has a voice mail feature (yes/no)       |
| **VMail Message** | The average number of voice mail messages per month       |
| **Day Mins** | The total number of calling minutes used during the day       |
| **Day Calls** | The total number of calls placed during the day       |
| **Day Charge** | The billed cost of daytime calls       |
| **Eve Mins, Eve Calls, Eve Charge** | The billed cost for evening calls       |
| **Night Mins, Night Calls, Night Charge** | The billed cost for nighttime calls       |
| **Intl Mins, Intl Calls, Intl Charge** | The billed cost for international calls       |
| **CustServ Calls** | The number of calls placed to customer service       |
| **Churn?** | Whether the customer left the service (true/false)       |

The last attribute, **Churn?**, is the attribute that we want the ML model to predict. The target attribute is binary, meaning our model predicts the output as one of two categories (True or False).

## Lab time!

1. [Prerequisites](./prerequisites/)
2. [ETL with Glue DataBrew](./etl-glue-databrew/)
3. [Model training with SageMaker Canvas](./ml-sagemaker-canvas/)
4. [Dashboarding with Amazon Quicksight](./dashboarding-quicksight/)
5. [Resources clean-up](./cleanup/)