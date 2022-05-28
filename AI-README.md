---
layout: page
title: AI Readme
permalink: /AI/
---

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
   </code></pre>
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




<link href="../lib/public/global-training.css" rel="stylesheet"></link>

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol.Please do not click *Start Lab* again. It may take a few mintues for the Fusion environment to fully display.

When the Fusion Login page displays, login:
    * USERNAME: ```admin```
    * PASSWORD: ```password123```

## In this lab  you will inspect a collection, train a classifier model, implement classification at query time, and test the classifier pipeline! Let's get started by inspecting the collection on the app that you built in the first lab.

1. Click on the app **Labs** to enter the *Fusion workspace*, this is where you can build and test the classifier model

   # Inspecting the Collection

2. Click the **Collections** dropdown in the top left navigation header and select **Labs_signals**

3. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**

   >Note: In this lab, we will build a classifier that predicts which store department a user is interested in based on their input query. This involves finding correlations between certain query terms and the store department the user ultimately clicks into.

4. Excecute the `query:"washer dryer combo"`

   >Note: Everyone who searched for “washer dryer combo” also clicked on an item from the APPLIANCE department.  Not every query is this clear-cut.

   <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%202%20Query%20example.png" style="height: 200px; width:250px;"/>


5. Execute the query `query:charger`

   >Note: These results are ambiguous,  however there is still a clear trend towards ACCESSORIES. These patterns can be captured and learned by a Classifier; then used to influence relevancy at query time.

   # Training a Classifier Model

6. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**

7. Click **Add+**, from the drop-down menu, select **Logistic Regression Classifier Training**
8. Click **Advanced**. Let's add some parameters:
    * Change the **Spark Job ID** to ``department_qi_model`` 
    * Update the **Training Collection** to ``Labs_signals``
    * Update the **Field to Vectorize** to ``longDescription`` 
    * Update the **Label Field** to ``department``
    * Update the **Auto-balance training classes** to **un-enabled** 
    * Change **Grid Search with Cross Validation** to **enabled** 
    * Update the **Elastic Net Weight** to ``0.2``

<details>

<summary>Why these parameters?</summary> 

|     Parameter    |      Value                   |Explanation                |
|----------------|-------------------------------|-----------------------------|
|Spark Job ID |`department_qi_model`         |Unique name for this job.  This will also be Model name, so make it intuitive          |
|Training Collection      |`Labs_signals`            |Collection from which to pull data.|
|Field to Vectorize         |`longDescription`|The input field. Model will predict a label based on the contents of this field|
|Label Field |`department`         |'The output field.  The model will write its prediction label here.|
|Auto-balance training classes     |`un-enabled`            |Ensure that all classes of training data have the same size|
|Grid Search with Cross Validation       |`enabled`|Cross Validation is always enabled.  This parameter also enables Grid Search, which will experimentally determine the “best” values for Elastic Net Weight and Regularization Weight|
|Elastic Net Weigh  |`0.2`            |The Elastic Net (link) allows smooth interpolation of the L1 and L2 regularization methods.  There is no single “correct” value for this, but a small number between 0 and 1 is a good base.|

</details>

<br/>
9. Click **Save**, then click **Run**, then click **Start**

>Note: Success! The job will take about a minute, when it's done, the "running" icon will change to a "sunshine". 

# Implementing Classification at Query Time

10. Click the **Collections** dropdown and select **Labs**

11. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**

12. Click **New** in the upper right corner of the Query Workbench, then click **Save** in the upper right corner. In the Save Pipeline box, name the new pipeline **Labs_department_QI**, then click **Save**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%202%20New%20Query%20Pipeline.png" style="height: 250px; width:3
00px;"/>

13. Click **Add a Stage** and select **Machine Learning**. Let's add some parameters:
    * Change the **Label** to ``department_QI_classifier`` 

    * Update the **Machine Learning Model ID** to ``department_qi_model``

    * Update the **Model input transformation script** to:
    
* 
<code>
    var modelInput = new java.util.HashMap();
modelInput.put("concatField", request.getFirstParam("q"));
modelInput
</code>
   
14. Update the **Model output transformation script** to:
<code>
request.putSingleParam("predicted_department", modelOutput.get("labelPredictedByFusionModel"));
</code>

15. Click **Apply**, then click **Cancel** to close the query pipeline

>Note: The classifier stage calculates a label in the predicted_department field of each query request but doesn’t do anything with that label.  We will create another stage that uses the label to filter or boost documents based on the label.

