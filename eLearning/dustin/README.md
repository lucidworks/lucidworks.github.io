---
layout: page
title: Dustin testing
permalink: /dustin/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

## It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

## When the Fusion login page appears, use the above provided username and password. Please minimize the **Credentials** window before proceeding.
<br>

## Welcome to the Indexing Data Lab! <br> Through this set of lab activities, you will ingest a datasource, index your data, and make schema changes. When we're done you'll have a functioning Fusion collection! 

---
<br>

## Ingest your data
For this example we will be ingesting a data file, but remember you can ingest data via a long list of connectors or other options.

1. Click the **Online_Shoes** app to open it and enter the Fusion workspace. 

2. In the left navigation pane, click **Indexing**, then select **Datasources** from the list. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_indexing.png" style="height:300px; width:200px;"/>

<br>
   
3. Click **Add+**, then select **File Upload** from the list. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffindex/ffindex_fileupload.png" style="height: 320px; width:360px;"/>

<br>

4. Enter the following datasource values:
* In the **Datasource ID** field, enter ```shoes```.
* In the **File ID** field, enter ```data.json.zip```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffindex/ffindex_datasourcefields.png" style="height: 300px; width:475px;"/>

<br>

5. Click **Save** to create the datasource.

<br>

Now we need to run a job in order to ingest the data into Fusion.

6. Click **Run**, then click **Start** in the job window to start the job.

>The job will take about 2 minutes to run. Note that the **Running** indicator displays while the job is in process, and will change to **Success** when the job is complete.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffindex/ffindex_runindexjob.png"/>

<br>

7. Once the job is complete, click the **X** to close the dialog.

<br>

## Index your data
Now that we have added data into Fusion, we can perform some indexing activities.

8.  In the left navigation pane, click **Indexing**, then select **Index Workbench** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_indexing.png" style="height: 300px; width:200px;"/>

<br>
   
9.  In the top right corner, click **Load**, then select **shoes** from the list.

 <img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffindex/ffindex_indexworkbenchload.png" style="height: 155px; width:550px;"/>
 
<br>

Notice we can see simulated results for our shoes data in the center window, and the first result has been expanded to display the fields details. 

Take a minute to click around and explore the data before continuing on in the lab.

<br>

## Manage your Schema
Our data has been indexed, but it doesn't display anything usable. Next we are going to add some static fields to better identify and display our results. 

10. In the left navigation pane, click **Collections**, then select **Fields** from the list.

 <img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collections.png" style="height: 350px; width:200px;"/>

<br>

Let's start by adding two static fields: ```item-data``` and ```brand```. 

11. In the Fields pane, click **Add a Field+**, then enter the following values:
* In the **Field Name** field, enter ```item-data```.
* In the **Field Type** field, select ```text_en```.
* Select the **Indexed** option.
* Deselect the **Stored** option.
* Select the **Multivalued** option.

12. Click **Save** to create the ```item-data``` field.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffindex/ffindex_itemdatafield.png" style="height: 300px; width:400px;"/>

<br>

13. Click **Add a Field** again, and enter the following values:
* In the **Field Name** field, enter ```brand```.
* In the **Field Type** field, select ```string```.
* Ensure the **Indexed** and **Stored** options are selected.

14. Click the green plus next to **+ Copy Fields to**. 
* In the **Copy Fields To** field, select the ```item-data``` option.

15. Click **Save** to create the ```brand``` field.
  
<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffindex/ffindex_brandfield.png" style="height: 300px; width:400px;"/>

<br>

You now have two new static fields: **brand** and **item-data**. However, they have no values in the Num Docs column (since they did not exist when we originally indexed our data). With the changes to our schema (the addition of the new fields), we need to re-index our data and populate these fields.

<br>

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffindex/ffindex_newfields.png" style="height: 240px; width:430px;"/>

<br>

><b>Note:</b> At this point, you have multiple windows open in your Fusion workspace, as indicated by the tabs along the bottom of the UI. You can navigate to a window by clicking the tab, or close it by clicking the <b>X</b> in the tab. 
<br>   
<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_tabs.png" style="height: 150px; width:450px;"/>

16.  Find and return to the **Datasources** tab and open the **shoes** datasource.

17.  Click **Clear Datasource**, then click **Yes, clear** to confirm the action.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffindex/ffindex_cleardatasource.png" style="height:210px; width:400px;"/>

<br>

18.  Click **Run**, then click **Start** to start the indexing job. 

>The job will once again take a couple minutes to run, since we are re-indexing all the data. Note that the **Running** indicator displays while the job is in process, and will change to **Success** when the job is complete.

19. Once the job is complete, click **X** to close the dialog.

<br>

Now that our job is complete, let's go review our simulated results.

20.  Navigate to the **Fields** tab, where your new fields should display Num Docs values. If you don't see Num Docs values, close and reopen the window (**Collections > Fields**).

>Now that we can see our new fields in action, we need to add a couple more to prepare our data for the ingestion and indexing process, which will in turn improve our query relevance in future lab activities.

<br>

21.  Add the following fields and their parameters by repeating steps 15-16 for each row in the table.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffindex/ffindex_fieldparams.png" style="height: 330px; width:650px;"/>

<br>

Since we have added more fields, we will need to repeat steps 20-24 and re-index our data again. After the re-index, your fields should look something like this:

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffindex/ffindex_indexedfields.png" style="height: 350px; width:650px;"/>

<br>

## Understanding Parsers
Our data ingestion step uses parsers to help Fusion understand and process the incoming data correctly. Let's take a minute to review how parser selections impact the results.

22. Navigate to the **Index Workbench** tab, and take a minute to review the **Simulated Results** displayed.

23. Click the arrow next to the **Parser** icon to expand the list of parser stages.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffindex/ffindex_parsers.png" style="height: 300px; width=400px;"/>

<br>

24. Click the green circle next to the **CSV** parser to disable it.

<details>
<summary>What Happened?</summary> 

Nothing! Since our data was in JSON format, there was no change to your results.
</details>

<br>

25.  Click the circle next to the **CSV** parser to re-enable it, then click and disable the **JSON** parser. 

<details>
<summary>What happened?</summary>

Since our data was in JSON format, this parser was applied during the indexing process. Notice that now all fields other than _lw_* fields have been moved into one field labeled body_t. This is not what we want! 
</details>

<br>

26. Click the circle next to the **JSON** parser stage to re-enable it. Your results will revert to much more usable fields again.
<br>

><b>Note:</b> This exercise demonstrates the critical importance of parsers in the ingestion process. In a real-world setting, you would likely need many different parsers organized and used in sequence to analyze your data.

<br>

Feel free to explore more by clicking to enable or disable one or more of the parsers, and see what happens.

---
<br>

## Great job! You have successfully completed the Indexing Lab, and you now have a functioning Fusion app with data and a customized schema. 

<br>

>Make sure to **Save** your open Fusion workspace tabs before exiting the application.

<br>

If you would like to save your Fusion app to import and practice with later, you can do it now:
1. In the left navigation panel, click **Apps**, then choose **Return to Launcher** from the list.
2. Hover over your app until a cog appears in the lower right corner.
3. Click the cog icon.
4. In the pop-up window, click **Export app to zip**.

---
<br>

## Hope to see you in our next course! 
## Thanks and happy learning!