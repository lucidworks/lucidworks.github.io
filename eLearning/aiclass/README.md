---
layout: page
title: Classification
permalink: /aiclass/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

## It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Classification Lab! <br> Through this set of lab activities, you will inspect a collection, train a classifier model, implement classification at query time, and test the classifier pipeline.

---
<br>

For this lab, we will be building a classifier that predicts which store department a user is interested in based on their input query. This involves finding correlations between certain query terms and the store department the user ultimately clicks into. We will be doing this using the **Labs** app created in the Intro to Machine Learning lab. 

1. On the Fusion launch page, click the **Labs** app to open it and enter the Fusion workspace.

>Before proceeding with the lab, please navigate to the **Jobs** tab (**Collections > Jobs**). Make sure that both the **BestBuy_catalog** and **BestBuy_signals_labs** jobs have run. If you see a caution sign, please run the job again before continuing on in the lab.

<br>

## Inspecting the Collection

Let's start with an exercise to help understand why using classifiers is a good idea.

2. In the top left corner, click the Collections dropdown, then select the **Lab_signals** collection.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collectiondropdown.png" style="height: 320px; width: 200px;"/>

<br>

3. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list.

 <img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_querying.png" style="height: 300px; width:200px;"/>

<br>
   
4. In the search field, execute a query search for ```"washer dryer combo"```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_wdsearch.png"/>

<br>

Notice in the search results that everyone who searched for “washer dryer combo” also clicked on an item from the APPLIANCE department. Not every query is this clear-cut.

<br>
Let's try another one.

5. In the search field, execute a query search for ```"charger"```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_chargersearch.png"/>

<br>

Notice, that these results are ambiguous, however there is still a clear trend towards ACCESSORIES. These patterns can be captured and learned by a classifier, which can then used to influence relevancy at query time.

<br>

## Training a Classifier Model

Now that we hae a better grasp on why we use classifiers, let's set up the job to train our classifier.

6. In the left navigation pane, click **Collections**, then select **Jobs** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collections.png" style="height: 300px; width: 180px"/>

7. In the Jobs pane, click **Add+** and begin typing ```logistic```, then select **Logistic Regression Classifier Training** from the autosuggestion list.

8. In the job configuration window, enter the following values:
* In the **Spark Job ID** field, enter ```department_qi_model```. 
* In the **Training Collection** field, enter ```Labs_signals```.
* In the **Field to Vectorize** field, enter ```longDescription```. 
* In the **Label Field** field, enter ```department```.

9. Click to enable the **Advanced** fields. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_trainingjobsettings_1.png"/>

<br>

10. Scroll down and click to expand the Model Tuning Parameters section, then make the following selections:
* Deselect the **Auto-balance training classes** field. 
* Select the **Grid Search with Cross Validation** field. 
* In the **Elastic Net Weight** field, enter ```0.2```.

<details>

<summary><b>Why these parameters?</b></summary> 

|     Parameter    |      Value                   |Explanation                |
|----------------|-------------------------------|-----------------------------|
|Spark Job ID |`department_qi_model`         |Unique name for this job.  This will also be the Model name, so make it intuitive.          |
|Training Collection      |`Labs_signals`            |Collection from which to pull data.|
|Field to Vectorize         |`longDescription`|The input field. The model will predict a label based on the contents of this field.|
|Label Field |`department`         |The output field.  The model will write its prediction label here.|
|Auto-balance training classes     |`disabled`            |Disabling this ensures that all classes of training data have the same size.|
|Grid Search with Cross Validation       |`enabled`|Cross Validation is always enabled.  This parameter also enables Grid Search, which will experimentally determine the “best” values for Elastic Net Weight and Regularization Weight.|
|Elastic Net Weight  |`0.2`            |The Elastic Net (link) allows smooth interpolation of the L1 and L2 regularization methods.  There is no single “correct” value for this, but a small number between 0 and 1 is a good base.|

</details>

<br>

11. Click **Save** to create the new job.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_trainingjobsettings_2.png"/>

<br>

12. Click **Run**, then click **Start** in the job dialog to start the job.

>The job will take a couple minutes to run. Note that the **Running** indicator displays while the job is in process, and will change to **Success** when the job is complete.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_runjob.png"/>

<br>

13. Once the job is complete, click **X** to close the job dialog.

<br>

## Implementing Classification at Query Time

