---
title : "Extract, Transform and Load data with AWS Glue DataBrew"
weight : 20
---

::alert[Make sure you have downloaded the dataset and performed the steps described in the **"Prerequisites"** section before beginning this lab.]{type=warning}

## Agenda

1. [Import the dataset in Glue DataBrew](#import-the-dataset-in-databrew)
1. [Define data transformation recipe](#define-the-data-transformation-recipe)
1. [Running the transformation job](#running-the-transformation-job)


## Import the dataset in DataBrew

Under Services search for **S3**.

![](/static/databrew/search-s3.png)


Click on **Create bucket** button in the right.

![](/static/databrew/create-bucket.png)


Name the bucket **output-dataprep-**`accountID` (get the accountID from the menu on the upper right). 

![](/static/databrew/create-bucket-parameters.png)


Leave the remaining fields at their default and click on **Create bucket**.

![](/static/databrew/create-bucket-parameters2.png)


Click on **Create folder** button to create the folder `raw`.

![](/static/databrew/create-folder-1.png)


On the **Create folder** screen, name the folder `raw` and click on **Create folder** button. Leave the other fields with their default values. 

![](/static/databrew/create-folder-2.png)


Using the same approach, create the folder `clean`. You will get the following structure in the **output-dataprep-**`accountID` bucket:

![](/static/databrew/create-folder-3.png)


Under Services search for **AWS Glue DataBrew**.

![](/static/databrew/search-databrew.png)


Click on the **Create Project** button.

![](/static/databrew/create-project.png)


In the **Project details**, name your project `CustomerChurnPrep`.

![](/static/databrew/project-details.png)


Under **Select a dataset** click on **New dataset**. Name your dataset `Churn` click on **File upload** and choose the file `churn.csv` that you downloaded in the **"Prerequisites"**. Under **Enter S3 destination**, click on **Browse S3** and select the S3 bucket (created in the previous step) **output-dataprep-**`accountID`and select the folder **raw**.

![](/static/databrew/create-dataset.png)


Keep the selected file type `CSV` and the column header values `Treat first row as header`. 

![](/static/databrew/create-dataset-csv.png)


Keep the default sampling with the first 500 records of the dataset.

![](/static/databrew/validate-create-project-v2.png)


Under **Permissions** select `Create new IAM role` and input `churn` as **New IAM role suffix**. Leave the other fields with their default values and and click on **Create project**. 

![](/static/databrew/permission-project-v2.png)


## Define the data transformation recipe

Wait between 1 to 3 minutes and you will get the following screen that enables to define your data transformation recipe. When you build your recipe, you can test the recipe on the dataset sample (the first 500 records by default). Once the recipe is published, you can apply the recipe for the full dataset.

![](/static/databrew/view-transformation-recipe.png)


The dataset contains the column **Phone** which provides the remaining seven-digit phone number. The phone number is a PII (Personal Identifiable Information) so the purpose is to anonymize this field for the ML analysis. AWS Glue DataBrew provides a tool to anonymize a field. To try it, select, **More...**, **SENSITIVE** and **Redact values**. 

![](/static/databrew/transformation-redact-1.png)


For the **Source Columns** select `Phone` and keep the other fields with their default value (you can replace the default redact symbol by another one). Click on **Preview change** to see the result of the transformation, a new column (highlighted in yellow) will appear near the Pone column with the transformed value. 

![](/static/databrew/transformation-redact-2.png)


Click on **Apply** to include this step in the recipe. The field **Phone** displays now the transformed value and the first step is noted in the right under **Recipe**.

![](/static/databrew/transformation-redact-3.png)


Looking at the column **Churn?** we can notice that it contains the values `True.` and `False.` Glue DataBrew can be used to clean the data and remove the character `.` at the end of field's value. 

![](/static/databrew/churn-values.png)


Click on **Clean** and select **Special characters** under **Remove**.

![](/static/databrew/transformation-clean-1.png)


For the **Source column** select `Churn?` under **Special characters** select **Custom special characters** with the special character `.` and click **Preview change** to see the result of the transformation. Leave the other fields at their default values. 

![](/static/databrew/transformation-clean-2.png)


Click on **Apply** to include this step in the recipe. The field **Churn?** has been updated with the transformed value and the second step is added in the **Recipe**.

![](/static/databrew/transformation-clean-3.png)



## Running the transformation job

Once the recipe is defined, click on **Publish** under **Recipe**.

![](/static/databrew/recipe-publish-1.png)


Confirm the action by clicking on **Publish** button on the validation screen.

![](/static/databrew/recipe-publish-2.png)


Once the recipe is published (version 1.0 will appear under the recipe name), click on **Create job** button to apply the recipe on the full dataset and write the output in the destination S3 bucket. 

![](/static/databrew/create-job-1.png)


Under **Job details** name the job `churn-dataprep`. Under the **Job output settings** click on **Browse** for the S3 location and select **output-dataprep-**`accountID` with the folder **clean** (the folder `raw` contains the initial churn.csv and the folder `clean` will contain the output file after the Glue DataBrew processing). You can define the output format and the file type. Keep the default parameters. 

![](/static/databrew/create-job-2.png)


Under **Permissions** select the role that you previously created **AWSGlueDataBrewServiceRole-churn**. Leave the other fields with their default values. Click on **Create and run job**. 

![](/static/databrew/create-job-3.png)


On the **JOBS** view you can follow the status of the job execution from `running` to `succeeded` after 2 to 5 minutes. 

![](/static/databrew/create-job-4.png)


The output CSV file is available in the path **output-dataprep-accountID / clean**, the file can be used with Sagemaker Canvas for ML analysis. 



Additionally from AWS Glue DataBrew, you can get Data Quality overview and lineage information. 

From the **PROJECTS** view, click on **PROFILE** button to get an overview of the data quality. 

![](/static/databrew/data-quality-1.png)


Click on **Run on data profile** to configure the data profiling job. 

![](/static/databrew/data-quality-2a.png)

Under the **S3 location** select the path **output-dataprep-accountID/raw.** Under **Role name** select **AWSGlueDataBrewServiceRole-churn**. Leave the remaining fields at their default values. Click on **Create and run job**. 

![](/static/databrew/data-quality-2.png)


After few minutes, the data quality report is generated by the data profiling job. 

![](/static/databrew/data-quality-3.png)


From the **PROJECTS** view, click on **LINEAGE** button to get an overview of the data lineage.

![](/static/databrew/data-lineage-1.png)


You will get the data linegae for the dataset. 

![](/static/databrew/data-lineage-2.png)