16. Click **Add a Stage** and select **Additional Query Parameters**. Let's add some parameters:
    * Change the **Label** to ``QI_department_filter``

    * Under **Parameters and Values**, click **+** to add a new parameter 

      * Change the **Parameter Name** to ``fq`` 

      * Update the **Parameter Value** to ``department:"<predicted_department>"`` 

17. Click **Apply**, then click **Cancel**. 
    * Using the three horizontol lines icon, drag the **QI_department_filter** stage so that it appears after the **department_QI_Classifier** stage in the Query Pipeline stages

18. Click **Save** and save over the existing pipeline

# Testing the Classifier Pipeline

19. Using the **Labs_department_QI** pipeline, excecute the query **ipod cover**

20. Click **Add a field facet** and select **department**

21. Click **Display Fields** in the upper right corner of the Query Workbench and change the **NAME** display field to ``name``

>Note: The classifier associates the query (ipod cover) with COMPUTERS department.  The department filter stage eliminates all documents from every other department.

22. Click the green circle to disable the **QI_department_filter** query pipeline stage. Note that the department facet now includes documents from APPLIANCE, ACCESSORIES and COMPUTERS.

23. Re-enable the **QI_department_filters** query pipeline stage and click on it to open the editor

>Note: Filtering is not the only way we can utilize the classifier label.  In fact, it is probably one of the least effective methods because, in cases where the classifier is “wrong”, the user-desired-department will not appear at all.  Instead, lets use the classifier label to implement a relevance boost.  In this case, the predicted department will still rise to the top of the results, but the other documents are still there to be found in case the prediction was wrong.

24. Change the Parameter Name to ``bq`` and the Parameter Value to ``department:"<predicted_department>"^20``

25. Click **Apply**, then **Cancel**

>Note: Now we get the same COMPUTERS documents in the top results as we did with a Filter Query, but without sacrificing the other documents in case of a classifier mistake.

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%202%20Final%20Edit.png" style="height: 350px; width:300px;"/>


26. Make sure to **Save** your open Fusion Workspace tabs!

________
Great job! You now have a functioning query intent classification model! If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**

This concludes the Building a Query Intent Classifier Lab.


<link href="lib/public/global-training.css" rel="stylesheet"></link>

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol. Please do not click *Start Lab* again. It may take a few mintues for the Fusion environment to fully display.

When the Fusion Login page displays, login:
* USERNAME: ```admin```
* PASSWORD: ```password123```

## In this lab you will ingest data so that you can enhance relevancy using query rewriting! Let's get started by importing the relevancy app

# Configuring the Relevancy App

1. Click on the app **relevancy-app** to enter the *Fusion workspace*, this is where you can ingest the data

2. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**

3. Select and run each of the following jobs in the order listed below:
    * ``relevancy``
    * ``relevancy_signals``
    * ``relevancy_click_signals_aggregation``

>Note: Success! The jobs will take about up to three minutes each, when it's done, the "running" icon will change to a "sunshine". If the job fails initially, rerun the job again.

4. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**. Check the first few results to ensure the job was run successfully

# Relevancy Enhancement Tactics

5. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**. Click on and run ``relevancy_head_tail``

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%203%20Head-tail.png" style="height: 300px; width:500px;"/>

>Note: Success! The job will take about a few minutes, when it's done, the "running" icon will change to a "sunshine". 

6. Hover over the **RELEVANCE** icon in the sidebar, then click **Rules**. A new tab will open in your browser. Keep this tab open as we will revisit it through the training session.

7. Click the **Rewrite** icon in the sidebar to access the Underperforming Query Rewriting dashboard

8. Click **Head/Tail** and find **dsl router** in the list of rewrites

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Head-tail%20rewrites%20nav.png" style="height: 300px; width:500px;"/>

9. Notice that Status is set to auto and that Published is set to yes. This is because the Head/Tail suggestion falls into the auto publish category set by the head-tail relevancy job we noted earlier in training. 
    * Click on **Auto** and select **Approved** to change the status to approved. 
    * The change in status will unpublish the rewrite. To publish, hover over the rule and click the **green up arrow** in the Published column. Confirm you want to publish by clicking **Publish** in the Publish Rules box that appears. 

10. Return to the Fusion tab. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**

11. Toggle off the **Text Tagger** stage in the query pipeline by clicking on the green circle. Update the **View As** option to **Debug**. This is located in the bottom right side of the query workbench

