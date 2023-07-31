---
layout: page
title: Advanced Query Tools
permalink: /afadvqu/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

## It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Advanced Query Tools Lab! <br> Through this set of lab activities, you will learn how to use the eDisMax Parser, facets, and function queries. 

---
<br>

For this lab, we will once again use our **Online Shoes** app. 

1. On the Fusion launch page, click the **Online_Shoes** app to open it and enter the Fusion workspace.

<br>

## Using the eDismax Parser

2. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list.

 <img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_querying.png" style="height: 300px; width:200px;"/>

<br>
   
3. Click **Display Fields** and change the following parameters:
* In the **NAME** field, enter ```name```.
* In the **DESCRIPTION** field, enter ```description```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_displayfields.png"/>

<br>

4. Click **Display Fields** again to close the dropdown. 

5. In the search field, enter a query for **canvas wedge sandal**. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_canvaswedgesandal.png" style="height: 150px; width:550px;"/>

<br>

Take a moment to review the search results, and note the number of documents that have been returned for this search.

<br>

6. Click the green circle next to the **Query Fields** stage to disable it.

><b>Note:</b> We are disabling this stage because we want to use some custom parameters. We will create a new stage while keeping this original **Query Fields** stage for later use.

<br>

7. Click **Add a Stage**, begin typing ```additional```, then select **Additional Query Parameters** from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_addstage.png"/>

<br>

8. In the **Label** field, enter ```myQueryParams```.

9. In the Parameters and Values section, click the green plus, then enter the following values:
* In the **Parameter Name** field, enter ```defType```.
* In the **Parameter Value** field, enter ```edismax```.
* Click the **Update Policy** field and select ```append```.

10. Add a second parameter by clicking the green plus again, then entering the following values:
* In the **Parameter Name** field, enter ```mm```.
* In the **Parameter Value** field, enter ```2```.
* Cliick the **Update Policy** field and select ```append```.

> <b>Note:</b> Parameter <b>mm</b> (minimum match) is an eDisMax parameter that specifies the minimum number of terms that need to match in a Disjunction (OR) query. For our **canvas wedge sandal** search, it means that 2 of the 3 terms in the search need to be found in the document in order to be included in the returned results.

<br>

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_myqueryparams.png" style="height: 300px; width:400px;"/>

<br>

11. Click **Apply** to create the new ```myQueryParams``` field, then click **Cancel** to collapse the configuration window and see a larger view of our results.

Notice that our results have changed with the addition of the new **myQueryParams** stage. The total number of documents returned is smaller, due to the inclusion of the **mm** parameter.  

Before moving on, try changing **mm** to 3 and look at the results again.

<br>

## Boosting with eDisMax

12. In the search field, execute a query for ```*:*``` (the default search, so we return all available results).

13. Click **myQueryParams** to reopen the stage configuration window. 

><b>Note:</b> For the step below, it may be helpful to copy the values and paste them directly into the fields in the lab environment.

14. In the Parameters and Values section, click the green plus to add another parameter and enter the following values:
* In the **Parameter Name** field, enter ```boost```.
* In the **Parameter Value** field, enter ```recip(ms(NOW,dateAdded_dt),3.16e-11,10,1)```.
* Click the **Update Policy** field and select ```append```.

><b>Note:</b> This is a common Reciprocal function applied to date fields to give more weight to recent dates. 

<br>

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afasvqu_addboostparam.png" style="height: 350px; width:350px;"/>

<br>

15. Click **Apply** to save your changes to the ```myQueryParams``` field, then click **Cancel** to collapse the configuration window and see a larger view of our results.

<br>

With the addition of the **boost** parameter, you can observe that more recent documents are now on top by looking at the **dateAdded_dt** field. The parameter multiplies the function by the BM25 of the search.

><b>Note:</b> The boosting factor is the number ```10``` in the formula above. Try changing this number and see how the score changes.

<br>

Before moving on to the next lab activity, we need to reset our stages. 

16. Click the green circle next to the **myQueryParams** stage to disable it. 

17. Click the circle next to the **Query Fields** stage to enable it.

18. Click **Save** to save your changes to the Query Workbench, then click **Yes, save over the existing pipeline** to confirm the action.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_stageupdates.png"/>

<br>

## Using facets
Within the Fusion UI, there are two methods for adding field facets. In this activity, we will be adding them directly to the Facets stage.

19. Click **Facets** to open the stage configuration window.

20. In the Facet Fields section, click the green plus to add a facet field. Begin typing ```sizes```, then select **sizes** in the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_sizesfacet.png"/>

<br>

21. Repeat step 20 and add the following facet fields:
* ```brand```
* ```colors```
* ```{!ex=dt}sizes```
* ```{!ex=dt}brand```

><b>Note:</b> The last two facet fields will not have a autosuggestion option to select. Using the ```'ex'``` parameter excludes everything but the sizes and brand fields from the other facets that reference that field.

<br>

