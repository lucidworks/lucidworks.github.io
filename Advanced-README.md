---
layout: page
title: Advanced Readme
permalink: /Advanced/
---

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

When the Fusion Login page displays, login:
    * USERNAME: ```admin```
    * PASSWORD: ```password123```

# In this lab  you will learn how to use the eDisMax Parser, facets, and function queries. Let's get started!

> Note: You may need to adjust the size of the instructions panel to fully view results in the UI. Toggle the window sizes as needed.

1. In the launcher, click on the app **Online_Shoes**

2. Hover over QUERYING and click **Query Workbench**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/query_workbench.png" style="height: 185px; width:300px;"/>

<br>


3. In the Query Workbench window, click the Display Fields dropdown and change the display fields to **Name** and **Description**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/name_description.png" style="height: 259px; width:350px;"/>

<br>


# Using the eDisMax Parser

4. On the top of the page, enter a query in the search field for **canvas wedge sandal**. 

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/canvaS_wedge_sandal_query.png" style="height: 63px; width:500px;"/>

<br>

5. Deselect **Query Fields**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/deselect.png" style="height: 288px; width:200px;"/>

<br>


6. Click the **Add a Stage** button to add a stage and select **Additional Query Parameters**. 

    a. For label, enter **myQueryParams**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/additional_quer_parameters.png" style="height: 278px; width:300px;"/>

<br>


7. In this stage, under **Parameters and Values**, add a parameter by clicking the green plus sign **(+)** under Parameters and Values. Enter the following values in the fields:

    a.  Name: **defType**
    
    b. Value: **edismax**

    c. Update: **append**

    <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/parameters_and_values.png" style="height: 100px; width:340px;"/>
    
    <br>

8. Add another parameter by clicking the green plus sign **(+)** under Parameters and Values. Enter the following values in the fields:

    a. Name: **mm**

    b. Value: **2**

    c. Update: **append**

9. Click **Apply**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/p_v_2.png" style="height: 300px; width:400px;"/>

<br>

> Note: Parameter mm (minimum match) is an eDisMax parameter that specifies the minimum number of terms that need to match in a Disjunction (OR) query. In this case, 2 of 3 terms in the search need to be found in the doc.

10. Look at your results again.
Notice the total number of docs returned. 

    There are much fewer docs that match 2 out of 3 of the terms.
    Try changing mm to 3 and look at the results again.
    

 # Boosting with eDisMax

11. Query search for ```*:*```

12. In the **myQueryParams** stage, under **Parameters and Values** add another parameter and enter the following values in the fields:

    a. Name: ``boost``
    
    b. Value: ``recip(ms(NOW,dateAdded_dt),3.16e-11,10,1)``
    
    c. Append
    
   >Note: You can copy the values above and paste them into the fields in the lab

13. Click: **Apply**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/p_v_3.png" style="height: 350px; width:350px;"/>

<br>


>Note: This is a common Reciprocal function used on Date fields to give more weight to recent dates.

>You can observe that more recent documents are now on top by looking at the dateAdded_dt field.
boost multiplies the function by the BM25 of the search.

>The boosting factor is the number 10 (in red) in the formula above. Try changing this number and see how the score changes.

14. Change States:

    a. Deselect **myQueryParams**

    b. Select **Query Fields**

15. Click: **Save**

    a. Click **Yes, save over the existing pipeline**


<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/deselect_myqueryparams_select_query_fields.png" style="height: 361px; width:268px;"/>

<br>

# Facet Exploration

16. While in the **Query Workbench**, click the **Facets** pipeline stage

17. Click the green plus sign **(+)** under **Facet Fields**, and enter facets for the following fields:

    a. ``sizes``
    
    b. ``brand``
    
    c. ``colors``
    
    d. ``{!ex=dt}sizes``

    e. ``{!ex=dt}brand``

18. Click **Apply**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/facets.png" style="height: 300px; width:500px;"/>

<br>

>This ex parameter excludes everything but the sizes and brand fields from the other facets that used that field.

You will now see multi-select facets for the sizes and brand field facets. If you wanted to find Nine West and Easy Spirit, size 8 shoes

19. Click the following facets:

    a. **8 under sizes**

    b. **Nine West** and **Easy Spirit** under brand

Try other combinations to explore your results.

>Note also that you could easily add a multi-select field facet for colors as well.


# Function Queries

Let’s use a Function Query to find the frequency of a term within a field.

20. De-select all field facets from the prior section

21. Execute a query in the search bar for: 
``termfreq(colors, 'Multicolor')``

Notice the score is determined by the function and the number of documents returned is based on function results

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/function_queries.png" style="height: 250px; width:450px;"/>

<br>


