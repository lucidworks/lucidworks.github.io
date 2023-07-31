---
layout: page
title: Intro to Machine Learning
permalink: /aipbl/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

# It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Intro to Machine Learning Lab! <br> Through this set of lab activities, you will ingest and transform data with the Parallel Bulk Loader (PBL), prepare data with Spark shell, and verify your successful data load.

---
<br>

Let's get started by creating a new app in Fusion. 

1. From the Fusion launch page, click **Create new app**. 

2. In the **App Name** field, enter the name ```Labs```. 

3. *(Optional)* Enter an **App Description** and select an **App tile color**.

4. Click **Create App**.
   
5. Once it has been created, click the **Labs** app to open it and enter the Fusion workspace. 

<br>

## Ingest and Transform your Data

For this lab exercise, we will be using PBL jobs to populate data and signals in the collections. 

6. In the left navigation pane, click **Collections**, then select **Jobs** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collections.png" style="height: 350px; width:200px;"/>

<br>
   
7. In the Jobs pane, click **Add+** and begin typing ```parallel```, then select **Parallel Bulk Loader** from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aipbl/aipbl_addPBLjob.png"/>

<br>

8. In the job configuration window, enter the following values:
* In the **Spark Job ID** field, enter ```BestBuy_catalog```.
* In the **Format** field, enter ```parquet```.
* In the **Path** field, enter ```gs://training-ecommerce/catalog```.
* Click the **Output Collection** field and select ```Labs```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aipbl/aipbl_BBcat_jobsettings.png"/>

<br>

9. Click to enable the **Advanced** fields.

10. Scroll down to the Write Options section, then copy and paste the follow value into the **Transform Scala** field:

```
def transform(inputDF: Dataset[Row]) : Dataset[Row] = {
inputDF.filter("department IN ('ACCESSORIES', 'APPLIANCE', 'COMPUTERS')")
}
```

11. Click **Save** to create the new job. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aipbl/aipbl_BBcat_transform.png"/>

<br>

Now we need to run the job in order to ingest the data into Fusion.

12. Click **Run**, then click **Start** in the job dialog to start the job.

>The job will take a couple minutes to run. Note that the **Running** indicator displays while the job is in process, and will change to **Success** when the job is complete.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aipbl/aipbl_BBcat_runjob.png"/>

13. Once the job is complete, click **X** to close the job dialog.

<br>

We need to add one more PBL job, this time to ingest our signals data.

14. In the Jobs pane, click **Add+** and begin typing ```parallel```, then select **Parallel Bulk Loader** from the autosuggestion list.

15. In the job configuration window, enter the following values:
* In the **Spark Job ID** field, enter ```BestBuy_signals_labs```.
* In the **Format** field, enter ```parquet```.
* In the **Path** field, enter ```gs://training-ecommerce/signals```.
* Click the **Output Collection** field and select ```Labs_signals```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aipbl/aipbl_BBsig_jobsettings.png"/>

<br>

16. Click to enable the **Advanced** fields.

17. Scroll down to the Write Options section, then copy and paste the follow value into the **Transform Scala** field:

```
import java.sql.Timestamp
def transform(allClicks: Dataset[Row]) : Dataset[Row] = {
val ecommerceFullCatalog = spark.read.parquet("gs://training-ecommerce/catalog")
val someHardGoods = ecommerceFullCatalog.filter("department IN ('ACCESSORIES', 'APPLIANCE', 'COMPUTERS')")
val trimmedClicks = allClicks.select("query","doc_id","fusion_query_id","filters_s","type", "count_i","timestamp_tdt","user_id","id")
val hardGoodClicks = trimmedClicks.alias("TC").join(someHardGoods.withColumnRenamed("id", "doc_id"), Seq("doc_id")).select("TC.*", "name", "longDescription", "department")
val userClickCounts = hardGoodClicks.groupBy("user_id").count.withColumnRenamed("count", "user_count")
val itemClickCounts = hardGoodClicks.groupBy("doc_id").count.withColumnRenamed("count", "item_count")
val clicksWithCounts = hardGoodClicks.join(userClickCounts, Seq("user_id")).join(itemClickCounts, Seq("doc_id"))
val usefulClicks = clicksWithCounts.filter("user_count > 2 AND item_count > 4").drop("user_count","item_count")
val now = System.currentTimeMillis()
val maxDate = usefulClicks.agg(max("timestamp_tdt")).take(1)(0).getAs[Timestamp](0).getTime
val diff = now - maxDate
val addTime = udf((t: Timestamp, diff : Long) => new Timestamp(t.getTime + diff))
val newDF = usefulClicks
.withColumnRenamed("timestamp_tdt", "orig_timestamp_tdt")
.withColumn("timestamp_tdt", addTime($"orig_timestamp_tdt", lit(diff)))
newDF
}
```
        
18. Click **Save** to create the new job. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aipbl/aipbl_BBsig_transform.png"/>

<br>

19. Click **Run**, then click **Start** in the job dialog to start the job.

>Once again, the job will take a couple minutes to run. If your job fails, be sure to check your parameters with the configurations above and run the job again. 

20. Once the job is complete, click **X** to close the job dialog.

<br>

## Verify Successful Data Load
Now that we have ingested all of our data, we want to verify that it was loaded correctly. 

Let's start by updating the display fields and adding facets for both the **Labs** and **Labs_signals** collections.

21. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list. 
   
22. Click **Display Fields**, and change the following values:
* In the **Name** field, enter ```name```. 
* In the **Description** field, enter ```longDescription```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aipbl/aipbl_displaynames.png"/>

<br>

23. Click **Display Fields** again to close the dropdown.

24. Click **Add a field facet**, begin typing ```department``` then select **department** in the autosuggestion list.

25. Click **Save** to save your changes to the Query Workbench, then click **Yes, save over the existing pipeline** to confirm the action.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aipbl/aipbl_addfacets.png"/>

<br>

Next, we will switch collections and make the same changes.

26. In the top left corner, click the Collections dropdown, then select the **Labs_signals** collection.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collectiondropdown.png" style="height: 320px; width: 225px;"/>

27. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list. 
   
28. Click **Display Fields**, and change the following parameters:
* In the **Name** field, enter ```name```. 
* In the **Description** field, enter ```longDescription```.

29. Click **Display Fields** again to close the dropdown.

30. Click **Add a field facet**, begin typing ```department```, then select **department** in the autosuggestion list.

31. Click **Save** to save your Query Workbench changes, then click **Yes, save over the existing pipeline** to confirm the action.

><b>Note:</b> These signals contain all the data from the associated catalog item.  This is NOT a recommended design for production, as the signals index would be very large.  However, this can be very useful for our examples, as the click data is easier for us to read and comprehend.

---
<br>

## Great job! You have successfully completed the Intro to Machine Learning Lab, where you have ingested and transformed data with the Parallel Bulk Loader (PBL) and Spark shell.

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