Now that we have set up and run the classifier job, let's implement classification in our workspace and view our results.

First, we need to create a new query pipeline.

14. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list.

15. In the top right corner of the Query Workbench window, click **New**, then click **Save**.  

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_addpipeline_1.png"/>

<br>

16. In the Save Pipeline dialog, enter **Labs_department_QI** for the name of the pipeline, then click **Save pipeline**.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_addpipeline_2.png"/>

<br>

Next, let's add a new stage to our pipeline.

17. In the Query Workbench pane, click **Add a Stage** and begin typing ```machine```, then select **Machine Learning** from the autosuggestion list. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_addstage.png"/>

<br>

18. In the stage configuration window, enter the following values:
* In the **Label** field, enter ```department_QI_classifier```. 
* Click in the **Machine Learning Model ID** field and select the ```department_qi_model``` option.

19. Copy and paste the follow value into the **Model input transformation script** field:

```
var modelInput = new java.util.HashMap();
modelInput.put("concatField", request.getFirstParam("q"));
modelInput
```
   
20. Copy and paste the following value into the **Model output transformation script** field:

```
request.putSingleParam("predicted_department", modelOutput.get("labelPredictedByFusionModel"));
```

21. Click **Apply** to create the new ```department_QI_classifier``` stage, then click **Cancel** to collapse the stage configuration window.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_stagefields.png"/>

<br>

This new classifier stage calculates a label in the **predicted_department** field of each query request, but doesn’t do anything with that label.  

Next, we will create another stage that uses the label to filter or boost documents based on the label.

22. Click **Add a Stage**, begin typing ```additional```, then select **Additional Query Parameters** from the autosuggestion list. 

23. In the stage's **Label** field, enter ```QI_department_filter```.

24. In the Parameters and Values section, click the green plus to add a parameter and enter the following values: 
* In the **Parameter Name** field, enter ```fq```.
* In the **Parameter Value** field, enter ```department:"<predicted_department>"```. 

25. Click **Apply** to save your the new ```QI_department_filter``` field, then click **Cancel** to collapse the configuration window. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_filterstagefields.png"/>

<br>

26. Using the stage's hamburger icon, move the **QI_department_filter** stage so that it appears *after* the **department_QI_classifier** stage in the Query Pipeline stages.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_movestage.png"/>

<br>

27. Click **Save** to save your changes to the pipeline, then click **Yes, save over the existing pipeline** to confirm the action.

<br>

## Testing the Classifier Pipeline

Now that our pipeline is set up in the workspace, it's time to test it out.

28. Using the **Labs_department_QI** pipeline, excecute a query for ```ipod cover```.

29. Click **Display Fields**, and enter ```name``` in the **NAME** field.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_namedisplay.png"/>

<br>

30. Click **Add a field facet**, begin typing ```department``` then select **department** in the autosuggestion list.

><b>Note:</b> As displayed in the image below, the classifier associates the query (```ipod cover```) with the COMPUTERS department.  The **QI_department_filter** stage eliminates all documents from every other department.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_filter.png"/>

<br>

31. Click the green circle next to the **QI_department_filter** stage to disable it. 

Notice that the department facet now includes documents from APPLIANCE, ACCESSORIES and COMPUTERS.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_nofilter.png"/>

<br>

Filtering is not the only way we can utilize the classifier label.  In fact, it is probably one of the least effective methods because, in cases where the classifier is “wrong”, the user-desired-department will not appear at all.  

Let's instead use the classifier label to implement a relevance boost.  In this case, the predicted department will still rise to the top of the results, but the other documents are still there to be found in case the prediction was wrong.

32. Click the circle next to the **QI_department_filter** stage to re-enable it. 

33. Click the **QI_department_filter** stage to open the configuration window, then make the following value changes:
* Change the **Parameter Name** field to ```bq```.
* Change the **Parameter Value** to ```department:"<predicted_department>"^20```.

34. Click **Apply** to save your changes to the stage, then click **Cancel** to collapse the stage configuration window and view the changes to your results.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_filterchanges.png"/>

<br>

Notice that now we get the same COMPUTERS documents in the top results as we did with a filter query, but without sacrificing the other documents in case of a classifier mistake.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclass/aiclass_newfilter.png"/>

---
<br>

## Great job! You have successfully completed the Classification Lab, where you have created a functioning query intent classification model.

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