12. Execute a search for **dsl router**

>Note: Notice what Fusion is using to perform this search in the rawquerystring and querystring sections

13. Toggle on the **Text Tagger** stage by clicking on the grey circle. If the view does not automatically update, requery dsl router to see the change

>Note: Notice the search enhancement when we use Query Rewrite principles by turning on the Text Tagger stage. This shows the search enhancement when we use Query Rewrite principles through the Text Tagger stage. Notice the updated search parameters Fusion is using to perform this search in the rawquerystring and querystring sections

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%203%20Query%20Workbench%20Head-tail.png" style="height: 200px; width:400px;"/>

14. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**. Click on and run ``relevancy-spell-correction``

>Note: Success! The job will take about a few minutes, when it's done, the "running" icon will change to a "sunshine". 

15. Return to the **Query Rewriting** browser tab 

16. Click **Misspelling** and find any entry in the list of rewrites

17. Change the **Status** to **Approved** and the **Published** to **Yes**. Remember which one you published becuase you'll need it in the next steps.

18. Return to the Fusion tab. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**

19. Change **View As** to **Results** 

20. Toggle off the **Text Tagger** stage by clicking on the green circle and execute a search for the misspelling rule you approved and published on the Query Rewrites page

21. Toggle back on the **Text Tagger** stage by clicking on the grey circle and observe the difference in the relevancy of results

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%203%20Misspelling.png" style="height: 200px; width:300px;"/>

>Note: Notice the search enhancement when we use Query Rewrite principles by turning on the Text Tagger stage. This shows the search enhancement when we use Query Rewrite principles through the Text Tagger stage. Notice the updated search parameters Fusion is using to perform this search in the rawquerystring and querystring sections

22. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**. Click on and run ``relevancy-phrase-extraction``

23. Return to the **Query Rewriting** browser tab 

24. Click **Phrase** and find any entry in the list of rewrites

25. Change the **Status** to **Approved** and the **Published** to **Yes**. Remember which one you published because you'll need it in the next steps.

26. Return to the Fusion tab. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**

27. Toggle off the **Text Tagger** stage by clicking on the green circle and execute a search for the entry you approved and published on the Query Rewrites page

28. Toggle back on the **Text Tagger** stage by click on the grey circle and observe the difference in the relevancy of results

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%203%20Phrase%20Example.png" style="height: 200px; width:300px;"/>

>Note: Notice the search enhancement when we use Query Rewrite principles by turning on the Text Tagger stage. This shows the search enhancement when we use Query Rewrite principles through the Text Tagger stage. Notice the updated search parameters Fusion is using to perform this search in the rawquerystring and querystring sections

29. Make sure to **Save** your open Fusion Workspace tabs!

________
Great job! You now have functioning query rewrites! If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**

This concludes the Query Rewrites Relevancy Lab.

<link href="lib/public/global-training.css" rel="stylesheet"></link>

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol. Please do not click *Start Lab* again. It may take a few mintues for the Fusion environment to fully display.

When the Fusion Login page displays, login:
* USERNAME: ```admin```
* PASSWORD: ```password123```

## In this lab  you will set up clustering, evaluate results, and tune the clustering job! Let's get started by setting up clustering
 
1. Click on the app **Labs** to enter the *Fusion workspace*, this is where you can build and test document clustering

# Setting up Clustering

2. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**

3. Click **Add**, then select **Document Clustering**

4. Toggle on **Advanced**. Let's add some parameters:
    * Change the **Spark Job ID** to ``product_clustering``
    * Update the **Training Collection** to ``Labs``
    * Update the **Output Collection** to ``Labs``
    * Find **Training Data Sampling Fraction** and input ``0.2``
    * Update the **Field to Vectorize** to ``longDescription``

5. Click **Save**, then **Run**, then **Start**

  <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%204%20Clustering.png" style="height: 250px; width:400px;"/>

>Note: Success! The job will take about a minute, when it's done, the "running" icon will change to a "sunshine". 

# Evaluating Results

6. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**

7. Click **Add a field facet** and select **cluster_label**

8. Click **Add a field facet** and select **freq_terms**

9. Click **View next 10** under the **cluster_label** facet

>Note: The cluster_label field contains the five terms that best define the center of each cluster.  The freq_terms field contains the five terms that appear most often in each cluster.  You will note that, in many cases, the frequent terms in a cluster are also among those those that best define it. The clustering job also identified and labeled oddball documents: abnormally long ones, those too short to determine anything meaningful, and those that do not seem closely related to any of the big clusters.

