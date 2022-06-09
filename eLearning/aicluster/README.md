---
layout: page
title: Document Clustering
permalink: /aicluster/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol. Please do not click *Start Lab* again. It may take a few mintues for the Fusion environment to fully display.

When the Fusion Login page displays, login:
* USERNAME: ```admin```
* PASSWORD: ```password123```

## In this lab  you will set up clustering, evaluate results, and tune the clustering job! Let's get started by setting up clustering
 
1. Click on the app **Labs** to enter the *Fusion workspace*, this is where you can build and test document clustering

# Setting up Clustering

2. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**

3. Click **Add**, then select **Document Clustering**

4. Toggle on **Advanced**. Let's add some parameters:
    * Change the **Spark Job ID** to ``product_clustering``
    * Update the **Training Collection** to ``Labs``
    * Update the **Output Collection** to ``Labs``
    * Find **Training Data Sampling Fraction** and input ``0.2``
    * Update the **Field to Vectorize** to ``longDescription``

5. Click **Save**, then **Run**, then **Start**

  <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%204%20Clustering.png" style="height: 250px; width:400px;"/>

>Note: Success! The job will take about a minute, when it's done, the "running" icon will change to a "sunshine". 

# Evaluating Results

6. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**

7. Click **Add a field facet** and select **cluster_label**

8. Click **Add a field facet** and select **freq_terms**

9. Click **View next 10** under the **cluster_label** facet

>Note: The cluster_label field contains the five terms that best define the center of each cluster.  The freq_terms field contains the five terms that appear most often in each cluster.  You will note that, in many cases, the frequent terms in a cluster are also among those those that best define it. The clustering job also identified and labeled oddball documents: abnormally long ones, those too short to determine anything meaningful, and those that do not seem closely related to any of the big clusters.

# Tuning the Clustering Job

10. Hover over the **COLLECTIONS** icon in the sidebar, then click **Collections Manager**

11. Click **New**, and name your new collection **Labs2**.

12. Toggle on **Advanced** and uncheck **Enable Signals**. Click **Save Collection**

13. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**

14. Select the **product_clustering** job and toggle on **Advanced**

15. Modify the following parameters:
    * Change the **Output Collection** to ``Labs2``
    * Update the **Outlier Cutoff** to ``0.02``
    * Update the **Min Possible Number of Clusters** to ``5``
    * Update the **Max Possible Number of Clusters** to ``25``
    * Update the **Word2Vec Dimension** to ``100``
  
16. Click **Save**, then **Run**, then **Start**

>Note: Success! The job will take about a minute, when it's done, the "running" icon will change to a "sunshine". 

17. Click the **Collections** dropdown and select the output collection **Labs2**

18. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**

19. Click **Add a field facet** and select **cluster_label**

20. Click **Add a field facet** and select **freq_terms**

>Note: Explore your clusters. Do they look better than they did previously?

  <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%204Tuning%20Clustering.png" style="height: 250px; width:300px;"/>

21. Make sure to **Save** your open Fusion Workspace tabs!

________
Great job! You now have functioning document clustering in your Fusion instance! If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**

This concludes the Document Clustering Lab.
