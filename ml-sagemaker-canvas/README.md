# Train a Machine Learning model and generate accurate predictions with Amazon SageMaker Canvas

![canvas](/static/shared/canvas-logo.png)

> Make sure you have performed the steps described in the **"Extract, Transform and Load data with AWS Glue DataBrew"** section before beginning this lab.

## Agenda

1. [Import the dataset in Canvas](#import-the-dataset-in-canvas)
1. [Building and Training a ML model](#building-and-training-a-ml-model)
1. [Using the model to generate predictions](#using-the-model-to-generate-predictions)


## Import the dataset in Canvas

Go back to the SageMaker Canvas tab created in the **Prerequisites** section. On the left menu, you can click the second icon to head to the Datasets section, then click the **Import** button.

![](/static/canvas/import-data-v2.png)

Now, select **S3** option and browse the folder named **output-dataprep-AccountID** to import the dataset prepared by Glue DataBrew.

![](/static/canvas/import-from-s3-01.png)

![](/static/canvas/import-from-s3-02.png)

The import process takes approximately 10 seconds (this can vary depending on dataset size). When it’s complete, we can see the dataset is in Ready status.

![](/static/canvas/finaldataset-v2.png)

After we confirm that the imported dataset is ready, we create our model.

## Building and Training a ML model

Now, let's head back to the **Models** section of the web page, by clicking the second button on the left menu.

![](/static/shared/canvas-models.png)

Click on **\+ New model**, and name your model `CustomerChurn`. 

![](/static/canvas/new-model.png)


In the Model view, you will see four tabs, which correspond to the four steps to create a model and use it to generate predictions: **Select**, **Build**, **Analyze**, **Predict**. In the first tab, **Select**, click the radio button to select the `churn-dataprep_XXXXX.csv` dataset we've imported previously. This dataset includes 21 columns and 5K rows. Click the bottom button **Select dataset**.

![](/static/canvas/model-dataset-v2.png)

Canvas will automatically move to the **Build** phase. In this tab, choose the target column, in our case `Churn?`. Your marketing team has informed you that this column indicates  whether the customer left the service (true/false). This is what you want to train your model to predict. Canvas will automatically detect that this is a **2 category prediction** problem (also known as binary classification). If the wrong model type is detected, you can change it manually with the **Change type** link at the center of the screen.

![](/static/canvas/model-build-v2.png)

We now validate some assumptions. We want to get a quick view into whether our target column can be predicted by the other columns. We can get a fast view into the model’s estimated accuracy and column impact (the estimated importance of each column in predicting the target column).

Select the **Preview model** option

![](/static/canvas/model-preview.png)

This feature uses a subset of our dataset and only a single pass at modeling. For our use case, the preview model takes approximately 2 minutes to build.

![](/static/canvas/model-preview-1.png)

Our preview model has a 95.8% estimated accuracy, and the columns with the biggest impact are Night Calls, Eve Mins, and Night Charge. This gives us an insight into what columns impact the performance of our model the most. Here we need to be careful when doing feature selection because if a single feature is extremely impactful on a model’s outcome, it’s a primary indicator of target leakage, and the feature won’t be available at the time of prediction. In this case, few columns showed very similar impact, so we continue to build our model.


For this workshop, we're planning on using all of the available features. You can come back to this step later and try to change some of the features to see the impact on the model training. 

Once you've explored this section, it's time to finally train the model! Before building a complete model.

Canvas offers two build options:

   * Standard build – Builds the best model from an optimized process powered by AutoML; speed is exchanged for greatest accuracy.
   * Quick build – Builds a model in a fraction of the time compared to a standard build; potential accuracy is exchanged for speed.

![](/static/shared/canvas-quick-vs-standard.png)


 It is a good practice to have a general idea about the performances that our model will have by training a **Quick Model**. A quick model trains fewer combinations of models and hyper-parameters in order to prioritize speed over accuracy, especially in cases like ours where we want to prove the value of training an ML model for our use case. Note that quick build is not available for models bigger than 50k rows. Let's go ahead and click **Quick build**.

![](/static/canvas/model-building.png)

Now, we wait anywhere from 2 to 15 minutes. Since the dataset is small, this will take probably even less than 2 minutes. 

> Don\'t worry if the numbers in the below images differ from yours. Machine Learning introduces some stochasticity in the process of training models, which can lead to different results to different builds.

When the model building process is complete, the model predicted churn **95.9%** of the time. This seems fine, but as analysts we want to dive deeper and see if we can trust the model to make decisions based on it. Let's focus on the first tab, **Overview**. This is the tab that shows us the **Column impact**, or the estimated importance of each column in predicting the target column. In this example, the `Night Calls` column has the most significant impact in predicting if a customer will churn. This information can help the marketing team gain insights that lead to taking actions to reduce customer churn.

![](/static/canvas/model-status-1.png)

For example, we can see that both low and high number of `CustServ Calls` also increase the likelihood of churn. The marketing team can take actions to prevent customer churn based on these learnings. Examples include creating a detailed FAQ on websites to reduce customer service calls, and running education campaigns with customers on the FAQ that can keep engagement up.

![](/static/canvas/model-status-2.png)

On the **Scoring** tab, we can review a visual plot of our predictions mapped to their outcomes. This allows us a deeper insight into our model. Canvas separates the dataset into training and test sets. The training dataset is the data Canvas uses to build the model. The test set is used to see if the model performs well with new data. The Sankey diagram in the following screenshot shows how the model performed on the test set. 

![](/static/canvas/model-overview-1.png)

To learn more, you can check the ["Evaluating Your Model's Performance in Amazon SageMaker Canvas" section](https://docs.aws.amazon.com/sagemaker/latest/dg/canvas-evaluate-model.html) of the Canvas documentation, as well as the page for [SHAP Baselines for Explainability](https://docs.aws.amazon.com/sagemaker/latest/dg/clarify-feature-attribute-shap-baselines.html).

To get more detailed insights beyond what is displayed in the Sankey diagram, business analysts can use a confusion matrix analysis for their business solutions. For example, we want to better understand the likelihood of the model making false predictions. We can see this in the Sankey diagram, but want more insights, so we choose Advanced metrics. We’re presented with a confusion matrix, which displays the performance of a model in a visual format with the following values, specific to the positive class—we’re measuring based on whether they will in fact churn, so our positive class is True in this example:

   True Positive (TP) – The number of True results that were correctly predicted as True

   True Negative (TN) – The number of False results that were correctly predicted as False

   False Positive (FP) – The number of False results that were wrongly predicted as True

   False Negative (FN) – The number of True results that were wrongly predicted as False

We can use this matrix chart to determine not only how accurate our model is, but when it is wrong, how often that might be and how it’s wrong.

![](/static/canvas/advanced-metrics-1-v2.png)

The advanced metrics looked good and we can therefore trust the model result. We see very low false positives (FP) and false negatives (FN). These are if the model thinks a customer in the dataset will churn and they actually don’t (false positive), or if the model thinks the customer will not churn and they actually do (false negative). High numbers for either might make us think more on if we can use the model to make decisions.

## Using the model to generate predictions

Since our model looks pretty accurate, we can move on to perform an interactive prediction on the **Predict** tab, either in batch or single (real-time) prediction.

Choose **Select dataset**.

![](/static/canvas/batch-predict.png)

Choose the imported `churn-dataprep_XXXXX.csv`. Next, choose **Generate predictions** at bottom of the page.

![](/static/canvas/batch-predict-ds-v2.png)

Canvas will use this dataset to generate our predictions. Although it is generally a good idea not to use the same dataset for both training and testing, we're using the same dataset for the sake of simplicity. After a few seconds, the prediction is done.

You can click **View** to see the prediction.

![](/static/canvas/batch-predict-results.png)

Once the prediction is complete, click the **Download CSV** button to download a CSV file containing the full output. SageMaker Canvas will return a prediction for each row of data and the probability of the prediction being correct. Keep this file safe, as it will be used for the next step.

![](/static/canvas/batch-predict-results-1-v2.png)

You can also choose to predict one by one values, by selecting **Single prediction** instead of batch prediction. Canvas will show you a view where you can provide manually the values for each feature, and generate a prediction. This is ideal for situations like **what-if scenarios**: e.g.  What happens to the churn rate if `Night Charge` is increased? 

![](/static/canvas/singleprediction.png)

> If you wish to augment data in real-time in Amazon Quicksight, you will need [to integrate the SageMaker model to your Quicksight dataset](https://docs.aws.amazon.com/quicksight/latest/user/sagemaker-integration.html#sagemaker-using). This requires you to: train a standard build model; share it via Amazon SageMaker Studio; deploy the model to a real-time endpoint. Please collaborate with a data scientist or ML Engineer to use this capability. Learn how to do so [here](https://aws.amazon.com/blogs/machine-learning/build-share-deploy-how-business-analysts-and-data-scientists-achieve-faster-time-to-market-using-no-code-ml-and-amazon-sagemaker-canvas/). Since training a standard build model could take around 1-2 hours, we will avoid doing so in this workshop.

-----

Congratulations\!\! You have successfully completed **Model training with SageMaker Canvas**. Now, you may proceed to the next lab:

4. [Dashboarding with Amazon Quicksight](../dashboarding-quicksight/)