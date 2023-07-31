---
layout: page
title: Advanced Signals
permalink: /afsig/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

## It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Fusion Signals Lab! <br> Through this set of lab activities you will learn how to use aggregated signals, how to apply and analyze signal boosting. 

---
<br>

For this lab, we will be using the **Electronics** app that has already been created in Fusion.

1. On the Fusion launch page, click the **Electronics** app to open it and enter the Fusion workspace.

<br>

##  Inspect Aggregated Signals

Before we get started configuring the app for the lab exercises, let's take a minute to investigate the aggregated signals that are available for our data.

2. In the left navigation pane, click **Collections**, then select **Collections Manager** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collections.png" style="height: 300px; width:185px;"/>

<br>

3. Click to expand and view the **Your Collections** list and select **Electronics_signals_aggr** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afsig/afsig_collectionslist.png"/>

<br>

Notice the collection in the the top corner has been changed and now indicates that we will be looking at results related to the **Electronics_signals_aggro** collection.

4. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list.

<br>

You will notice that, instead of seeing results returned in the Query Workbench window, we can see an API error displayed. This is due to the fact that the Apply Rules stage is interfering with the search results.

5. Click the green circle next to the Apply Rules stage to disable it.

<br>

In the bottom right corner, you will see that we are still getting the API error warning, but we now have results displayed. 

><b>Note:</b> This will work for the purposes of this lab. In a production environment, you would want to avoid this error by setting up a custom pipeline before ingesting your data.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afsig/afsig_applyrules.png"/>

<br>

6. In the Query Workbench window, click **Show Fields** to display the field details for the first document. 

<br>

Let’s look at a couple of things:
* The **doc_id_s** and **query_s** fields record the original query entered by a user, along with which document they ultimately clicked (**query_s** will display a value when it given a specific query).
* The **aggr_count_i** field records how many times a specific query led to a click on this document.
* The **weight_d** field indicates how much to promote this document in response to a specific query.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afsig/afsig_fields.png"/>

<br>

To better understand how these fields will be returned, let's execute a query and add a field facet to isolate the results.

7. In the search field, execute a query for ```doc_id_s: 2842056```.

8. In the Query Workbench window, click **Add a field facet**. 

9. Begin typing ```query```, then select **query_s** in the autosuggestion list.

10. Click **Show Fields** to display the field details for the first document. 

<br>

Notice that now our fields display with results based on the query we ran, and show values for all of the user queries that led to a click on this document. Feel free to examine the other returned documents to see the click-count and weight for each case.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afsig/afsig_fieldsafterquery.png"/>

<br>

11. Click **Save** to save your changes to the Query Workbench, then click **Yes, save over the existing pipeline** to confirm the action.

<br>

## Applying signal boosting

For our next exercise, we are going to practice using signal boosting on our results.

12. Navigate to the **Collections Manager** tab, click to expand and view the **Your Collections** list and select **Electronics** from the list.

13. Navigate back to the **Query Workbench** tab.

14. Enter a query for ```ipad```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afsig/afsig_ipadsearch.png"/>

<br>

Before moving forward, take a minute to review the search results, taking notice of the scores for each search result.

15. Click the green circle next to the **Boost with Signals** stage to disable it.

<br>

Take another minute to review the updated results. While the number of returned results did not change, the relevance is terrible (we don't even have an ipad returned at the top of the results). 

Let's investigate a bit further.

16. In the lower right corner, locate the **View As** field. Click the dropdown arrow, then select **Debug** in the list. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afsig/afsig_debug.png"/>

<br>

The **explain** section provides a full description of how the relevancy score for each document in the results set was calculated.  At present, with signal boosting disabled, this is based solely on **TF*IDF**.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afsig/afsig_debugresults.png"/>

<br>

17. Click the circle next to the **Boost with Signals** stage to re-enable it.

<br>

Once more, let's observe the debugged results:
* Notice that **parsedquery** became MUCH more complex due to the added boosting.
* In addition, the relevance **explain** section has became more complex as well, as we are now employing a Signal Boosting factor in addition to the TF*IDF factors.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afsig/afsig_debugresults2.png"/>

<br>

If we switch back to viewing the results (**View As > Results**), we will see that the document ids displayed in the boosted query were generated by first executing the same user query (```ipad```) on the **Labs_signals_aggr** collection, and collecting the top-weighted results.

<br>

## Reviewing Parameters

Finally, let's take a moment to explore the details of the **Boost with Signals** stage.

19. Click **Boost with Signals** to open the pipeline stage's configuration window.

20. Scroll down until you locate the **Solr Query Parameters** section.

<br>

The **Solr Query Parameters** govern how Fusion should locate and prioritize the signals related to a given query, as well as how the signals-score should be combined with the standard TF*IDF score when calculating the relevance of the search result as compared to the query.

>Keep in mind, all of these parameters can (and should be) tuned to suit your specific use cases when implementing Signal Boosting in a Fusion app.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afsig/afsig_queryparams.png"/>
  
---
<br>

## Great job! You have successfully completed the Fusion Signals Lab, where you have learned how to use aggregated signals, and how to apply and analyze signal boosting. 

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