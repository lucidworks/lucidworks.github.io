---
layout: page
title: Recommendations
permalink: /airecomm/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

# It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Recommendations Lab! <br> Through this set of lab activities, you will configure recommendations, verify successful model builds, test item-item recommendations and test user-item recommendations.

---
<br>

For this lab, we will be using the **Labs** app created in the Intro to Machine Learning lab.

1. On the Fusion launch page, click the **Labs** app to open it and enter the Fusion workspace.

>Before proceeding with the lab, please navigate to the **Jobs** tab (**Collections > Jobs**). Make sure that both the **BestBuy_catalog** and **BestBuy_signals_labs** jobs have run. If you see a caution sign, please run the job again before continuing on in the lab.

<br>

## Configuring Recommendations

For our first activity, we are going to set up some items-for-user recommendations. 

To get started, we need to first enable the use of recommendations in our Labs app.

2. In the left navigation pane, click **Relevance**, then select **Recommendations** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_relevance.png" style="height: 380px; width:200px;"/>

<br>

3. After reading the dialog box, click **Enable Recommendations**.

4. In the left navigation pane, click **Collections**, then select **Jobs** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collections.png" style="height: 300px; width:200px;"/>

<br>

There are two main tasks involved in setting up a job for items-for-user recommendations. 
* First, it uses existing signals to determine each past user’s level of interest in each item. 
* Second, it uses past user-item preferences to create a user-item matrix, which can be used both to recommend items to new users and recommend other items that tend to collocate with the one currently clicked.

Let's start by making some changes to our Item Recommender job. 

<br>
  
5. Click **Labs_item_recs** to open the job configuration window.

6. Click to enable the **Advanced** fields.

7. Click to expand the Training Data Settings section, then enter the following value:
* In the **Training Data Sampling Fraction** field, enter ```0.05```.

8. Click to expand the Item Metadata Settings section, then enter the following values:
* In the **Item Metadata Collection** field, enter ```Labs```.
* In the **Item Metadata Join Field** field, enter ```id```.

9. Navigate to the **Add Item Metadata Fields** section and click **Add**, then enter ```department``` in the text field.

10. Click **Save** to save your change to the job, then click **Cancel** to close the job's configuration window.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airecomm/airecomm_itemrecjobconfig.png"/>

<br>

Before running this job, we also need to make some changes to another job to implement recommendations. 

The **Labs_user_item_prefs_agg** job will calculate user-item preferences based on past behavior. The output will be used by **Labs_item_recs** to create a user-item matrix (which is why we configured that job first).

Let's go make our updates to the Preferences job.

11. Click **Labs_user_item_prefs_agg** to open the job configuration window.

12. Click to enable the **Advanced** fields.

13. Deselect **Aggregate New and Merge with Existing** option.

14. Click **Save** to save your changes to the job.

><b>Note:</b> This parameter change is only applicable to subsequent runs of the job, not on the first run.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airecomm/airecomm_prefjobconfig.png"/>

<br>
Now that everything is set up, it's time to run both jobs, starting with the Preferences job. 

15. Click **Run**, then click **Start** in the job dialog to start the **Labs_user_prefs_agg** job.

>The job will take a couple minutes to run. Note that the **Running** indicator displays while the job is in process, and will change to **Success** when the job is complete.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airecomm/airecomm_runjob.png"/>

16. Once the job is complete, click **X** to close the job dialog.

17. Reopen the **Labs_item_recs** job, and repeat steps 15-16 to run the job. 

<br>

## Verify Successful Model Build

Now that we have successfully run the jobs, let's take a moment to review the results in the collections.

18. In the top left corner, click the Collections dropdown, then select the **Labs_items_for_user_recommendations** collection.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collectiondropdown.png" style="height: 300px; width: 200px"/>

<br>

19. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_querying.png" style="height: 300px; width: 200px"/>

<br>

20. In the search results window, click **show fields** under the first document.

<br>

There are several fields displayed that we want to take note of:
* The <b>itemID</b> and <b>userID</b> fields, which represent a single, unique user-item pairing.  
* The <b>weight</b> field is a prediction of how well this item matches this user based on the behavior of other users with similar activity.
* The <b>department</b> field (which was pulled in by the metadata JOIN we requested in the <b>Labs_item_recommendations</b> job), can be used at query time, for example, to only recommend items from certain departments.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airecomm/airecomm_itemuserrecomm.png"/>

<br>

21. In the top left corner, click the **Collections** dropdown, then select the **Labs_items_for_item_recommendations** collection.

22. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list.

23. In the search results window, click **show fields** under the first document.

Similar to our item-user recommendations, the <b>itemId</b> and <b>otherItemId</b> fields represent a single unique pairing of items, and we see the <b>department</b> field from the metadata JOIN. The item-item recommendations results also display a <b>sim</b> field, which is a measurement of how “similar” these two items are based on collocation in user activities.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airecomm/airecomm_itemitemrecomm.png"/>

<br>

## Testing Item-Item Recommendations

For our next lab activities, we are going to test the item-item recommendations feature.

Let's start with the item-item recommendations.

