---
layout: page
title: Advanced Readme
permalink: /aiclass/
---

<link rel="stylesheet" href="./lib/public/global-training.css">

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
