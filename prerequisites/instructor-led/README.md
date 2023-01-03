# AWS Instructor-Led Lab

> Follow the instructions given by the workshop administrators on how to log in to the AWS account provided for this workshop. Do NOT use your personal or business account to run this workshop, as the required pre-built resources will not be available.

- [Download Dataset](#download-dataset)
- [Event Engine AWS Account access](#event-engine-aws-account-access)
- [Amazon SageMaker Canvas access](#amazon-sagemaker-canvas-access)
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


## Event Engine AWS Account access

Go to: https://dashboard.eventengine.run/login. You will be redirected to the page below. 

![](/static/prerequisites/image43.png)

Enter the event hash you have received from your instructor.

![](/static/prerequisites/image44.png)

Click on **Email One-Time Password (OTP)**.

![](/static/prerequisites/image45.png)

You are redirected to the following page:

![](/static/prerequisites/image46.png)

Enter your email address and click on **Send passcode**.

![](/static/prerequisites/image47.png)

You are redirected to the following page:

![](/static/prerequisites/image48.png)

Check your mailbox, copy-paste the one-time password and click on **Sign in**.

![](/static/prerequisites/image49.png)

You are redirected to the **Team Dashboard**. Click on **AWS Console**.

![](/static/prerequisites/image50.png)

On the next screen, click on **Open AWS Console**.

![](/static/prerequisites/image51.png)

You are then redirected to the **AWS Console**.


## Amazon SageMaker Canvas access

Amazon SageMaker Canvas expands access to machine learning by providing business analysts with a visual point-and-click interface that allows them to generate accurate ML predictions on their own — without requiring any machine learning experience or having to write a single line of code.

If the AWS Account has been provisioned by your AWS Instructor, follow the next steps to access the SageMaker Studio environment:

1.  Open AWS console and switch to AWS region communicated by your instructor.

> Ireland is depicted on the image below but you can choose other region as well wherever SageMaker Canvas is available. The right region must be communicated by your instructor.

You can find the list of the AWS regions that support SageMaker Canvas [here](https://docs.aws.amazon.com/sagemaker/latest/dg/canvas.html).

![](/static/prerequisites/image22.png)

2.  Under services search for **Amazon SageMaker**.

![](/static/prerequisites/image23.png)

3.  Under the **Getting Started** panel on the left, click on **Canvas**.

![](/static/prerequisites/image41-v2.png)

4.	A SageMaker Canvas environment should already be provisioned. Click on the orange **Open Canvas** button under the pre-provisioned **sagemakeruser** user profile.

![](/static/prerequisites/image42-v2.png)

5.	The page can take 1 or 2 minutes to load when you access SageMaker Canvas for the first time.

![](/static/prerequisites/image30.png)

6.	You will be redirected to a new web page that looks like this:

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

Congratulations\!\! You have successfully completed the Prerequisites. Now, you may proceed to the next lab:

2. [ETL with Glue DataBrew](./etl-glue-databrew/)