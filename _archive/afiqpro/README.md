---
layout: page
title: Index and Query Profiles
permalink: /afiqpro/
---

<link rel="stylesheet" href="./lib/public/global-training.css">


## The environment should begin to load immediately. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

When the Fusion Login page displays, login:
    
* USERNAME: ```admin```
* PASSWORD: ```password123```

# In this lab  you will learn how to define index pipelines, index data, and utilize query profiles. Let's get started!


> Note: You may need to adjust the size of the instructions panel to fully view results in the UI. Toggle the window sizes as needed.

1. In the Fusion Admin UI, click **Create New App**

2. For App Name, enter ``Profiles_Test``

3. Click **Create App**

4. Click **Profiles_Test** to open your newly created app

5. Hover over INDEXING icon and click: **Index Profiles**
    
> Note that when we create a new App, a default Index and Query profile are created.

We will want to compare two profiles in our experiment, so we will create an additional collection.

6. Hover over COLLECTIONS icon and click: **Collections Manager**

7. Click: **New**

    a. Name this new collection: ``Profiles_Test_2``
    
    b. Cick on the **Advanced** tab to enable it

    c. **Deselect Enable Signals**

    * This prevents axillary signals collections from being created

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Index_and_Query_Profiles_3/Index%20and%20Query%20Profiles_1.png" style="height: 315px; width:550px;">
  
<br>

8. Scroll down and click **Save Collection**

  >In the Collection Manager window you should now see your primary collection and the newly created second collection along with various system collections. 

# Define Index Pipelines

As you can see in the Collections Manager, both of our collections are empty. However, before we populate them, we will need to make some pipeline adjustments.

9. Go to **Index Pipelines** 

10. Select **Profiles_Test** under Existing Pipelines

11. Click **Add a new pipeline stage**

12. Begin typing “regex” and select **Regex Field Extraction**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Index_and_Query_Profiles_3/Index%20and%20Query%20Profiles_2.png" style="height: 375px; width:400px;"/>
  
<br>

13. Enter ``Extract Year`` for **Label**

    a. Under Regex Rules click the **green plus icon** to add a new row

    b. In the Source Fields column, click **[…]**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Index_and_Query_Profiles_3/Index%20and%20Query%20Profiles_3.png" style="height: 315px; width:500px;"/>
  
<br>

14. In the Source Fields window that opens, click the **green plus icon** to add a new source field

    a. Enter ``initial_release_date_dt``

  
15. Click **Apply**

16. Fill out the rest of the row using the table provided

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Index_and_Query_Profiles_3/Screen%20Shot%202021-07-08%20at%205.57.02%20PM.png" style="height: 215px; width:400px;"/>
 
<br>

> **Note:** You can copy and paste the values in the table below:

* Target Field: ```Year```
* Write Mode: ```overwrite```
* Regex Pattern: ```^([0-9]{4})```
* Return If No Match: ```value```
* No Match Literal Value: ```ERROR-PARSING-YEAR```
* Regex Capture Group: ```1```

> **Note:** You may need to use the scroll bar underneath Regex Rules to be able to fill the whole row.

17. Click **Save** to save the Extract Year stage

18. **Move the Extract Year stage** to directly before the Solr Indexer stage using the “hamburger” icon to drag and drop it into place

19. Click **Save** again to save the pipeline stages in this new order

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Index_and_Query_Profiles_3/Index%20and%20Query%20Profiles_4.png" style="height: 375px; width:450px;"/>

<br>

Now we want to perform the same regex extraction for Profiles_Test_2

20. Click the **Collections** drop-down in the upper left

21. Select **Profiles_Test_2**

22. Navigate to Index Pipelines, then click **Add+** to add a new Pipeline

    a. For Pipeline ID, enter ``Profiles_Test_2``

23. Click **Add a new pipeline stage**, and select Regex Field Extraction

    a. For Label, enter ``Extract Year``

    b. Add a new Regex Rule using the values in the table:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Index_and_Query_Profiles_3/Screen%20Shot%202021-07-08%20at%206.07.33%20PM.png" style="height: 215px; width:400px;"/>

