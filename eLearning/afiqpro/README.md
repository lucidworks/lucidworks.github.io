---
layout: page
title: Index and Query Profiles
permalink: /afiqpro/
---

<link rel="stylesheet" href="./lib/public/global-training.css">

## It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Index & Query Profiles Lab! <br> Through this set of lab activities, you will learn how to use index profiles to manage collections and pipelines, as well as how to utilize query profiles to enhance your end user search results. 

---
<br>

Let's get started by creating a new app in Fusion.

1. From the Fusion launch page, click **Create new app**.

2. In the **App Name** field, enter the name ```Profiles_Test```.

3. *(Optional)* Enter an **App Description** and select an **App tile color**.

4. Click **Create App**.  

5. Once it has been created, click the **Profiles_Test** app to open it and enter the Fusion workspace. 

<br>

## Exploring Index Profiles

For the first exercise, we will exploring how to use an index profile to duplicate an existing collection into a new collection that has an altered pipeline. 

For example, let's say we want to set up 2 different collections; one for PROD, and one for DEV. We want our DEV collection to be a smaller set of data, so we will use a index profile to "duplicate" our PROD collection, thereby creating a new DEV collection that will have its own pipeline.

To illustrate this example, we will be completing the following steps:
* Creating a second collection
* Updating the index pipelines for each collection
* Indexing data for the first collection
* Adjusting the index profile, then indexing data for the second collection

<br>

### Creating Collections

As a reminder, Fusion automatically creates a collection, along with its default pipelines and default profiles, when the app is created. Right now we have a ```Profiles_Test``` collection in our app, which will be our "PROD" collection.

Our first step is to create our second collection, which will be our "DEV" collection.

6. In the left navigation pane, click **Collections**, then select **Collections Manager** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collections.png" style="height: 350px; width:200px;"/>

<br>

7. In the Collection Manager pane, click **New**, then enter the following values:
* In the **Collection Name** field, enter ```Profiles_Test_2```.
* Click to enable the **Advanced** fields.
* Deselect the **Enable Signals** field (this prevents axillary signals collections from being created).

8. Scroll down and click **Save Collection** to create the new collection.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_profilestest2collection.png">
  
<br>

In the Collection Manager window, you should now see your primary collection (```Profiles_Test```) and the newly created second collection (```Profiles_Test_2```). 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_profilestest2.png">

<br>

### Define Index Pipelines

As you can see in the Collections Manager, both of our collections are empty. 

This is intentional. Before we populate them with data, we want to make some pipeline adjustments. We are going to start by setting up identical pipelines for both collections, then adding an additional stage that will make changes when populating the second collection.

Let's start with updating the ```Profiles_Test``` index pipeline by adding an additional pipeline stage for our data to pass through.

9. In the left navigation pane, click **Indexing**, then select **Index Pipelines** from the list. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_indexing.png" style="height: 300px; width:200px;">

<br>

10. In the Existing Pipelines pane, click **Profiles_Test** to open the configuration window.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_indexprofile_profilestest.png" style="height: 330px; width:200px;">

<br>

11. Click **Add a new pipeline stage** and begin entering ```regex```, then select **Regex Field Extraction** from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_regex.png"/>
  
<br>

12. In the **Label** field, enter ```Extract Year```.

13. In the Regex Rules section, click the green plus to add a new row.

14. In the **Source Fields** field, click **[…]** to open the configuration dialog. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_regexrules.png"/>
  
<br>

15. In the Source Fields dialog, click the green plus, then enter ```initial_release_date_dt``` for the new source field.
  
16. Click **Apply** to add the new field value and close the source field configuration dialog.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_regexsourcefield.png">

<br>

17. Enter the following values for the remaining fields in the row:
* In the **Target Field**, enter ```Year```.
* Click the **Write Mode** field and select ```overwrite```.
* In the **Regex Pattern** field, enter ```^([0-9]{4})```.
* Click the **Return If No Match** field and select ```value```.
* In the **No Match Literal Value** field, enter ```ERROR-PARSING-YEAR```.
* In the **Regex Capture Group** field, enter ```1```.

> <b>Note:</b> You can copy and paste the fields from here as necessary. Also note, you may need to use the scroll bar to be able to fill in the entire row.

<br>

18. Click **Save** to save the new ```Extract Year``` pipeline stage.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_regexsetup.png">

<br>

In a production environment, the specific order of your pipeline stages may be critical, therefore the execution order of the stages can be rearranged. For this exercise, we want our new ```Extract Year``` pipeline stage to be executed *before* the Solr Indexer stage. 

19. Click the stage's hamburger icon, then drag and drop the Extract Year stage to directly *above* the Solr Indexer stage. 

