---
layout: page
title: Advanced Query Tools
permalink: /afadvqu/
---

<link rel="stylesheet" href="./lib/public/global-training.css">

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
