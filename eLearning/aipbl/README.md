---
layout: page
title: Intro to Machine Learning
permalink: /aipbl/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol. Please do not click *Start Lab* again. It may take a few mintues for the Fusion environment to fully display.

When the Fusion Login page displays, login:
* USERNAME: ```admin```
* PASSWORD: ```password123```

## In this lab  you will ingest and transform data with the Parallel Bulk Loader (PBL), prepare data with spark shell, and verify successful data load! Let's get started by creating a Fusion App.

1. Click on **Create new app**, name it **Labs** and click **Create App**
   
2. Click on your newly created app to enter the *Fusion workspace*, this is where you can use the PBL jobs to populate data and signals in the collections

# Ingest and Transform your Data

3. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**
   
4. Click **Add+**, from the drop-down menu, select **Parallel Bulk Loader**

5. Toggle on **Advanced**. Let's add some parameters to ingest the data:
    * Update the **Spark Job ID** to ``BestBuy_catalog``
    * Update the **Format** to ``parquet``
    * Update the **Path** to ``gs://training-ecommerce/catalog``
    * Change the **Output Collection** to ``Labs``
    * Copy the **Transform Scala** below and paste it into the **Transform Scala** text box

<pre><code>
<p id="copy">def transform(inputDF: Dataset[Row]) : Dataset[Row] = {
inputDF.filter("department IN ('ACCESSORIES', 'APPLIANCE', 'COMPUTERS')")
}</p>
</pre></code>
<button type="button" onclick="copyEvent('copy')" style="background-color:#C52574;  border: none;
  color: white;
  padding: 5px 16px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;">Copy</button>

<script>
    function copyEvent(id)
    {
        var str = document.getElementById(id);
        window.getSelection().selectAllChildren(str);
        document.execCommand("Copy")
    }
</script> 
<br>

6. Close the **Transform Scala** text box. Click **Save**, then click **Run**, then click **Start**

>Note: Success! The job will take up to three minutes, when it's done, the "running" icon will change to a "sunshine". 

7. Click **Save**

8. Let's add another PBL job. Click **Add+**, from the dropdown menu, click **Parallel Bulk Loader**

9. Click **Advanced**. Let's add some parameters to ingest the data:
    * Update the **Spark Job ID** to ``BestBuy_signals_labs``
    * Update the **Format** to ``parquet``
    * Update the **Path** to ``gs://training-ecommerce/signals``
    * Change the **Output Collection** to ``Labs_signals``
    * Copy the **Transform Scala** below

<pre><code>
<p id="copy2">import java.sql.Timestamp
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
}</p>
</pre></code>
<button type="button" onclick="copyEvent('copy2')" style="background-color:#C52574;  border: none;
  color: white;
  padding: 5px 16px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;">Copy</button>

<script>
    function copyEvent(id)
    {
        var str = document.getElementById(id);
        window.getSelection().selectAllChildren(str);
        document.execCommand("Copy")
    }
</script> 
<br>
        
10. Close the **Transform Scala** text box. Click **Save**, then click **Run**, then click **Start**

>Note: Success! The job will take about up to three minutes, when it's done, the "running" icon will change to a "sunshine". If your job fails, be sure to check your parameters with the configurations above and run the job again. 

# Verify Successful Data Load

11. Hover over **QUERYING**, click on **Query Workbench**
   
12.  Click **Display Fields** in the upper right corner and change the following fields:
* **Name** field to ``name`` 
* **Description** field to ``longDescription``

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%201%20Display%20Fields.png" style="height: 250px; width:320px;"/>

13. Click **Add a field facet** and choose **department**

14. Click **Save**

>Note: If prompted, save over the existing Labs pipeline. 

15. Click the **Collections** dropdown and select **Labs_signals**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%201%20Collections.png" style="height: 250px; width:32
0px;"/>


16. Hover over **QUERYING**, click on **Query Workbench**
   
17.  Click **Display Fields** and change the **Name** field to ``name``

18. If there are no facets, click **Add a field facet** and choose **department**

19. Click **Save**. Confirm that you will save over the existing pipeline.

>Note: Note that these signals contain all the data from the associated catalog item.  This is NOT a recommended design for production, as the signals index would be very large.  However, this can be very useful for our examples, as the click data is easier for us to read and comprehend.

20. Make sure to scroll through all of your open Fusion tabs and **Save** each!

________
Great job! You now have a functioning Fusion app with data from utilizing the Parallel Bulk Loader! If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**

This concludes the PBL Lab.