24. In the top left corner, click the **Collections** dropdown, then select the **Labs** collection.

25. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list.

26. In the top right corner, click **Load**, then select **Labs_items_for_item_recommmendations** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airecomm/airecomm_loadjob.png"/>

<br>

27. Select the **Recommend Items for Item** stage and enter the following value:
* Click the **Boost Param** field and select the ```bq``` option.

This stage implements a relevance boost for similar items when a single item is “selected” via an **item_id** parameter. This parameter will be populated, for example, by going to the details page for a given item. 

The last three parameters - **Item ID Field**, **Recommended Item ID Field**, and **Similarity Score Field** - relate to the structure of the items-for-item documents examined previously.

<br>

28. Click **Apply** to save your changes to the stage, then click **Cancel** to collapse the stage configuration window.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airecomm/airecomm_boostparam.png"/>

<br>

29. In the top right corner, click **Parameters** and select **Edit parameters**.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airecomm/airecomm_parameters.png"/>

<br>

30. In the Parameters and Values dialog, click the green plus icon to add a new parameter and enter the following values:
* In the **Parameter Name** field, enter ```item_id```.
* In the **Parameter Value** field, enter ```2460117```. 

><b>Note:</b> This parameter prompts the Recommend Items for Item stage to boost items similar to the one with doc id 2460117.

31. Click **Close** to apply the parameter and close the dialog.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airecomm/airecomm_itemidparam.png"/>

<br>

32. Execute a search for ```id:2460117``` and click **show fields** to display the item details.

Notice that this item is an SSD drive. When we execute another query, the recommender boosts items related to hard drives.

Let's try that now.

33. Execute a query for ``*:*``.

Notice that the parameter has been applied, and similar items are now boosted.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airecomm/airecomm_itemrecomm.png"/>

<br>

Let's explore another test of our recommendations.

34. Switch to the **Labs_item_for_item_recommendations** collection.

>If prompted, go ahead and abandon your changes to the existing pipeline.

35. Navigate back to the Query Workbench and execute a search for ```sim:[.997 TO *]```.

36. Click **Add a field facet**, begin typing ```item```, then select **itemId** in the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airecomm/airecomm_itemidfacet.png"/>

<br>

When reviewing our facet results, note that any items with 10 similar items at such high similarities should look pretty good.  (Feel free to adjust the lower bound of the sim query to find the best candidates).

37. Pick out any one **itemId** in the facet list and record the **itemId** value for use in step 41.

38. Switch back to the collection **Labs**. 

39. In the top right corner, click **Load**, then select **Labs_items_for_item_recommmendations** from the list.

40. In the top right corner, click **Parameters** and select **Edit parameters**.

41. For the **item_id** parameter, enter the new parameter value that you recorded in step 37, then click **Close** to apply the parameter and close the dialog.

42. In the Query Pipeline pane, disable the **Recommended Items for Item** stage.

When the pipeline stage is disabled, note that the items are back to a pseudo-random document ordering. 

43. Re-enable the **Recommended Items for Items** stage before continuing on in the lab.

<br>

# Testing User-Item Recommendations

Now that we have explored how item-item recommendations work, let's explore item-user recommendations in Fusion.

There are two ways to implement a user-item recommendation. First is personalized recommendations where we offer users a list of interesting items before they ask for anything. Second is personalized search where we apply boost factors to items based on the user-item similarity of the person looking.  

44. In the top right corner, click **Load**, then select **Labs_items_for_user_recommendations** from the list.

>If prompted, go ahead and abandon your changes to the existing pipeline.

45. Click **Recommend Items for User** to open the stage's configuration window.

The key query parameter is **user_id**, which will generally be populated by a login action.  The user-item recommendations collections will be searched for items that have a userId field equal to **user_id**, and will provide a relevance boost on the associated itemId.  The weight determines the magnitude of the boost.

46. Click **Cancel** to close the stage's configuration window. 

47. Click **Display Fields** and change the following values:
* In the **Name** field, enter ```name```.
* In the **Description** field, enter ```longDescription```.

48. Click **Parameters**, then select **Edit Parameters**.

49. Delete the **item_id** parameter, then click the green plus icon to add a new parameter with the following values:
* In the **Parameter Name** field, enter ``user_id``.
* In the **Parameter Value** field, enter ``8423cdfb8a15894e414ca32c21f68a95aacc0326``. 

50. Click **Close** to apply the parameter and close the dialog.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airecomm/airecomm_itemuserrparam.png"/>

<br>

Let's take a look at the impact these changes have on our search results.

51. Execute a search query for ``*:*``, and take a moment to observe the documents returned. 

  <img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airecomm/airecomm_itemusergeneral.png"/>

  <br>

52. Next, execute a search query for ``laptop``.

Note the difference in item order. The top result for this user returned very different items without the recommender active.  

This is an example of personalized search. For better results, use a large sample when building the recommender model. Feel free to execute different searches and explore more before ending the lab experience.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airecomm/airecomm_itemuserlaptop.png"/>

---
<br>

## Great job! You have successfully completed the Recommendations Lab, where you have learned to utilize recommendations to enhance your search results. 

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