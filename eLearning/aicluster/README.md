---
layout: page
title: Document Clustering
permalink: /aicluster/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

## It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Document Clustering Lab! <br> Through this set of lab activities, you will set up document clustering, evaluate results, and tune the clustering job.

---
<br>
 
For this lab, we will be using the **Labs** app created in the Intro to Machine Learning lab.

1. On the Fusion launch page, click the **Labs** app to open it and enter the Fusion workspace.

>Before proceeding with the lab, please navigate to the **Jobs** tab (**Collections > Jobs**). Make sure that both the **BestBuy_catalog** and **BestBuy_signals_labs** jobs have run. If you see a caution sign, please run the job again before continuing on in the lab.

<br>

## Setting up Clustering

2. In the left navigation pane, click **Collections**, then select **Jobs** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collections.png" style="height: 300px; width:200px;"/>

<br>

3. In the Jobs pane, click **Add** and begin typing ```document```, then select **Document Clustering** from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclust/aiclust_clustjobcreate.png"/>

<br>

4. In the job configuration window, enter the following values:
* In the **Spark Job ID** field, enter ```product_clustering```.
* Click the **Training Collection** field and select ```Labs```.
* Click the **Output Collection** field and select ```Labs```.
* In the **Field to Vectorize** field, enter ```longDescription```.

5. Click to enable the **Advanced** fields. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclust/aiclust_clustjobdetails1.png"/>

<br>

6. Scroll down to the Dataframe Config Options section, then enter the following value:
* In the **Training Data Sampling Fraction** field, enter ```0.2```.

7. Click **Save** to create the new job.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclust/aiclust_clustjobdetails2.png"/>

<br>

Now we need to run the job.

8. Click **Run**, then click **Start** in the job dialog to start the job.

>The job will take a couple minutes to run. Note that the **Running** indicator displays while the job is in process, and will change to **Success** when the job is complete.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclust/aiclust_clustrunjob.png"/>

9. Once the job is complete, click **X** to close the job dialog.

<br>

## Evaluating Results
Now that we have run the Document Clustering job, let's take a minute to review our results.

10. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list. 

11. Click **Add a field facet**, begin typing ```cluster```, then select **cluster_label** in the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclust/aiclust_fieldfacet.png"/>

<br>

12. Repeat step 10 to add a second field facet for **freq_terms**.

The **cluster_label** field contains the five terms that best define the center of each cluster.  The **freq_terms** field contains the five terms that appear most often in each cluster.  You will note that, in many cases, the frequent terms in a cluster are also among those those that best define it. 

<br>

13. Under the **cluster_label** facet, click **View next 10**.

In the next set of facet options, you can see that the clustering job also identified and labeled oddball documents: abnormally long ones, those too short to determine anything meaningful, and those that do not seem closely related to any of the big clusters.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclust/aiclust_labsfacets.png"/>

<br>

## Tuning Clustering Jobs

For our next activity, we are going to add some additional parameters to our clustering job and compare the results to our original set. For this, we will start by creating a new collection, then pointing the job to use it instead.

14. In the left navigation pane, click **Collections**, then select **Collections Manager** from the list.

15. In the Collection Manager pane, click **New**, then enter the following values: 
* In the **Collection Name** field, enter ```Labs2```.
* Click to enable the **Advanced** fields.
* Deselect the **Enable Signals** field (this prevents auxiliary signals collectsion from being created).

16. Scroll down and click **Save Collection** to create the new collection.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclust/aiclust_createlabs2job.png"/>

<br>

17. Navigate back to the **Jobs** tab.

18. Click the **product_clustering** job to open the job configuration window.

19. In the job configuration window, enter the following values:
* Click the **Output Collection** field and select ```Labs2```.

20. Click to enable the **Advanced** fields.

21. Click to expand the Model Tuning Parameters section, then enter the following values:
* In the **Outlier Cutoff** field, enter ```0.02```.
* In the **Max Possible Number of Clusters** field, enter ```25```.
* In the **Min Possible Number of Clusters** field, enter ```5```.
* In the **Word2Vec Dimension** field, enter ```100```.
  
22. Click **Save** to save your changes to the job.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclust/aiclust_jobchanges.png"/>

<br>

23. Click **Run**, then click **Start** in the job dialog to start the job.

Once again, the job will take a couple minutes to run. Once it is complete, let's go review our new results.

<br>

24. In the top left corner, click the Collections dropdown, then select the **Labs2** collection.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collectiondropdown.png"/>

<br>

25. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list.

24. Click **Add a field facet** and add field facets for **cluster_label** and **freq_terms**.

Take a moment to explore your clusters. Do they look better? 

Notice that, with the application of the new parameter settings, you see a difference in the number of cluster labels created (which translates to more accurate search results for the end user). 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aiclust/aiclust_jobcomparison.png"/>

---
<br>

## Great job! You have successfully completed the Document Clustering Lab, where you have learned how to utilize document clustering to enhance your search results.

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