<br>

> **Note:** You can copy and paste the values in the table below:

* Source Field: ```initial_release_date_dt```
* Target_Field: ```Year```
* Write Mode: ```overwrite```
* Regex Pattern: ```^([0-9]{4})```
* Return If No Match: ```value```
* No Match Literal Value: ```ERROR-PARSING-YEAR```
* Regex Capture Group: ```1```

24. Click **Save** to save the Extract Year stage

25. Move the **Extract Year** stage to directly *before* the Solr Indexer stage using the “hamburger” icon to drag and drop it into place

26. Click **Save** again to save the pipeline stages in this new order

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Index_and_Query_Profiles_3/Index%20and%20Query%20Profiles_5.png" style="height: 375px; width:450px;"/>

<br>

Since we want to compare pipelines via Profile, we need to make Profiles_Test_2 different than Profiles_Test. For Profiles_Test_2  we will only ingest the subset of the data.

27. Click **Add a new pipeline stage** and select **Include Documents**

28. Input the following into the new pipeline:

    a. Label: ``Only include genre: Drama``

    b. Field: ``genre_txt``

    c. Regex Pattern: ``Drama``

29. Click **Save**

> **Note:** You may need to use the scroll bar underneath Regex Rules to be able to fill the whole row.

30. Move the **Only include genre: Drama** stage to *between* the Extract Year and Solr Indexer stages as shown

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Index_and_Query_Profiles_3/Index%20and%20Query%20Profiles_6.png" style="height: 250px; width:450px;"/>

<br>

31. Click: **Save**

# Indexing Data

32. Switch back to the **Profiles_test** collection.

33. Navigate to **Datasources**, click **Add+**, and select **File Upload**.

34. For DATASOURCE ID, enter ``profiles_test``. For FILE ID, enter ``profiles_test.json``

    a. Save the job before proceeding.

35. **Run** and **Start** the job. Click **Save** after job status reads Success

36. Navigate to the **Query Workbench** to review the imported data

37. Click **Display Fields**

    a. NAME: ``name_s``

    b. DESCRIPTION: ``genre_txt``

38. Click **Add a field facet**

    a. Select **genre_ss**

> Notice that there are 1100 docs returned for this collection (on bottom of window)

39. Click on show fields for one of the documents

>Notice the number and variety of these fields before continuing on.

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Index_and_Query_Profiles_3/Index%20and%20Query%20Profiles_7.png" style="height: 325px; width:580px;"/>

<br>

40. Select **Profiles_Test_2** from Collections Manager

41. Navigate to **Index Profiles** and click on **Profiles_Test**

42. Change the Index Pipeline and Collection to point to **Profiles_Test_2**

43. Click **Save**

44. Navigate to Datasources and click **Add+**

45. Select **File Upload**

    a. Datasource ID: ``profiles_test_2``

    b. Pipeline ID: ``Profiles_Test_2``

    b. FILE ID: ``profiles_test.json``

    c. Save the job before proceeding.

>Notice that the Pipeline now points to **Profiles_Test_2**

46.  **Run** and **Start** the job. Click **Save** after job status reads Success

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Index_and_Query_Profiles_3/Index%20and%20Query%20Profiles_8.png" style="height: 325px; width:580px;"/>

<br>

47. Now that we have indexed both collections, we can compare our results in the **Query Workbench** of each collection.

>Notice that **Profiles_Test_2** contains fewer documents and they all share the **Drama** genre.

# Query Profiles

48. From the Collections Manager, in the collection dropdown, select Profiles_Test

49. Navigate to **Query Profiles**

50. Select Query Profile **Profiles_Test**

51. Under Query Params, scroll down and click **New params**

52. In the window that opens, enter the values from the table below:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Index_and_Query_Profiles_3/Screen%20Shot%202021-07-08%20at%206.38.37%20PM.png" style="height: 150px; width:350px;"/>

<br>

53. Once finished, click **Apply**

## Congratulations! You have successfully completed the Index and Query Profiles lab. If you would like to save your Fusion App to reference later, you can do it now:

1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**



