# Self-Paced Lab

> If you have already performed the instructions mentioned on the previous page "Option 1. AWS Instructor-Led Lab, you **DON'T** need to execute these step.

> You need to use your own AWS Account to perform the next steps. This may incur some charges.

- [Download Dataset](#download-dataset)
- [Launch Amazon SageMaker Canvas](#launch-amazon-sagemaker-canvas)
- [Amazon QuickSight access](#amazon-quicksight-access)

## Download Dataset

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

## Launch Amazon SageMaker Canvas

Amazon SageMaker Canvas is a new visual, no code capability that allows business analysts to build ML models and generate accurate predictions without writing code or requiring ML expertise. Its intuitive user interface lets you browse and access disparate data sources in the cloud or on-premises, combine datasets with the click of a button, train accurate models, and then generate new predictions once new data is available.

SageMaker Canvas leverages the same technology as Amazon SageMaker to automatically clean and combine your data, create hundreds of models under the hood, select the best performing one, and generate new individual or batch predictions. It supports multiple problem types such as binary classification, multi-class classification, numerical regression, and time series forecasting. These problem types let you address business-critical use cases, such as fraud detection, churn reduction, and inventory optimization, without writing a single line of code.

Here are the one-time steps for onboarding to Amazon SageMaker Canvas
using Quick Setup:

1.  Open AWS console and switch to AWS region you would like to use.

> **Ireland** is depicted on the image below but you can choose other region as well wherever [SageMaker Canvas is available.](https://docs.aws.amazon.com/sagemaker/latest/dg/canvas.html).

![](/static/prerequisites/image22.png)

2.  In the search bar, type **SageMaker** and click on **Amazon SageMaker**.

![](/static/prerequisites/image23.png)

3.  Click on **Amazon SageMaker Studio** (first option on the left pane).

![](/static/prerequisites/image40.png)

4.  Click on **Quick start**.

5.  Define **Name** as **sagemakeruser** for example.

![](/static/prerequisites/image52.png)

6.  Select **Create a new role** under Execution role.

![](/static/prerequisites/image53.png)

7. Keep the default and click **Create Role**.

![](/static/prerequisites/image54.png)

8. You will see that the role is successfully created.

![](/static/prerequisites/image55.png)

9. Click **Submit**.

![](/static/prerequisites/image27.png)

10.	The SageMaker Studio environment will stay in **Pending** state for a few minutes.

![](/static/prerequisites/image56.png)

11.	After a few minutes, the SageMaker Studio Domain will be provisioned. Click on **Canvas** under **Launch app** on the right of the screen.

![](/static/prerequisites/image57.png)

12.	Once Amazon SageMaker Studio is ready then click on **Open Studio**. The page can take 1 or 2 minutes to load when you access SageMaker Studio for the first time.

![](/static/prerequisites/image30.png)

13.	You will be redirected to a new web page that looks like this:

![](/static/prerequisites/image31.png)

## Amazon QuickSight access

Amazon QuickSight is a cloud-native, serverless, business intelligence with native ML integrations and usage-based pricing, allowing insights for all users.

If the AWS Account has been provisioned by your AWS Instructor, follow the next steps to sign up for QuickSight:

1.  Open AWS console and switch to AWS region communicated by your instructor.

> Ireland is depicted on the image below but you can choose other region as well wherever QuickSight is available. The right region must be communicated by your instructor.

![](/static/prerequisites/image22.png)

2.  Under services search for **QuickSight**.

![](/static/prerequisites/quicksight-01.png)

3.  Click on the button **Sign up for QuickSight**.

![](/static/prerequisites/quicksight-02.png)

4.	Keep the default selection (**Enterprise** Edition) and then click on the button **Continue**.

![](/static/prerequisites/quicksight-03.png)

5.	Provide the QuickSight account name as `workshopdemo`, and input your email address under the notification email. Keep everything else as default, and then click on **Finish** to proceed.

![](/static/prerequisites/quicksight-04.png)

6.	It can take 1 or 2 minutes to complete the sign up process. After the sign up is completed succesfully, click on the button **Go to Amazon QuickSight**.

![](/static/prerequisites/quicksight-05.png)

-----

Congratulations\!\! You have successfully completed the Prerequisites. Now, you can move on to the next lab by selecting it from the left-side menu on this page.