22. Click **Apply** to save your changes to the **Facets** stage, then click **Cancel** to collapse the configuration window.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_facets.png" style="height: 300px; width:400px;"/>

<br>

With our field facets in place, we can get more specific with our result set. For instance, let's try looking for size 8 shoes by Nine West.

23. Click the following selections in the facets list:
* **sizes**: 8
* **brand**: Nine West and Easy Spirit
* **colors**: (none)

<br>

Before moving on, feel free to try other combinations and explore your results.

>Clear all field facets selections before continuing on in the lab.

<br>

## Using Function queries

Let’s try using a Function query to find the frequency of a term within a field.

24. In the search field, execute a query for ```termfreq(colors, 'Multicolor')```.

For these search results, notice the score is determined by the function, and the number of documents returned is based on function results.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_multicolor.png"/>

<br>

Let’s try using a field that uses TF-IDF to make our results more accurate.

25. In the search field, enter a query for ```tf(colors, 'Multicolor’)```.

<br>

These results are more accurate because in addition to term frequency, we are incorporating inverse document frequency.

26. Click **Save** to save your changes to the Query Workbench before continuing on in the lab.

<br>

## Additional Query Parsers

For this next section, we will need some data that contains latitude and longitude fields. Our shoes dataset doesn’t include this, so we will use separate dataset with a new app.

27. In the left navigation pane, click **Apps**, then select **Return to Launcher** from the list.
    
<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_apps.png" style="height:300px; width:200px;"/>

<br>

28. From the Fusion launch page, click **Create new app**.

29. In the **App Name** field, enter the name ```citibikes```.
    
30. *(Optional)* Enter an **App Description** and select an **App tile color**. 
    
31. Click **Create App**.  

32. Once it has been created, click the **citibikes** app to open it and enter the Fusion workspace. 

<br>

We will ingest this **citibikes** datasource ad-hoc without a schema pre-defined, ending up with a field with latitude/longitude data called **start_station_s**. Notice however, that this is a string field that is not suitable to use in latitude/longitude calculations. 

To use our data effectively, we will need to create a new location type field, **start_station_p**, then copy the information from the string field over to the location field (which will support our latitude/longitude calculation requirements).

Similarly, we will have a **birth_year_s** field which we need to calculate a range on. This will also be ingested as a string field, and once again we will need to create a new pint type field, **birth_year_pint**, then copy the information over to the new field (which will better support range calculations).

Let's start by creating the new fields.

33. In the left navigation pane, click **Collections**, then select **Fields** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collections.png" style="height: 330px; width:200px;"/>

<br>

34. In the Fields pane, click **Add a Field+**, then enter the following field parameters:
* In the **Field Name** field, enter ```start_station_p```.
* In the **Field Type** field, select ```location_rpt```.
* Select the **Indexed** option.
* Select the **Stored** option.
* Select the **Multivalued** option.

35. Click **Save** to create the ```start_station_p``` field. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_startstation.png" style="height: 350px; width:500px;"/>
    
<br>

><b>Note:</b> After we ingest our data, we will add the <b>Copy Fields To</b>, setting it up to copy the value of the <b>start_station_s</b> field into this new field.

36. In the Fields pane, click **Add a Field+**, then enter the following field parameters:
* In the **Field Name** field, enter ```birth_year_pint```.
* In the **Field Type** field, select ```pint```.
* Select the **Indexed** option.
* Select the **Stored** option.
* Deselect the **Multivalued** option.

37. Click **Save** to create the ```birth_year_pint``` field. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_birthyear.png" style="height: 350px; width:500px;"/>

<br>

><b>Note:</b> Again, after we ingest our data, we will add the <b>Copy Fields To</b> setting it up to copy the value of the <b>birth_year_s</b> field into this new field for more proper Date calculations.

<br>

Now that our new fields are set up, let's ingest our data.

38. In the left navigation pane, click **Indexing**, then choose **Datasources** from the list. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_indexing.png" style="height:300px; width:200px;"/>

<br>

39. Click **Add+**, then choose **File Upload** from the list. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffindex/ffindex_fileupload.png" style="height: 320px; width:360px;"/>

<br>

40. Enter the following datasource details:
* In **Datasource ID** field, enter ```citibikes```.
* Click in the **Parser** field and select ```citibikes```.
* In **File ID** field, enter ```citibikes.csv```.

41. Click **Save** to create the datasource.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_citibikedatasource.png">

<br>

>**Important**: DO NOT start the job yet. We still need to modify our index pipelines to set up the field copying process.

<br>

42. Click the link to the right of the citibikes **Pipeline ID** to use the shortcut into the Index Pipeline tab.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_citibikepipeline.png"/>

<br>

43. Click **citibikes**, then click **Field Mapping** to open the stage's configuration window.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_citibikesindexpipeline.png">

<br>

44. In the **Label** field, enter **Copy Location and Pint Fields**.

><b>Note:</b> Notice that the stage name has now changed to match the label.

<br>

