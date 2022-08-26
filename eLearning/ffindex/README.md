---
layout: page
title: Indexing Data
permalink: /ffindex/
---

<link rel="stylesheet" href="/lib/public/global-training.css">


## The environment should begin to load immediately. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

When the Fusion Login page displays, login:
* USERNAME: ```admin```
* PASSWORD: ```password123```


## Welcome to the Indexing Lab, in this lab  you will ingest a datasource, index your data and make schema changes. When we're done you'll have a functioning Fusion collection! .....Let's get started by creating a Fusion App...

 

1. Click on **Create new app**, name it ```Online_Shoes``` and click **Create App**. It will take a few seconds to create. 
   
2. Click on your newly created app **Online_Shoes** to enter the *Fusion workspace*, this is where you can configure how an app ingests, indexes, queries, and analyzes data 

# Ingest your Data

4. Hover over the **INDEXING** icon in the sidebar, then click **Datasources**

 <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%205%20ff%20ingest.png" style="height: 300px; width:400px;"/>
   
5. Click **Add+**, from the drop-down menu, click on **File Upload** 
   
6. Let's add some parameters:
    * In **DATASOURCE ID** add: ```shoes```
    * In **FILE ID**, add: ```data.json.zip``` then click **Save**

7. Click **Run**, then click **Start**

>Note: Success! The job will take about 2 minutes, when it's done, the "running" icon will change to a "sunshine".

8. Click **Save**, then close the job box

 <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%209%20ff%20ingest%20close%20job%20box.png" style="height: 170px; width:300px;"/>


# Index your data 

9.  Hover over **INDEXING**, click on **Index Workbench**
   
10.   Click **Load** then click on **Shoes** from the drop-down

 <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%209%20FF%20ingest.png" style="height: 100px; width:400px;"/>

>Note: Here we see simulated results for our shoes data, with the fields for the first result expanded. Take a minute to explore the data!

11.   Hover over **COLLECTIONS** in the sidebar, then click **Fields**

 <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%2012%20ff%20ingests%20fields.png" style="height: 200px; width:300px;"/>

# Manage your Schema

12.   Click **Add a Field+** and add these parameters:
* **Field Name**: ```item-data```
* **Field Type**: text_en
* Check **Indexed** and **Multivalued** 
* Uncheck **Stored**
* Click **Save**

13.   Let's create a static field for Brand. Start by clicking **Add a Field**, and include these parameters:
* **Field Name**: ```brand```
* **Field Type**: string
* Ensure **Indexed** and **Stored** are checked
* Click **+ Copy Fields to** 
* **Copy Fields To**: item-data
* Click **Save**
  
<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%2016%20copy%20fields%20ff%20ingest.png" style="height: 100px; width:500px;"/>

>Note: You now have two new static fields: brand and item-data. However, they have no values in the Num Docs column. At this point, you also have multiple windows open in your Fusion workspace. Each window is shown in the tabs along the bottom of the UI. You can navigate to each window by clicking the tabs. Find and return to the **Datasources** window  <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%2016%20note%20ff%20ingest.png" style="height: 50px; width:600px;"/>


14.  Because we made changes to the Schema, we need to re-index our data. Open the **shoes** datasource

15.  Click **Clear Datasource**, then click **Yes, clear**

16.  Click **Run** then click **Start**. Again, the job will take a few minutes to complete. When the job finishes running, click **Save**

17.  Return to the **Fields** window. Your new fields should have Num Docs values. If you don't see Num Docs values, close out of **Fields** and reopen the window.

18.  Add the following fields and their parameters by repeating **step 15** for each row:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%2019%20field%20params.png" style="height: 350px; width:700px;"/>

>Note: We're taking these steps to prepare our data for the ingestion and indexing process. This then improves our query relevance in future labs.

19. We need to re-index again! Return to the **Datasources** window, open the **shoes** datasource, then Click **Clear Datasource**

20. Click **Run** then click **Start**, when the job finishes running, click **Save**

21. Return to the **Fields** window. Close it and reopen it to refresh. Notice that almost all the new static fields have Num Docs values.

22. Return to the **Index Workbench**, and click on the arrow next to the **Parser** icon

23. Take a minute to review the **Simulated Results**, then click on the green circle next to the **CSV** parser to deselect it

<details>
<summary>What Happened?</summary> 

Nothing! there was no change to your results - this data is in JSON format!
</details>

24.  Click on the green circle next to the **JSON** parser to deselect it. Notice that now all fields other than _lw_* fields have been moved into one field labeled body_t. This is not what we want! 

25. Click on the circle next to the **JSON** parser stage to reselect the parser stage. Your results will revert to much more usable fields again.

>Note: This exercise demonstrates the critical importance of parsers in the ingestion process. In a real-world setting, you would likely need many different parsers

26. Make sure to **Save** your open Fusion Workspace tabs!

_______________________________________________________________________________

Great job! You now have a functioning Fusion app with data and a customized Schema! If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app, a cog will appear in the lower right corner, click it
3. On the box that opens, click **Export app to zip**
   
This concludes the Indexing Lab. 




