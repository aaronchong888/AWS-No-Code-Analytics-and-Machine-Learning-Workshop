---
title : "Resources clean-up"
weight : 50
---

::alert[In order to avoid future charges, especially if running in your own account, please follow the steps below to clean resources created during the workshop.]{type=warning}

## AWS Glue DataBrew - cleanup

1. Open the [DataBrew console](https://console.aws.amazon.com/databrew/), and on the navigation pane, choose **Projects**.
2. Choose the project that we have created at the beginning of this workshop. For **Actions**, choose **Delete**.
3. On the Delete project pane, choose **Delete attached recipe**. Then choose **Delete**. Your project, along with its recipe and jobs, will be deleted.
4. On the navigation pane, choose **Datasets**.
5. Choose your dataset, and for **Actions**, choose **Delete**.
6. Open the [Amazon S3 console](https://console.aws.amazon.com/s3/). Delete the `databrew-output` folder and its contents.

## SageMaker Canvas - logout

If you're not using Amazon SageMaker Canvas, you can log out of your session. A session starts as soon as you launch SageMaker Canvas from the console. Logging out ends the session. You are only billed for the duration of the session.

When you log out, your models and datasets aren't affected, but SageMaker Canvas cancels any Quick build tasks. If you log out of SageMaker Canvas while running a Quick build, your build might be interrupted until you log back in. When you log back in, SageMaker Canvas automatically restarts the build.

To log out, choose the Log out button on the left panel of the SageMaker Canvas app.

![logout](/static/canvas/logout.png)

You can also log out from the SageMaker Canvas app by [deleting the app](https://docs.aws.amazon.com/sagemaker/latest/dg/canvas-manage-apps.html#canvas-manage-apps-delete) in the console.

More information can be found on the [Logging out of Amazon SageMaker Canvas](https://docs.aws.amazon.com/sagemaker/latest/dg/canvas-log-out.html) documentation.

## Amazon Quicksight - delete the dashboard

Use the following procedure to delete a dashboard.

1. On the **Dashboards** tab of the Amazon QuickSight start page, choose the details icon (vertical dots) on the dashboard that you want to delete.
2. Choose **Delete**. Then choose **Delete** again to confirm that you want to delete it.