45. In the **Field Translations** section, click the green plus to add a new field and enter the following values:
* In the **Source Field**, enter ```start_station_s```.
* In the **Target Field**, start typing ```start_station_p```, then select it from the autosuggestion list.
* Click in the **Operation** field and select ```Copy```. 

46. Add a second row by clicking the green plus again, then entering the following values:
* In the **Source Field**, enter ```birth_year_s```.
* In the **Target Field**, start typing ```birth_year_pint```, then select it from the autosuggestion list.
* Click in the **Operation** field and select ```Copy```. 

><b>Note:</b> The ```start_station_s``` and ```birth_year_s``` will not prompt via the autosuggestion list, as we have not ingested the data and created them yet.

<br>

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_copyfields.png"/>

<br>

47. Click **Save** to apply your changes to the stage.

<br>

We have one additional change to make: we need this stage to occur *after* the Solr Dynamic Field Mapping stage. 

48. Click the stage's hamburger icon, then drag and drop the stages into the order you want them to be applied.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_fieldsarrangement.png" style="height:250px; width:400px;"/>

<br>

We have completed the setup for our new fields, so it is time to ingest our data and test our results.

49. Navigate back to the **Datasources** tab.

50. Click **Run**, then click **Start** in the job dialog to start the **citibikes** ingesting job.

>The job will take about 5 minutes to run. Note that the **Running** indicator displays while the job is in process, and will change to **Success** when the job is complete.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_citibikeingest.png" style="height:260px; width:550px;"/>

<br>

51. Once the job is complete, click the **X** to close the dialog.

<br>

Let's use some query parameters to answer the following question: How many stations are 1 km from the start station that has coordinates of 40.70,-73.99?

52. In the left navigation pane, click **Querying**, then choose **Query Workbench** from the list.

 <img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_querying.png" style="height: 300px; width:200px;"/>

<br>

53. Click **Display Fields**, and change the following values:
* In the **NAME** field, enter ```start_station_p```.
* In the **DESCRIPTION** field, enter ```birth_year_pint```. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_newdisplayfields.png"/>

<br>

54. Click **Display Fields** again to close the dialog.

55. Click **Add a Stage**, begin typing ```additional```, then select **Additional Query Parameters** from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_newquerystage.png">

<br>

56. In the Parameters and Values section, click the green plus three times, then enter the following values:
* In the **Parameter Name** field, enter ```fq```.
* In the **Parameter Value** field, enter ```{!geofilt sfield=start_station_p}```.
* Click the **Update Policy** field and select ```append```.

<br>

* In the **Parameter Name** field, enter ```pt```.
* In the **Parameter Value** field, enter ```{40.70,-73.99}```.
* Click the **Update Policy** field and select ```append```.

<br>

* In the **Parameter Name** field, enter ```d```.
* In the **Parameter Value** field, enter ```1```.
* Click the **Update Policy** field and select ```append```.

<br>

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_queryparams.png">

<br>

57. Click **Apply** to create the new ```Additional Query Parameters``` stage, then click **Cancel** to collapse the configuration window and see a larger view of our results.

<br>

We can see that over 223k documents (each representing a station that is 1 km from the start station that has coordinates of 40.70,-73.99) have been returned. 

Let's use this same stage to answer another question: Find all stations that were built between 1980-1983.

58. Click **Additional Query Parameters** to reopen the stage's configuration window. 

59. Click **X** to delete the **d** and **pt** parameters.

60. For the **fq** parameter, change the **Parameter Value** field value to ```{!terms f=birth_year_s}1980,1981,1982,1983```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_birthyearlist.png"/>
    
<br>

61. Click **Apply** to apply the changes to the stage, then click **Cancel** to collapse the configuration window and see a larger view of our results.

<br>

We can see that over 32k documents (each representing a station that meets the requirement of being built between 1980-1983) have been returned.

Let's make one more update to our stage and use it to answer one additional question: Find all stations build between the years 1988 to 1990.

62. Click **Additional Query Parameters** to reopen the stage's configuration window. 

63. For the **fq** parameter, change the **Parameter Value** field value to ```{!frange l=1988 u=1990}birth_year_pint```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_range.png"/>

<br>

64. Click **Apply** to apply the changes to the stage, then click **Cancel** to collapse the configuration window and see a larger view of our results.

<br>

Before reviewing the results, let's change the display fields so they highlight the information we want to view.

65. Click **Display Fields**.

66. In the **Name** field, start typing ``start_station_name_s``, then select it from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afadvqu/afadvqu_rangedisplayfield.png"/>

<br>

67. Click **Display Fields** again to close the dropdown and view the updated results. 

The returned results give the state station name of each document that meets our requirements (stations built between 1988 and 1990.) Note that, similar to the second example, we could have listed out all the years individually, however this time we used a range function to find our results. 

---
<br>

## Great job! You have successfully completed the Advanced Query Tools lab, where you learned to use eDisMax Parser, facets, and function queries to refine the search results for your end-users. 

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
