---
title : "Create your Business Dashboard with Amazon Quicksight"
weight : 40
---

![](/static/shared/amazon-quicksight-logo.png)

::alert[Make sure you have performed the steps described in the **"Train a Machine Learning model and generate accurate predictions with Amazon SageMaker Canvas"** section before beginning this lab.]{type=warning}

## Agenda

1. [Amazon Quicksight setup and data upload](#amazon-quicksight-setup-and-data-upload)
2. [Creating the dashboard](#creating-the-dashboard)


## Amazon Quicksight setup and data upload

Open Amazon QuickSight in AWS console. Select “Datasets” in a left side menu and then click “New dataset” button.

![new-dataset](/static/quicksight/new-dataset.png)

Amazon QuickSight supports many data sources. In this workshop, we are going to use a local file, the one we have previously generated in Canvas, as our source data. We can do so by choosing the “Upload a file” option. 

![upload-file](/static/quicksight/upload-file.png)

In the new window, select the file downloaded from SageMaker Canvas containing the predictions. Amazon QuickSight will upload and analyze the file. After checking that everything is as we expect it in the preview, we can click “Next” and then “Visualize”. 

![visualize](/static/quicksight/visualize1.png)
![visualize](/static/quicksight/visualize2.png)

At this stage data successfully imported and we are ready to analyze it. 

## Creating the dashboard

Our goal is to create a clear and easy-to-use dashboard that recaps all the information necessary for assisting data analysts and marketing specialists to take data-driven business decisions. It will look like the following:

![dashboard-prototype](/static/quicksight/dashboard-prototype6.png)
![dashboard-prototype](/static/quicksight/dashboard-prototype7.png)

On this dashboard we visualize several important business metrics: 

1.	Customers under the risk - Top left gauge chart represents of users with a risk of churning out of the total number of customers. This chart helps us quickly understand size of a potential problem. 

2.	Potential Revenue Loss by Churn – Second donut chart from the left represents the charges incurred by users with a risk of churning versus the loyal customers. This chart helps us quickly understand size of a potential charges lost. We can also get a glimpse of the percentage of each category of users

3.	Total Churn by Churn Category with Percentage - The third donut gives the total number of customers with their churn category and their percentage of each category

4.	Customers Likely to Churn by State – The table at the right groups the customers at risk of churn by state, revenue loss, number of customers at risk for each state, churn rate per state and the average length of account in days. This gives at a glance immediate answers to some critical questions, for example, the imapct to each states bottomline and the predicted revenue loss. As you can see, this impact is not uniform across the states, therefore, this information can drive strategic marketing campaign at the states with higher churn rate & revenue loss.

5.	Map of Customers at Risk - The geographic representation visual of the total customers at risk by states across the country

6.	Customers at Risk Across the 50 States at a Glance – The stacked bar chart gives a visual contrast of customers at risk and the loyal customers by states with the percentage gauge on the horizontal axis for quick visual comparison. 


### Customers likely to churn

The first metric we will visualize in our dashboard are the customers that are at risk of churning. We will create for this a gauge chart representing data distribution of the churn variable in our dataset. To create this visualization, let's do the following:

1. Choose **Add** on the top left of the application bar, and then choose **Add visual**

	A new, blank visual is created and receives focus.

	The field wells display the fields that are visualized.

2. In the **Fields list** menu, select the “Churn?” attribute and QuickSight will automatically build a visualization for you.

![](/static/quicksight/first-churn-plot.png)

3. Although the bar plot is a common visualization to understand data distribution, we prefer to use a "Gauge chart”. Below the **Field list** menu is **Visual types**, select Gauge visual type. At the top of the visual is the **Field wells**, drag the Churn attribute from the **Fields list** into the **Value** field well.

![](/static/quicksight/visual_type.png)

### Adding a Churn Filter
What you have is a semicircle of the all churn, both true and false. We want to be able to see at a glance the total gauge of the true churn against the total custimer size. To do this, we will need to add a filter to the visual using the "churn" attribute. 

![](/static/quicksight/churn1.png)

1. While the focus is on the Gauge customer churn visual, choose **Add filer** on the left side of the page, and then choose the "Churn" attribute to filter

![](/static/quicksight/churn-filter1.png)

2. Choose the new filter in the pane to configure it. Or you can choose the three dots to the right of the new filter and choose **Edit.**

3. In the **Edit filter** pane that opens, for Applied to, choose the following options.

	- **Only this visual** – The filter applies to the selected item only.

4. Deselect the **Select all** checkbox and after then check the **True** checkbox to select only the customers likely to churn

5. Leave other options as default then click **Apply** at the botton of the page 

![](/static/quicksight/churn-filter2.png)

In order to view the true churn in the context of the total churn, you need to perform this final steps:

- Hover over the visual to select the pen icon at the top right of the screen

- On the **Format Visual** pane that opens up to the left of the screen, edit the **Axis Style** option

- On **Range** enter an 0 as the minimum range and 5000 as the maximum range since those are the minimum and maximum values of rows that we have in our data

![](/static/quicksight/churn-filter3.png)

We can change this plot by changing its properties. We could also change the chart title by double clicking on the current name: change it to `Customers likely to churn`.

![](/static/quicksight/churn-gauge.png)

![](/static/quicksight/churn-edit-visual1.png)


We could also customize other visual effects (remove agenda, add values, change font size) by clicking the options button. We can see below that we have increased the area of the donut, as well as added some extra information in the labels of our plot.


### Editing visual titles or subtitles

The visual title is shown by default. After subtitles are created, they're also shown by default. Right now, the visual should show "Count of Churn?"

1. On the analysis, select the visual and perform the following steps

	a. At the visual's right, choose the **Format visual** icon.

	b. In the **Format Visual** pane that opens at left, choose the **Title** tab.

	c. Choose **Edit title** 
	d. In the **Edit title** page that opens up, type "Customers Likely
	e. When you're finishing editing, choose **Save**



2. To change the background and/or foreground
	a. Choose the left semicircle on the visual, and then choose **Color foreground** and select red color 

	b. While on the same click, choose a color for the **Color background** and select grey color

	![](/static/quicksight/colors.png)

### Potential revenue loss

Another important metric to take into account when calculating business impact of customer churn is  “Potential revenue loss”. This is an important metric as it helps us to understand business impact from customers with a churning risk. In Telecom industry we could have many inactive clients who will have high churn risk and but zero charges. This chart will help us understand are we in a such situation or not. To add this metric to our dashboard, we create a custom calculated field by providing the mathematical formula for computing potential revenue loss, then plot it as a donut chart. 

We have four different attributes related to charges (Day, Eve, Int, Night) and we could create a calculated field as sum of them. Click “Add” button and select “Add calculated field”.

![](/static/quicksight/revenue-loss-add-calculated-field.png)

Let's compute the total charges: 
1.  Add name “Total charges”
2.	Write a simple formula `{Day Charge}+{Eve Charge}+{Intl Charge}+{Night Charge}`
3.	Click “Save” button

![](/static/quicksight/revenue-loss-compute-formula.png)

Click “Add” button and select “Add visual”.

![](/static/quicksight/revenue-loss-add-visual.png)

Let's make it look nice:

1.	Choose the Donut chart icon on **Visual types** pane
2.	From the **Field list** pane, drag the “Churn?” attribute to the **Group/Color** field wells
3.	From the **Field list**, drag the “Total Charges” measure into **Value** field wells
4.	In **Value** field well, click the drop-down menu and select **Show as**  “Currency”

![](/static/quicksight/revenue-loss-donut-final1.png)

We could also customize our visual by formatting the donut diameter size. Start by clicking the **Format visual** icon on the  top right of the donut visual

![](/static/quicksight/revenue-loss-donut-final2.png)

You can toggle between the sizes to get a feel of the sizes, for our purpose, we will leave the size option at medium.

We can also change the data labels to reflect the value and percent of each selected category, that way we can see what these values are at a glance without havning to click the visual. The following steps will allow you display the total charges and the percentage of the churn categories outside the circumference of the donut visual

1. Expand the **Data labels** pane by clicking on it, click the **Show data labels**, Under **Label options**, check **Show category** and **Show metric**
2. To view the percentage values:
	- Under *Metric label style* select "value and percent"
	- Under *Position* choose "Outside"
	- Select a font size "Medium"

![](/static/quicksight/revenue-loss-donut-final3.png)

To view the percent of customer churn

1. On the analysis page, choose **Visualize** on the tool bar.

2. Choose **Add** on the application bar, and then choose Add visual.

3. On the **Visual types** pane, choose the donut chart icon.

4. From the **Fields list** pane, drag the "Churn" field to the **Group/Color** and **Value** field wells


Let's review how our dashboard looks like so far, and what we can understand from it:

![](/static/quicksight/dashboard-checkpoint1.png)

Currently, we already could say that in total we could lose almost 50% (2,479) customers which equals to 58% ($56.14K) revenue. Let’s deep dive further by analyzing potential revenue loss, at the state level.

### Potential revenue loss by State

Let's drill down and analyze potential revenue loss by State. You know by now how to create a new visual, so go ahead and add a new visual: 

1. Click on **Add**, then select **Add visual**
2.	Select “Horizontal bar chart”
3.	Drag “Churn?” attribute into **Group/Color** field well
4.	Drag “Total Charges” attribute into the **Value** field well
5.	In **Value** drop-down menu select “Show as” -> “Currency”
6.	Drag “State” attribute into the **Y axis**


This visual could help us to understand which state is the most important for us from a marketing campaign perspective. For example, in WV (West Virginia) we potentially could lose about $1,245 of our revenue while in  VT (Vermont) this value is lesser at less a thousand at $931. 

We could also customize other visual effects (remove agenda, add values, change font size) by clicking the selector icon at the top right corner "Format visual".

![](/static/quicksight/revenue-loss-state-creation.png) 

We could also sort new visual by clicking “Total charges” at the bottom and select “Descending”.

![](/static/quicksight/revenue-loss-state-sorted.png)

### Geographical Map Representation of Churn

What if we want to have a quick glance of the customer churn by geography and see the potential revenue loss at a glance through the size of the orange circles which represents the customers that are likely to churn? We can create a point map of the geographic location by states.
1. Click on **Add**, then select **Add visual**
2. For **Visual type**, choose the points on map icon. It looks like a globe with a point on it.

![](/static/quicksight/point-map1.png)

3. Drag “States” attribute into “Geospatial" field well
4. Drag "Total Charges" attribute into "Size" 
5. Drag "Churn" into "Color" 

![](/static/quicksight/point-map2.png)


### Churning customer details

The final visualization we will add to our dashboard is all about enabling the marketing team to reach out to the customers that are at risk of churning, by visualizing their contact information:

1. As usual, start by clicking the **Add** button and select “Add visual”. 
2. This time, we'll select “Table” as **Visual types** 
3. Then, we will add customer information by dragging the following attributes to the **Group by** field well:
	"Area Code", “Phone”, “State”, “Int’l Plan”, “Vmail Plan”, “Churn?”, “Account Length” 
4.  Drag the  “probability” attribute into **Value**. From the **Value** drop-down menu select “Show as” -> “Percent". 


![](/static/quicksight/customer-info2.png)

<!-- ![](/static/quicksight/customer-info.png) -->

We can enhance the look of our visual, lets add some conditioning with a smiley or sad emoticons

On the table visual, open the context menu on the **Format visual** icon at the upper-right. Then choose **Conditional formatting.** 

![](/static/quicksight/customer-info1.png)

Options for formatting will display on the left, then do the following:

1. Choose the "Churn" column
2. Click the **Add background color** and a sub-menu pane opens up with other options

![](/static/quicksight/conditional-formatting.png)

3. Leave the **Aggregation** as "No aggregation"
4. Under **Condition** select "Equals", input "True." into  **Value** and select red under **Color**

![](/static/quicksight/edit-background-colors.png)

5. Click **Add condition** to add another "Condition". For **Condition #2** Repeat the same steps but input "False." into **Value** Select green for **Color**
6. Click **Apply** and then **close**

We will proceed to complete our styling by adding an icon for true & false churns categories.

1. On the **Conditional formatting** pane, choose **Add icon** to set an icon
2. Under **Condition #1** choose "Equals" and input "False." as **Value** choose the "smiley" icon and leave **color** as white
3. For **Condition #2** choose "Equals" and input "True" as **Value** choose the "sad" icon and leave **color** as white
4. Choose **Apply** and **Close**

![](/static/quicksight/edit-icon.png)

As you can see we can gain some quick insight looking at our table, we see the state, account length, the churn and the probability.  

### Final (optional) touches: customizing the dashboard

Amazon Quicksight provides the capability to customize your dashboard. In this lab, we will a dashboard title, and change the color palette to a dark theme. Please do take the time to explore other customization option, such as moving visuals around and resizing them, or add your own custom visuals that might make more sense for your business. 

To add the title, click "Add" then "Add title". We will call our dashboard "Churn Analysis". 

![churn-analysis](/static/quicksight/churn-analysis.png)

To change the theme, click on the "Themes" button in the left side menu, and select the one you prefer. We will choose "Midnight" here. 

![midnight](/static/quicksight/midnight.png)

### Publish the dashboard

A dashboard is a read-only snapshot of an analysis that you can share with other Amazon QuickSight users for reporting purposes. A dashboard preserves the configuration of the analysis at the time you publish it, including such things as filtering, parameters, controls, and sort order. The data used for the analysis isn't captured as part of the dashboard. When you view the dashboard, it reflects the current data in the data sets used by the analysis.

To publish a dashboard, click on the “Share” button in the navigation menu on the top, and select “Publish dashboard”. 

![](/static/quicksight/dashboard-publish.png)

Provide a name, then click on "Publish". Congratulations, your dashboard is now ready to be used! 

![dashboard-prototype](/static/quicksight/dashboard-prototype6.png)

## Updating the dashboard with new predictions

As the model evolves and we generate new data from the business, we might need to update this dashboard with new information. To do that, we have to:

1. Generate new predictions with a new dataset in Canvas, then download it;
2. Open Amazon QuickSight, choose “Datasets” on the left side navigation menu and click on the existing dataset that we have created previously.

![](/static/quicksight/old-dataset.png)

3. In the pop-up window, click “Edit dataset” button.

![](/static/quicksight/edit-dataset-v2.png)

4. In the drop-down file menu, choose “Update file”, then "Upload file".

![](/static/quicksight/update-file.png)

5. Choose the downloaded file with the predictions. Once the preview is shown, click “Confirm file update” button

![](/static/quicksight/confirm-file-update.png)

6.	After the “File updated successfully” message is shown, we can see that file name has also changed. Click “Save & publish” button.

![](/static/quicksight/save-and-publish.png)

7.	Once the “Saved and published successfully” message pops up, you can go back to the main menu by clicking the “QuickSight” logo in the left upper corner.

![](/static/quicksight/back-home-success.png)

8. Select “Dashboards” on the left side menu and select the dashboard we have created before.

![](/static/quicksight/dashboard.png)

We have just updated an Amazon QuickSight dashboard with the most recent predictions from Amazon SageMaker Canvas. 