Let’s try using a field that uses TF-IDF to make our results more accurate.

22. Execute a query for: 
``tf(colors, 'Multicolor’)``

These results are more accurate because in addition to term frequency, we are incorporating inverse document frequency

# Additional Query Parsers

For this next section, we will need some data that contains latitude and longitude fields. Our shoes dataset doesn’t include this, so we will use separate dataset with a new app.

23. Click **Save** to save the work you have done in the Query Workbench

    a. Save over the existing pipeline.

    b. Click the upper-left icon and select Return to launcher
    
    <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/Screen%20Shot%202021-11-22%20at%2011.31.43%20AM.png
" style="height: 225px; width:302px;"/>

24. Create a new app called **citibikes**

25. Once it is created, click on the app to open it

26. Navigate to **Fields** by hovering over COLLECTIONS and selecting Fields


We will ingest this citibikes datasource ad-hoc without a schema pre-defined. We will end up with a field with Lat/Long data called start_station_s. However, this will be a String field and it is not suitable for Lat/Long calculations.

We need to copy this field to a location type of field that supports Lat/Long.

Similarly, we will have a field birth_year_s which we need to calculate a range on. We need to copy this field to a pint type of field that will better support ranges

27. Click **Add a Field +** and enter the following values in the fields:

    a. Field Name: ``start_station_p``

    b. Field Type:  select ``location_rpt``

    c. Select **Indexed**, **Stored**, and **Multivalued**

    d. Click **Save** to save the field parameters

    <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/query_params_citibikes.png" style="height: 350px; width:500px;"/>
    
    <br>

We will copy the value of the start_station_s field into this new field, start_station_p for more usable Lat/Long calculations.

28. Click **Add a Field+**

    a. Field Name: ``birth_year_pint``
    
    b. Field Type: ``pint``

    c. Select **Indexed** and **Stored** only

29. Click Save to save the field parameters

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/query_params_citibikes2.png" style="height: 375px; width:350px;"/>

<br>

We will copy the value of the birth_year_s field into this new field, birth_year_pint for more proper Date calculations

30. Hover over INDEXING, and click **Datasources**

31. Click **Add+** and select **File Upload** and enter the following values in the fields

    a. Datasource ID: **citibikes**

    b. Change the parser to **citibikes**

    c. File ID: **citibike.csv**

32. Click **Save**.

>**Important**: DO NOT start the job yet. We still need to modify our Index Pipelines to set up the field copying process.

33. Click the **link to the right** of the citibikes Pipeline ID
This is a shortcut into the Index Pipeline tab.

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/Screen%20Shot%202021-11-22%20at%2011.25.32%20AM.png" style="height: 53px; width:248px;"/>

<br>

34. In the Index Pipelines panel, click **Add a new pipeline stage**

    a. Select **Field Mapping**

35. For the label, enter: **Copy Location and Pint Fields**

    Scroll down to the **Field Translations** section

    a. Click the green plus icon and add:

    b. Source Field: ``start_station_s``

    c. Target Field: ``start_station_p``

    <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/Field%20Translations.png" style="height: 150px; width:400px;"/>
    
    <br>

    >Note:  Do not save the pipeline yet.

36. Under **Field Translations** add a second source field:

    a. Source Field: ``birth_year_s``

    b. Target Field: ``birth_year_pint``

37. **Save** the stage

38. Move this stage *after* the Solr Dynamic Field Mapping stage by dragging with the “hamburger” icon

39. Navigate back to the **Datasources** window

40. Click **Run**

41. Click **Start**

    >Note: Please be patient! This job can take around 5 minutes to complete

42. Click **Save**

Let's use some query parameters to answer the following question:
How many stations are 1 km from the start station that has coordinates of 40.70,-73.99?

43. Navigate to the **Query Workbench**

44. Click **Display Fields**

    a. Name: ``start_station_p``

    b. Description: ``birth_year_pint``

    <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/display_fields.png" style="height: 350px; width:500px;"/>

<br>

45. Click **Add a Stage**

46. Select **Additional Query Parameters**

47. Add Parameters and Values as shown below:


    fq: ```{!geofilt sfield=start_station_p}```

    pt: ```40.70,-73.99```

    d: ```1```

48. Click **Apply**

You can now see the number of stations returned.

We will use this same stage to answer:
Find all stations that were built between 1980-1983.

49. **Remove** the parameters d and pt

50. Change the value of fq:  ``{!terms f=birth_year_s}1980,1981,1982,1983``

    <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Advanced_queries/fq.png" style="height: 350px; width:450px;"/>
    
    <br>

51. Click **Apply**

The results show all the stations build in that time frame and the total number within the collection.

We will use this stage to answer one additional question:
Find all stations build between the years 1988 to 1990.

52. Change fq to: ``{!frange l=1988 u=1990}birth_year_pint``

53. Click **Apply**

54. Click **Display Fields**

55. Name: ``start_station_name_s``

Notice that this time we used a range function to find our results. This saves us from having to include every year.

_________

If you would like to save your Fusion App to reference later, you can do it now:

1. Return to the Fusion Launcher

2. Hover over your app and click on the cog that appears in the lower right corner
Within the box that opens, click **Export app to zip** 

_________

## Congratulations! By now you should be more comfortable using the eDisMax Parser, facets, and function queries. If you would like to save your Fusion App to reference later, you can do it now:

1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**


<link rel="stylesheet" href="lib/public/global-training.css">

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

When the Fusion Login page displays, login:
    * USERNAME: ```admin```
    * PASSWORD: ```password123```


# In this lab  you will learn how to use clean-up jobs, REST call jobs, and job management. Let's get started!


> Note: You may need to adjust the size of the instructions panel to fully view results in the UI. Toggle the window sizes as needed.

1. Click on the app **Online_Shoes** to enter the *Fusion workspace*

2. Hover over the Collections icon and click **Collections Manager**

Notice the system_logs collection. This collection has potential to increase in size exponentially in production. 

If you are not using these logs for further log analytics, or you are interested in analysis of only recent logs, it is better to get rid to these to prevent running into disk space issues. 

 <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Jobs_and_scheduling/systems_logs.png" style="height: 250px; width:550px;"/>
 
 <br>

3. Hover over Collections icon and click **Jobs**

4. Click  **Add+**

5. Begin typing “log” and select **Log Cleanup** from the dropdown

6. In the Log Cleanup window:

    a. ID: **LogCleanupSchedule1**

    b. Logs Collection: **system_logs**

    c. Delete Logs older than N days: **1**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Jobs_and_scheduling/log_cleanup.png" style="height: 150px; width:550px;"/>

<br>

7. Click **Save**

Notice now in the Jobs list that we have not only the LogCleanupSchedule1 job, but another job labeled 
**delete-old-system-logs**

8. Click on **delete-old-system-logs** to take a closer look at this job

Notice that this job is nearly identical to the job we just created. 

9. Click **Delete job**

10. In the window that appears click **Yes, delete**


# REST Call Jobs

11. Hover over Collections icon and click **Jobs**

12. Click  **Add+**

13. Begin typing “REST” and select **REST Call** from the dropdown

14. In the Rest Call window:

    a. ID: ``Message-Clean-up-Schedule1``

    b. Endpoint URI: ``solr://system_message/update``

    c. Call Method: **post**

We are now using a REST Call job to further clean up our Systems Collections.

15. Click **+** under Query Parameters

    a. Property Name: ``wt``

    b. Property Value: ``json``

16. Under Request Protocol Headers: 

    a. Request Entity (as string) 

 **Copy** the string and paste it into the Request Entity

```
    <root><delete><query>timestamp_dt:[* TO NOW-30DAYS] AND type_s:history</query></delete><commit /></root>
```

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Jobs_and_scheduling/rest_call_query_params.png" style="height: 350px; width:550px;"/>

<br>

17. Click **Save**

# Job Management

There are multiple ways to manage and schedule your jobs. We will look at a few.

Our first scenario is that our system logs collection does not need to be cleaned so often.

18. Click on **LogCleanupSchedule1**

19. Delete Logs older than N days: **5**

20. Click **Save**

Our second scenario is that our system messages collection is taking up too many resources.

21. Click on **Message-Clean-up-Schedule1**

22. Under Request Entitiy (as string), change: 

    ```[* TO NOW-30DAYS]``` to ```[* TO NOW-15DAYS]```

23. Click **Save**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Jobs_and_scheduling/message_cleanup.png" style="height: 350px; width:550px;"/>

<br>

We can use the Scheduler within the Fusion UI to manage jobs.

24. Hover over SYSTEM and click: **Scheduler**

In this last scenario, the job history collection is eating far too much memory.

25. Click on **delete-old-job-history**

26. Under Cronbtab Expression, change: 
    ```0 25 4 ? * SUN``` to

	```0 30 3 ? * SUN,TUE,THU *```

27. Click **Save**

We have changed the schedule of the job from “4:25:00 AM on every Sunday, every month” to “3:30 AM on Sunday, Tuesday, and Wednesday, every month.”
_______

If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**
_______

## Congratulations! You have successfully created clean-up jobs and REST call jobs, and should now be more familiar with job management.


If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**



<link rel="stylesheet" href="../lib/public/global-training.css">

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

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

35. **Run** and **Start** the job. Click **Save** after job status reads Success

36. Navigate to the **Query Workbench** to review the imported data

37. Click **Display Fields**

    a. NAME: ``name_s``

    b. DESCRIPTION: ``genre_txt``

38. Click **Add a field facet**

    a. Select **genre_ss**

> Notice that there are 1100 docs returned for this collection (on bottom of window)

39. Click on show fields for one of the documents

Notice the number and variety of these fields before continuing on.

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Index_and_Query_Profiles_3/Index%20and%20Query%20Profiles_7.png" style="height: 325px; width:580px;"/>

<br>

40. Select **Profiles_Test_2** from Collections Manager

41. Navigate to **Index Profiles** and click on **Profiles_Test**

42. Change the Index Pipeline and Collection to point to **Profiles_Test_2**

43. Click **Save**

44. Navigate to Datasources and click **Add+**

45. Select File Upload

    a. Datasource ID: **profiles_test_2**

    b. Choose to upload profiles_test.json

46. Click **Upload File** and then click **Save**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Index_and_Query_Profiles_3/Index%20and%20Query%20Profiles_8.png" style="height: 325px; width:580px;"/>

<br>

>Notice that the Pipeline now points to Profiles_Test_2

# Query Profiles

47. From the Collections Manager, in the collection dropdown, select Profiles_Test

48. Navigate to **Query Profiles**

49. Select Query Profile **Profiles_Test**

50. Under Query Params, scroll down and click **New params**

51. In the window that opens, enter the values from the table below:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Index_and_Query_Profiles_3/Screen%20Shot%202021-07-08%20at%206.38.37%20PM.png" style="height: 150px; width:350px;"/>

<br>

52. Once finished, click **Apply**

_______

If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**
_________

## Congratulations! You have successfully completed the Index and Query Profiles lab. If you would like to save your Fusion App to reference later, you can do it now:

1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**



<link rel="stylesheet" href="lib/public/global-training.css">

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

When the Fusion Login page displays, login:
    * USERNAME: ```admin```
    * PASSWORD: ```password123```

# In this lab  you will learn how to modify a document via REST Call, as well as authenticate a REST call. Let's get started!


> Note: You may need to adjust the size of the instructions panel to fully view results in the UI. Toggle the window sizes as needed.


# Modifying a Document via REST Call

1. In the Fusion Admin UI, click **Create New App**

2. For App Name, enter **JS Labs**

3. Click **Create App**

4. Click **JS Labs** to open your newly created app

5. Hover over INDEXING and click **Datasources**

6. Click: **Add+**

7. Begin typing “web” and select the **Web** result

8. For Datasource ID, enter: **Lucidworks_website**

    a. For PIPELINE ID, enter **JS_Labs**

    b. For PARSER, enter **JS_Labs**

>Note: The values for PIPELINE ID and PARSER may already be populated

9. Click **Add** next to **Start Link** and enter: ``https://lucidworks.com``

10. Scroll down and expand **Limit Documents**

    a. Max Crawl Depth: **1**

    b. Max Items: **10**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Javascript_1.png" style="height: 425px; width:475px;"/>

<br>

> **Note:** This ensures that our indexing job will only take a small sample of data.

11. Click: **Save**, **Run**, then **Start** and wait until the job shows success

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Screen%20Shot%202021-11-23%20at%2012.41.08%20PM.png" style="height: 282px; width:544px;"/>

<br>

In this task we will set up a JS stage that instantiates an HTTP client, accesses a URL, and uses data from that URL to modify the pipeline document

12. Navigate to **Index Pipelines**

13. Select pipeline: **JS_Labs**
    
14. Click **Add a new pipeline stage** and select **JavaScript** for the stage type

15. For Label, enter: **REST Call**

16. Find the Script Body, clear what is in it by default, and copy and paste the following to it:

```Javascript
function(doc){
  var e = java.lang.Exception;
  try{  
  }catch(e){
    logger.error(e.getLocalizedMessage());
  }
  return  doc;
}
```
<br>

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Screen%20Shot%202021-11-10%20at%204.15.02%20PM.png" style="height: 288px; width:500px;"/>

<br>

> **Note:** Embedding most of the functional code in a try-catch is a best practice for code safety

17. In the Script Body of the REST Call stage, add these class declarations <u>above</u> the **try clause**:

> Note: For reference, see screenshot below

```Javascript
var BufferedReader = java.io.BufferedReader;
  var InputStreamReader = java.io.InputStreamReader;
  var HttpResponse = org.apache.http.HttpResponse;
  var HttpClient = org.apache.http.client.HttpClient;
  var HttpGet = org.apache.http.client.methods.HttpGet;
  var StringBuffer = java.lang.StringBuffer;
  var String = java.lang.String;
  var userAgent = org.apache.http.HttpHeaders.USER_AGENT;
  var HttpClientBuilder = org.apache.http.impl.client.HttpClientBuilder;
```

The first thing this stage will do is set up an HTTP client and a REST request

<br>

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Screen%20Shot%202021-11-10%20at%204.20.02%20PM.png" style="height: 267px; width:500px;"/>

<br>

18. In the Script Body of the REST Call stage, <u>after</u> the variable definitions, add the following within the **try clause**:

```Javascript
 var client = HttpClientBuilder.create().build();
 var url = new String("http://www.google.com/search?q=httpClient");
 var request = new HttpGet(url);
 request.addHeader("User-Agent", userAgent);
```
<br>

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Screen%20Shot%202021-11-22%20at%2012.09.08%20PM.png" style="height: 517px; width:650px;"/>

<br>


The URL we are fetching is not very interesting nor is it related to the Lucidworks.com site that the documents are coming from.  It serves the purpose of illustrating how such a request can be made.


Next, the stage will execute the REST call and construct a response object to parse

19. In the Script Body add the following to the <u>end</u> of the **try clause**:

```Javascript
var response = client.execute(request);
 var rd = new BufferedReader(new InputStreamReader(response.getEntity().getContent()));
 var result = new StringBuffer();
 var line = "";
 while ((line = rd.readLine()) !== null) {
   result.append(line);
 } 
```

<br>

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Screen%20Shot%202021-11-09%20at%205.24.18%20PM.png" style="height: 262px; width:500px;"/>

<br>

Finally, the stage will parse the response using Jsoup, fetch the URL’s title, and attach that title to the Pipeline Document in the sub_title field

20. In the Script Body, add the following to the <u>end</U> of the **try clause**:

```Javascript
var Jsoup = org.jsoup.Jsoup;
 var httpDoc = Jsoup.parse(result);
 var httpTitle = httpDoc.select("title").first();
 doc.addField("sub_title", httpTitle);
 } 
```

<br>

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Screen%20Shot%202021-11-09%20at%205.28.50%20PM.png" style="height: 246px; width:500px;"/>

<br>

21. **Close** the Script Body editor and **save** the updated REST Call stage

22. Return to the Datasource window and **clear the Datasource**, then **re-run**, **start** and **save** the Lucidworks_website datasource

23. Navigate to the **Query Workbench**. There should be a total of 10 docs or less

If you look at the Job History for the Lucidworks_website datasource, you will see that its last successful run took ~10 seconds.  Given that it only produces ~30 documents, that is absurdly slow.  The reason for this is that setting up and using an HTTP Client is not very fast.  

Since the client we set up and the URL we fetch are the same every time, we can instead make this stage stateful.  It will execute the client setup and REST call once, save the result, and use that saved result every time the stage runs.
<br>

24. Return to the **Index Pipelines** window

25. In the Script Body of the REST Call stage, add the following class declaration <u>just above</u> the **try clause**:

```var System = java.lang.System;```

The Script Body should look like this (see line 12):

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Javascript_2.png" style="height: 275px; width:525px;"/>

<br>

26. Add the following line just <u>above</u> the **doc.addField line**:

```
System.setProperty("page_sub_title", httpTitle);
```


This saves httpTitle as a Java system property, so that it is persists between starts and stops of this stage

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Javascript_3.png" style="height: 175px; width:375px;"/><br>

Now that we have made the httpTitle persistent, we need to add a conditional to the function so that the HTTP Client will only be created if the target system property is empty.  Otherwise, the function should fetch the system property and skip client creation and REST call execution

27. Add the following <u>just beneath</u> the **try clause** declaration:

```
var httpTitle = "";
  if(System.getProperty("page_sub_title") == null){
```
<br>


So it looks like this:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Javascript_4.png" style="height: 110px; width:375px;"/>

<br>

28. Now, add the following <u>just</u> above the **doc.addField** line:

```
 } else {
   httpTitle = System.getProperty("page_sub_title");
 }
```
<br>

So it looks like this:


<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Javascript_5.png" style="height: 110px; width:375px;"/>

<br>

29. Close the Script Body editor

30. **Save** the updated REST Call stage

31. **Clear** and **re-run** the Lucidworks_website datasource

32. Once the datasource finished, check the **Job History**

Now the job should only take 3-5 seconds.

# Authenticating a REST Call

In the last task, we set up a JS stage that modified a document with information from a REST call.  But what do we do if the endpoint requires authentication?  That’s what this lab will explore.

In this case, we will use Fusion as our target endpoint, using the admin password you’ve already created.

33. Navigate to **Index Pipelines**

34. Select the **JS_Labs** pipeline

35. Add a new JavaScript stage

36. For Label, enter: **Authenticated Call**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Javascript_6.png" style="height: 275px; width:355px;"/>

<br>

37. Add the following to the **Script Body**:

```Java
function(doc){
var e = java.lang.Exception;
  try {
  } catch (e) {
    logger.error("Error getting httpclient " + e.getLocalizedMessage());
  }
  return  doc;
}
```

<br>


38. In the Script Body, add the following class declarations <u>to the top</u> of **function(doc)**:

```Javascript
var UsernamePasswordCredentials = org.apache.http.auth.UsernamePasswordCredentials;
  var AuthScope = org.apache.http.auth.AuthScope;
  var BasicCredentialsProvider = org.apache.http.impl.client.BasicCredentialsProvider;
  var HttpClientBuilder = org.apache.http.impl.client.HttpClientBuilder;
  var HttpPost = org.apache.http.client.methods.HttpPost;
  var StringEntity = org.apache.http.entity.StringEntity;
```

39.  Add credentials to the block of class declarations <u>at the top</u> of **function(doc)**:

```Javascript
 var pwd = "password123";
 var user = "admin";
 var fusionUrl = "http://localhost:8764";
 var client = null;
```
<br>


 So it looks like this:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Javascript_8.png" style="height: 310px; width:575px;"/><br>

Now that the building blocks are in place, we can instantiate the client 

40. Add the following code to the **try clause** <u>within</u> **fuction(doc)**:

```Javascript
var authJson = "{\"username\":\"" + user + "\", \"password\":\"" + pwd + "\"}";
    var authUrl = fusionUrl + "/api/session?realmName=native";
    var provider = new BasicCredentialsProvider();
    var credentials = new UsernamePasswordCredentials(user, pwd);
    provider.setCredentials(AuthScope.ANY, credentials);
    var client = HttpClientBuilder.create()
       .setDefaultCredentialsProvider(provider)
       .build();
```
<br>

Finally, we can use the client-plus-credentials to build a REST call and establish an authenticated session

41. Add the following code to the <u>end</u> of the **try clause** <u>within</u> **function(doc)**:

```Javascript
var session = new HttpPost(authUrl);
    var params = new StringEntity(authJson);
    session.addHeader("content-type", "application/json");
    session.setEntity(params);   
    var response = client.execute(session);
```
<br>

If you feel your codes aren't working, you can copy the full codes for the REST Call and the Authenticated Call pipelines below and paste them into the script bodies

<details>

<summary>Click to expand the REST Call full script body </summary> 

```Javascript
function(doc){
  var e = java.lang.Exception;
var BufferedReader = java.io.BufferedReader;
  var InputStreamReader = java.io.InputStreamReader;
  var HttpResponse = org.apache.http.HttpResponse;
  var HttpClient = org.apache.http.client.HttpClient;
  var HttpGet = org.apache.http.client.methods.HttpGet;
  var StringBuffer = java.lang.StringBuffer;
  var String = java.lang.String;
  var userAgent = org.apache.http.HttpHeaders.USER_AGENT;
  var HttpClientBuilder = org.apache.http.impl.client.HttpClientBuilder;
var System = java.lang.System;
  try{  
     var httpTitle = "";
  if(System.getProperty("page_sub_title") == null){
     var client = HttpClientBuilder.create().build();
 var url = new String("http://www.google.com/search?q=httpClient");
 var request = new HttpGet(url);
 request.addHeader("User-Agent", userAgent);
   var response = client.execute(request);
 var rd = new BufferedReader(new InputStreamReader(response.getEntity().getContent()));
 var result = new StringBuffer();
 var line = "";
 while ((line = rd.readLine()) !== null) {
   result.append(line);
 } 
var Jsoup = org.jsoup.Jsoup;
 var httpDoc = Jsoup.parse(result);
 var httpTitle = httpDoc.select("title").first();
 System.setProperty("page_sub_title", httpTitle);
 } else {
   httpTitle = System.getProperty("page_sub_title");
 }

 doc.addField("sub_title", httpTitle);

  }catch(e){
    logger.error(e.getLocalizedMessage());
  }
  return  doc;
}
```

</details>
<br>
<details>

<summary>Click to expand the Authenticated Call full script body</summary> 

```Javascript
function(doc){

var pwd = "Lucidworks1";
 var user = "admin";
 var fusionUrl = "http://localhost:8764";
 var client = null;

var UsernamePasswordCredentials = org.apache.http.auth.UsernamePasswordCredentials;
  var AuthScope = org.apache.http.auth.AuthScope;
  var BasicCredentialsProvider = org.apache.http.impl.client.BasicCredentialsProvider;
  var HttpClientBuilder = org.apache.http.impl.client.HttpClientBuilder;
  var HttpPost = org.apache.http.client.methods.HttpPost;
  var StringEntity = org.apache.http.entity.StringEntity;


var e = java.lang.Exception;
  try {

var authJson = "{\"username\":\"" + user + "\", \"password\":\"" + pwd + "\"}";
    var authUrl = fusionUrl + "/api/session?realmName=native";
    var provider = new BasicCredentialsProvider();
    var credentials = new UsernamePasswordCredentials(user, pwd);
    provider.setCredentials(AuthScope.ANY, credentials);
    var client = HttpClientBuilder.create()
       .setDefaultCredentialsProvider(provider)
       .build();

 var session = new HttpPost(authUrl);
    var params = new StringEntity(authJson);
    session.addHeader("content-type", "application/json");
    session.setEntity(params);   
    var response = client.execute(session);

  } catch (e) {
    logger.error("Error getting httpclient " + e.getLocalizedMessage());
  }
  return  doc;
}
```

</details>
<br>
Make sure to save your open windows before ending your lab.

_________

## Congratulations! You have successfully modified and authenticated a document via REST Call. If you would like to save your Fusion App to reference later, you can do it now:

1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**


<link rel="stylesheet" href="lib/public/global-training.css">

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

When the Fusion Login page displays, login:
    * USERNAME: ```admin```
    * PASSWORD: ```password123```

# In this lab  you will learn how to use aggregated signals, how to apply and analyze signal boosting. Let's get started!

> Note: You may need to adjust the size of the instructions panel to fully view results in the UI. Toggle the window sizes as needed.

#  Inspect Aggregated Signals

1. In the Fusion Admin UI, click **Electronics** to access the app

2. Navigate to **Collections Manager**

3. Change collection: **Electronics_signals_aggr**

4. In the App tool menu, gover over QUERYING and click **Query Workbench**

> Notice that no result turn up and you see an API Error. That is because the Apply Rules stage is interfering with the data.

5. Click on the green circle to turn the <u>Apply Rules</u> stage **off**

  <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Boosting%20With%20Signals_5/Boosting_with_Signals1.png" style="height: 355px; width:450px;"/>

<br>

>You will see the error still, but we now have results. This will work for the purposes of this lab. In production, you would want to set up a custom pipeline before ingestion.

6. Click Show Fields on any document

   * The fields <u>doc_id_s</u> and query_s record the original query entered by the user(s), along with which document they ultimately clicked (query_s shows when given specific query)

    * <u>aggr_count_i</u> records how many times this specific query (“fax machine”) led to a click on this document (1)

    * <u>weight_d</u> indicates how much to promote this document in response to this query

7.  Execute a query for: ``doc_id_s: 2842056``

8. Click: **Add a field facet** 

9. Choose: **query_s**

   * This query and facet show all of the user queries that led to a click on this document

   * We would need to examine individual documents to see the click-count and weight for each case.


<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Boosting%20With%20Signals_5/Boosting_with_Signals2.png" style="height: 225px; width:440px;"/>

<br>

10. Navigate to **Collections Manager**

11. Change collection: **Electronics**

> **Note:** You may leave without saving 

12. In the App tool menu, select: **QUERYING > Query Workbench**

# Applying Signal Boosting

13. Execute query for:  ``ipad``

    * Review the results


<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Boosting%20With%20Signals_5/Boosting_with_Signals3.png" style="height: 275px; width:450px;"/>

<br>

14. Click on the circle to turn the <u>Boost with Signals</u> stage **off**

    * Review the results. These results are terrible. There may not even be any ipads in the results

# Analyzing Signal Boosting

15. In Query Workbench, change View As: to **Debug**

16. Observe the **explain** section

This section provides a full description of how the relevancy score for each results document was calculated.  At present, with signal boosting disabled, this is based solely on TF*IDF

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Boosting%20With%20Signals_5/Boosting_with_Signals5.png" style="height: 349px; width:625px;"/>

<br>

17. **Re-enable** Boost with Signals stage (click to add green circle)

18. Observe debug output

    * First, notice that parsedquery became MUCH more complex due to the added boosting.

    * The doc ids you see in the boosted query were generated by first executing the same user query (“ipad”) on the Labs_signals_aggr collection, and collecting the top-weighted results

    * Second, notice that the relevance explain became more complex as well.  Now there is a Signal Boosting factor in addition to the TF*IDF factors.

    * In the example below, the final score for this document (20.69) was produced by similarly-scaled factors for TF*IDF (6.77) and Signals (3.05).  One did not overpower the other—a very good thing!

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Boosting%20With%20Signals_5/Boosting_with_Signals4.png" style="height: 184px; width:512px;"/>

<br>


19. Click to open **Boost with Signals** pipeline stage

20. Scroll down until you see **Solr Query Parameters**

The Solr Query Parameters govern how Fusion should locate and prioritize the signals related to a given query, as well as how the Signals-score should be combined with the standard TF*IDF score

When implementing Signal Boosting in a Fusion App, all of these parameters can and should be tuned to suit your specific use cases.

  <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Boosting%20With%20Signals_5/Boosting_with_Signals6.png" style="height: 480px; width:380px;"/>
  
 <br>

_____

## Congratulations! You should now know to use aggregated signals, and how to apply and analyze signal boosting. If you would like to save your Fusion App to reference later, you can do it now:

1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**


<link rel="stylesheet" href="lib/public/global-training.css">

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

When the Fusion Login page displays, login:
    * USERNAME: ```admin```
    * PASSWORD: ```password123```

# In this lab  you will learn how to connect to Jupyter, and explore data in Jupyter. Let's get started!

> Note: You may need to adjust the size of the instructions panel to fully view results in the UI. Toggle the window sizes as needed.

#  Connecting to Jupyter

1. Click **Jupyter** at the top of the screen. Note that a new tab will open with Fusion Jupyter.

This is what you will see after logging in:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Fusion%20SQL%206/SQL_1.png" style="height: 150px; width:600px;"/>

<br>

We will create a new jupyter notebook

2. Click the **New** button in the upper right

3. Select **Python 3** for the notebook type

4. Click **Untitled** (or the name of the notebook) to rename the notebook

5. In the Rename Notebook window, name your notebook: **Fusion_SQL** followed by your first name and last initial

    * Example: Fusion_SQL_John_B
    
A new notebook will now become available

6. For Input, enter: ``%load_ext fusionsql``. Then press Shift + Return on your keyboard

This loads the Fusion SQL interpreter into your notebook

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Fusion%20SQL%206/SQL_2.png" style="height: 250px; width:300px;"/>

<br>

7. Input the following into the notebook. After entering each line, press Enter or Return: 	

    a. ```username="admin"```

    b. ```hostandport="proxy:6764"```

8. Hit Shift + Return

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Fusion%20SQL%206/SQL_3.png" style="height: 250px; width:300px;"/>

<br>

This tells the notebook what host and port to listen to along with the username for login.

9. Input the following into the notebook:

    a. ```import getpass```

    b. ```password=getpass.getpass()```

10. Hit Shift + Enter

This will give you a dialog box to enter your password into.

11. Input the SQL password: ``password123`` and click **Enter**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Fusion%20SQL%206/SQL_4.png" style="height: 300px; width:350px;"/>

<br>

With all our credentials in place, we are now ready to connect to Fusion.

12. Input: ``%fusionsql connect``, then press shift + enter

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Fusion%20SQL%206/SQL_56.png" style="height: 350px; width:450px;"/>

<br>

Note the successful connection message below the line.

# Exploring citibikes Data with Fusion SQL

Now that we are successfully connected to our Fusion instances, we can use Fusion SQL to explore our data

13. Input: ``%fusionsql show tables``

14. Hit: Shift + Enter

This will show all the various tableNames in your Fusion VM

> Note that your table will look different than the image

> Note also that now we are given a response time for our query

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Fusion%20SQL%206/SQL_6.png" style="height: 350px; width:400px;"/>

<br>

15. Input: ```%fusionsql describe citibikes```, then press shift + enter

This command gives a description of the citibikes collection in the form of the associated fields.

> Note that we again are given a response time for our query. In fact, we will be given a query response time for each one we execute.

16. Input: ```%fusionsql select * from citibikes limit 20```, then press shift + enter

We can now see a detailed chart of not only the fields but their values as well

   * Select * indicates we want all field values to appear in our query.

   * From citibikes instructs that we want this data from the citibikes collection.

   * Limit 20 allows us to see the returned values of all fields while only seeing the first 20 documents

17. Input: ```%fusionsql select end_station_name_s, count(*) as cnt from citibikes group by end_station_name_s```, then press shift + enter

With this query we are asking for a total count (*) of all ending stations and we want each end station to have this count grouped together

Had we not indicated that we wanted them grouped together, our query would have returned each end station in the collection singley

18. Input: ```%fusionsql select start_time_dt, trip_duration_s, count(*) as cnt from citibikes group by start_time_dt, trip_duration_s limit 100```, then press shift + enter

    * With this query we are asking for a joining of how long a trip took with when that trip started

    * Here we place a limit of 100 due to the sheer volume of our query

________

If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**

_________

## Great job! If you would like to save your Fusion App to reference later, you can do it now:

1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**