# Tuning the Clustering Job

10. Hover over the **COLLECTIONS** icon in the sidebar, then click **Collections Manager**

11. Click **New**, and name your new collection **Labs2**.

12. Toggle on **Advanced** and uncheck **Enable Signals**. Click **Save Collection**

13. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**

14. Select the **product_clustering** job and toggle on **Advanced**

15. Modify the following parameters:
    * Change the **Output Collection** to ``Labs2``
    * Update the **Outlier Cutoff** to ``0.02``
    * Update the **Min Possible Number of Clusters** to ``5``
    * Update the **Max Possible Number of Clusters** to ``25``
    * Update the **Word2Vec Dimension** to ``100``
  
16. Click **Save**, then **Run**, then **Start**

>Note: Success! The job will take about a minute, when it's done, the "running" icon will change to a "sunshine". 

17. Click the **Collections** dropdown and select the output collection **Labs2**

18. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**

19. Click **Add a field facet** and select **cluster_label**

20. Click **Add a field facet** and select **freq_terms**

>Note: Explore your clusters. Do they look better than they did previously?

  <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%204Tuning%20Clustering.png" style="height: 250px; width:300px;"/>

21. Make sure to **Save** your open Fusion Workspace tabs!

________
Great job! You now have functioning document clustering in your Fusion instance! If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**

This concludes the Document Clustering Lab.



<link href="lib/public/global-training.css" rel="stylesheet"></link>

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol. Please do not click *Start Lab* again. It may take a few mintues for the Fusion environment to fully display.

When the Fusion Login page displays, login:
* USERNAME: ```admin```
* PASSWORD: ```password123```

## In this lab  you will configure recommendations, verify successful model builds, test item-item recommendations and test user-item recommendations! Let's get started by enabling recommendations

1. Click on the app **Labs** to enter the *Fusion workspace*, this is where you can build and configure recommenders.

2. Hover over the **RELEVANCE** icon in the sidebar, then click **Recommendations**.

3. After reading the dialog box, click **Enable Recommendations**.

# Configuring Recommendations

4. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**.

5. Click **Labs_item_recs**, then toggle on **Advanced**.

>Note: There are two main tasks involved in setting up items-for-user recommendations.  First, it uses existing signals to determine each past user’s level of interest in each item.
Second, it uses past user-item preferences to create a user-item matrix, which can be used both to recommend items to new users and recommend other items that tend to collocate with the one currently clicked.

6. Let's assign job parameters:
    * Expand **TRAINING DATA SETTINGS** and update the **Training Data Sampling Fraction** to ``0.05``
    * Expand **ITEM METADATA SETTINGS** and update the **Item Metadata Collection** to ``Labs``
    * Under **ITEM METADATA SETTINGS**, update the **Item Metadata Join Field** to ``id``
    * Under **ITEM METADATA SETTINGS**, locate the **Add Item Metadata Fields** and click **add** to ``department`` in the text field that appears


7. Click **Save**, but *do not run the job yet*

>The Labs_user_item_prefs_agg job will calculate user-item preferences based on past behavior. The output will be used by Labs_item_recs to create a user-item matrix. This is why we configured that job first. 

8. Click **Labs_user_item_prefs_agg** and toggle on **Advanced**.

9. Uncheck **Aggregate New and Merge with Existing**, then click **Save**. These parameters are only functional for subsequent runs of the job, not on the first run.

  <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%206%20Advanced%20Params.png" style="height: 200px; width:500px;"/>

10. Click **Run**, then click **Start**.

>Note: Success! The job will take about a minute, when it's done, the "running" icon will change to a "sunshine".

11. Return to the **Labs_item_recs** job. Click **Run**, then click **Start**.

>Note: Success! The job will take about a minute, when it's done, the "running" icon will change to a "sunshine".

# Verify Successful Model Build

12. Click the **Collections** dropdown and select **Labs_items_for_user_recommendations**.

13. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**.

14. Click **show fields** under any document.

>Note: The key among the fields here are itemID and userID, representing a single, unique user-item pairing.  The weight field is a prediction of how well this item matches this user, based on the behavior of other users with similar activity. Also note the department field.  This was pulled in by the metadata JOIN we requested in the Labs_item_recommendations job.  This field can be used at query time; for example, to only recommend items from certain departments.

  <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%206%20Verify%20Model.png" style="height: 200px; width:300px;"/>