20. Click **Save** to save the changes to the pipeline stages.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_profilesstageupdate.png"/>

<br>

The next step in our exercise is to update our ```Profiles_Test_2``` collection. Fusion does NOT automatically create pipelines or profiles for manually created collections, so we will be adding a new index pipeline and then creating the matching Regex Field Extraction stage.

21. In the top left corner, click the Collections dropdown, then select the **Profiles_Test_2** collection.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_collectionchange.png" style="height: 300px; width: 200px"/>

<br>

22. In the left navigation pane, click **Indexing**, then select **Index Pipelines** from the list. 

23. In the Index Pipelines pane, select **Add+** to add a new pipeline.

24. In the **Pipeline ID** field, enter ```Profiles_Test_2```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqprof_profilestest2pipeline.png"/>

<br>

25. Click **Add a new pipeline stage** and begin entering ```regex```, then select **Regex Field Extraction** from the autosuggestion list.

26. In the **Label** field, enter ```Extract Year```.

><b>Note:</b> The label must be unique to its pipeline, not to the system overall. Since we are building a unique version in each pipeline, we want to use the same label for this stage in both, which will make it easier for us to keep it organized when we apply them and compare the results. 

<br>

27. In the Regex Rules section, click the green plus to add a new row, then enter the following values:
* In the **Source Field**, enter ```initial_release_date_dt```.
* In the **Target_Field**, enter ```Year```.
* Click the **Write Mode** field and select ```overwrite```.
* In the **Regex Pattern** field, enter ```^([0-9]{4})```.
* Click the **Return If No Match** field and select ```value```.
* In the **No Match Literal Value** field, enter ```ERROR-PARSING-YEAR```.
* In the **Regex Capture Group** field, enter ```1```.

28. Click **Save** to create the new ```Profiles_Test_2``` pipeline and its corresponding ```Extract Year``` pipeline stage.

29. Click the stage's hamburger icon, then drag and drop the **Extract Year** stage to directly *above* the Solr Indexer stage. 

30. Click **Save** to save the changes to the pipeline stages.

<br>

For this exercise, we are planning to compare the collection's search results created by our pipelines (via our index profile). Following our example use case, we intentionally want to make the ```Profiles_Test_2``` collection slightly different than ```Profiles_Test``` collection. We are going to do this by ingesting a subset of the data, which means adding another pipeline stage to be executed when ingesting the data for the ```Profiles_Test_2``` collection.

31. Click **Add a new pipeline stage** and begin entering ```include```, then select **Include Documents** from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_includedocs.png"/>

<br>

32. In the **Label** field, enter ```Only include genre: Drama```.

33. In the Fields and Patterns section, click the green plus to add a new row, then enter the following values:
* In the **Field** field, enter ```genre_txt```.
* In the **Regex Pattern** field, enter ```Drama```.

34. Click **Save** to create the new ```Only include genre: Drama``` pipeline stage.

35. Use the stage's hamburger icon to move the **Only include genre: Drama** stage to be executed *between* the Extract Year and Solr Indexer stages.

36. Click **Save** to save your changes to the pipeline stages.

<br>

### Indexing the Primary Collection

Now that our index pipeline setup is complete, it's time to add some data to our collections. Let's start by ingesting some data for our **Profiles_Test** collection. 

37. In the top left corner, click the Collections dropdown, then select the **Profiles_Test** collection.

38. In the left navigation pane, click **Indexing**, then select **Datasources** from the list. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_indexing.png" style="height:300px; width:200px;"/>

<br>
   
39. Click **Add+**, then select **File Upload** from the list. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffindex/ffindex_fileupload.png" style="height: 320px; width:360px;"/>

<br>

40. Enter the following datasource values:
* In **Datasource ID** field, enter ```profiles_test```.
* In **File ID** field, enter ```profiles_test.json```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_profilestestdatasource.png"/>

<br>

41. Click **Save** to create the datasource.

<br>

Next we need to run a job in order to ingest the data into Fusion.

42. Click **Run**, then click **Start** in the job dialog to start the job.

>The job may take a couple minutes to run. Note that the **Running** indicator displays while the job is in process, and will change to **Success** when the job is complete.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_profilestestingest.png"/>

<br>

43. Once the job is complete, click the **X** to close the dialog.

<br>

Now that we have ingested data into our primary collection, let's navigate to the **Query Workbench** where we can review our results.

44. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list.

 <img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_querying.png" style="height: 300px; width:200px;"/>

<br>

45. Click **Display Fields** to open the dropdown, then change the following values:
* In the **NAME** field, enter ```name_s```.
* In the **DESCRIPTION** field, enter ```genre_txt```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_profiletest_querydisplayfields.png"/>

<br>

