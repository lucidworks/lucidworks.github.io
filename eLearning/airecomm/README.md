---
layout: page
title: Recommendations
permalink: /airecomm/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

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