15. Click the **Collections** dropdown and select **Labs_items_for_item_recommendations**.

16. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**.

17. Click **show fields** under any document.

>Note: Notable fields here are itemId and otherItemId representing a single unique pairing of items. The sim field is a measurement of how “similar” these two items are based on collocation in user activities.
Also note the department field from the metadata JOIN.

# Testing Item-Item Recommendations

18. Click the **Collections** dropdown and select **Labs**.

19. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**.

20. Click **Load** in the upper right corner of the screen and select **Labs_items_for_item_recommmendations**.

21. Select the **Recommend Items for Item** stage. Let's fill out the following parameters:
    * Set the **Boost Param** to ``bq``
> Note: This stage implements a relevance boost for similar items when a single item is “selected” via an item_id parameter.  This parameter will be populated, for example, by going to the details page for a given item. The last three parameters:  Item ID Field, Recommended Item ID Field, Similarity Score Field relate to the structure of the items-for-item documents examined previously

22. Click **Apply**, then click **Cancel** to close the stage.

23. Click **Parameters** in the upper right side of the Query Workbench and select **Edit parameters**.

24. Click the green **+** and add a parameter with a **Parameter Name** of ``item_id`` and a **Value** of ``2460117``. 

25. Click **Close** to apply the parameter.

>Note: This parameter prompts the Recommend Items for Item stage to boost items similar to the one with doc id 246011.

  <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%206%20Edit%20Params.png" style="height: 200px; width:300px;"/>

26. Execute a query for ``id:2460117`` and click **show fields**.

> Note: This item is an SSD drive. The recommender boosts items related to hard drives.

27. Execute a query for ``*:*``, and note that items similar are boosted.

28. Switch to **Labs_items_for_item_recommendations** collection. 
    * If prompted, abandon changes to the existing pipeline
    * Navigate to the **Query Workbench** and execute a query for ``sim:[.997 TO *]``, and add a field facet of **itemId**. *Pick out any one **itemId** in the facet list and remember the **itemId** value for Steps 29-31.* 

>Note: Any items with 10 similar items at such high similarities should look pretty good.  Feel free to adjust the lower bound of the sim query to find the best candidates.

29. Switch back to the collection **Labs**. 

30. Replace the existing **item_id** parameter with the noted **item_id** parameter (*from Step 28*) in the top right of the query workbench.

31. Disable the **Recommended Items for Item** stage in the query pipeline panel and note how the items are back to a pseudo-random document ordering. Re-enable **Recommended Items for Items**

# Testing User-Item Recommendations

32. Click **Load** in the upper right corner of the Query Workbench and select **Labs_items_for_user_recommendations**

>Note: There are two ways to implement a user-item recommendation. First is personalized recommendations where we offer users a list of interesting items before they ask for anything. Second is personalized Search where we apply boost factors to items based on the user-item similarity of the person looking.  

33. Select the **Recommend Items for User** stage.

> Note: The key query parameter is user_id that will generally be populated by a login action  The user-item recommendations collections will be searched for items that have a userId field equal to user_id, and will provide a relevance boost on the associated itemId.  The weight determines the magnitude of the boost.

34. Click **Cancel** to close the stage. Click **Display Fields** and change **Name** to ``name``. Change **Description** to ``longDescription``.

35. Click **Parameters**, then select **Edit Parameters**.

36. Delete the **item_id** parameter and add a new parameter with the **Parameter Name** of ``user_id`` and a **Value** of ``8423cdfb8a15894e414ca32c21f68a95aacc0326``. Click **Close**.

>Note: Enabled parameters should have a green circle next to the parameter name. You can observe the difference in results when the Recommend Items for User stage is disabled by clicking the green circle.

37. Execute a query for ``*:*``, and note the items listed.

  <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%206%20User%20Item%20before.png" style="height: 200px; width:250px;"/>

38. Execute a query for ``laptop`` and note the difference in item order.

  <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%206%20User%20Item%20After.png" style="height: 200px; width:300px;"/>

>Note: The top result for this user was originally 5 ranks lower, without the recommender active.  This is an example of Personalized Search. For better results, use a large sample when building the recommender model.

39. Make sure to **Save** your open Fusion Workspace tabs!

________
Great job! You now have a functioning recommender! If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**

This concludes the Building a Recommender Lab.