46. Click **Display Fields** again to close the dropdown. 

47. Click **Add a field facet** and begin typing ```genre```, then select ```genre_txt``` from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_profiletestfacet.png"/>

<br>

Let's look a little closer at the fields for one of the documents. 

48. Click **Show Fields** for the first document returned.

<br>

When reviewing the results, remember that we ingested this data using the ```Profiles_Test``` index pipeline, which only included the ```Extract Year``` pipeline stage. In the expanded results, we can see the **Year** field returned with a corresponding value, while the facet shows us all the different genres found in the dataset. Also notice at the bottom of the display, there are 1,100 documents returned for this collection.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_profilestestresults.png" style="height: 325px; width:580px;"/>

<br>

49. Click **Save** to save your Query Workbench changes before continuing on in the lab.

<br>

### Adjusting the Index Pipeline

Now let's compare these results to those from our ```Profiles_Test_2``` collection. To do this, we will start by pointing our index profile to the new collection, then we will ingest collection data and compare the search results. 

50. In the top left corner, click the Collections dropdown, then select the **Profiles_Test_2** collection.

51. In the left navigation pane, click **Indexing**, then select **Index Profiles** from the list. 

52. In the Index Profiles pane, click **Profiles_Test** to open the configuration window.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_indexprofilenavigation.png"/>

<br>

53. Change the profile configuration to point to the **Profiles_Test_2** collection by changing the following values:
* In the **Index Pipeline** field, enter ```Profiles_Test_2```.
* In the **Collection** field, enter ```Profiles_Test_2```.

>These changes tell Fusion to use the ```Profiles_Test_2``` index pipeline (which, if you recall, is the pipeline that has both the **Extract Year** and **Only include genre: Drama** stages) and to add the ingested data to the ```Profiles_Test_2``` collection.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_profilechanges.png"/>

<br>

54. Click **Save** to save your changes to the profile.

<br>

Now let's add our **Profiles_Test_2** datasource.

55. In the left navigation pane, click **Indexing**, then select **Datasources** from the list. 
   
56. Click **Add+**, then select **File Upload** from the list. 

57. Enter the following datasource values:
* In the **Datasource ID** field, enter ```profiles_test_2```.
* In the **Pipeline ID** field, select ```Profiles_Test_2```.
* In the **File ID** field, enter ```profiles_test.json```.

>Notice that the pipeline now points to **Profiles_Test_2**, which is what we want it to do.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_profilestest_2datasource.png"/>

<br>

58. Click **Save** to create the datasource.

<br>

Once again, we need to run a job in order to ingest the data into Fusion.

59. Click **Run**, then click **Start** in the job dialog to start the job.

60. Once the job is complete, click the **X** to close the dialog.

<br>

Now that we have indexed both collections, we can view the **Query Workbench** and compare our results for this collection.

Notice that **Profiles_Test_2** collection contains fewer documents (just over 500 documents), due to the addition of the **Only include genre: Drama** pipeline stage. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_profiletest2_testresults.png"/>

<br>

61. Click **Save** to save your Query Workbench changes before continuing on in the lab.

<br>

## Using Query Profiles

Query profiles are used in a similar fashion as index profiles - they allow us to curate a set of the returned search results based on the profile applied. 

For our last exercise in this lab, we are going to explore query profiles using our **Profiles_Test** collection. 

62. In the top left corner, click the Collections dropdown, then select the **Profiles_Test** collection.

63. In the left navigation pane, click **Querying**, then select **Query Profiles** from the list. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_querying.png" style="height: 300px; width: 200px;"/>

<br>

64. In the Query Profiles pane, click **Profiles_Test** to open the configuration window.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_queryprofile.png"/>

<br>

65. In the Query Params section, click **New params** to open the query params configuration window.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_queryparamsnav.png"/>

<br>

66. In the Query Params window, click the green plus to add a row, then enter the following values:
* In the **Parameter Name** field, enter ```q```.
* In the **Parameter Value** field, enter ```*:*```.
* Click the **Update Policy** field and select ```replace```.

67. Add a second parameter by clicking the green plus again, then entering the following values:
* In the **Parameter Name** field, enter ```facet.field```.
* In the **Parameter Value** field, enter ```Year```.
* Click the **Update Policy** field and select ```append```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afiqpro/afiqpro_queryparams.png"/>

<br>

68. Click **Apply** to add the new field values and close the query params configuration dialog.

69. Click **Save** to save your changes to the query profile.

<br>

For our last step, let's review the impact our query profile changes had on our search results.

70. Navigate to the Query Workbench tab. 

---
<br>

## Great job! You have successfully completed the Index and Query Profiles Lab, where you learned how to define index pipelines, index data, and utilize query profiles to refine your search results.

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