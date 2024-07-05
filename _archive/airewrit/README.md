---
layout: page
title: Query Analytics
permalink: /airewrit/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

## The environment should begin to load immediately. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

When the Fusion Login page displays, login:
* USERNAME: ```admin```
* PASSWORD: ```password123```

## In this lab you will ingest data so that you can enhance relevancy using query rewriting! Let's get started by importing the relevancy app

# Configuring the Relevancy App

1. Click on the app **relevancy-app** to enter the *Fusion workspace*, this is where you can ingest the data

2. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**

3. Select and run each of the following jobs in the order listed below:
    * ``relevancy``
    * ``relevancy_signals``
    * ``relevancy_click_signals_aggregation``

>Note: Success! The jobs will take about up to three minutes each, when it's done, the "running" icon will change to a "sunshine". If the job fails initially, rerun the job again.

4. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**. Check the first few results to ensure the job was run successfully

# Relevancy Enhancement Tactics

5. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**. Click on and run ``relevancy_head_tail``

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%203%20Head-tail.png" style="height: 300px; width:500px;"/>

>Note: Success! The job will take about a few minutes, when it's done, the "running" icon will change to a "sunshine". 

6. Hover over the **RELEVANCE** icon in the sidebar, then click **Rules**. A new tab will open in your browser. Keep this tab open as we will revisit it through the training session.

7. Click the **Rewrite** icon in the sidebar to access the Underperforming Query Rewriting dashboard

8. Click **Head/Tail** and find **dsl router** in the list of rewrites

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Head-tail%20rewrites%20nav.png" style="height: 300px; width:500px;"/>

9. Notice that Status is set to auto and that Published is set to yes. This is because the Head/Tail suggestion falls into the auto publish category set by the head-tail relevancy job we noted earlier in training. 
    * Click on **Auto** and select **Approved** to change the status to approved. 
    * The change in status will unpublish the rewrite. To publish, hover over the rule and click the **green up arrow** in the Published column. Confirm you want to publish by clicking **Publish** in the Publish Rules box that appears. 

10. Return to the Fusion tab. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**

11. Toggle off the **Text Tagger** stage in the query pipeline by clicking on the green circle. Update the **View As** option to **Debug**. This is located in the bottom right side of the query workbench

12. Execute a search for **dsl router**

>Note: Notice what Fusion is using to perform this search in the rawquerystring and querystring sections

13. Toggle on the **Text Tagger** stage by clicking on the grey circle. If the view does not automatically update, requery dsl router to see the change

>Note: Notice the search enhancement when we use Query Rewrite principles by turning on the Text Tagger stage. This shows the search enhancement when we use Query Rewrite principles through the Text Tagger stage. Notice the updated search parameters Fusion is using to perform this search in the rawquerystring and querystring sections

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%203%20Query%20Workbench%20Head-tail.png" style="height: 200px; width:400px;"/>

14. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**. Click on and run ``relevancy-spell-correction``

>Note: Success! The job will take about a few minutes, when it's done, the "running" icon will change to a "sunshine". 

15. Return to the **Query Rewriting** browser tab 

16. Click **Misspelling** and find any entry in the list of rewrites

17. Change the **Status** to **Approved** and the **Published** to **Yes**. Remember which one you published becuase you'll need it in the next steps.

18. Return to the Fusion tab. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**

19. Change **View As** to **Results** 

20. Toggle off the **Text Tagger** stage by clicking on the green circle and execute a search for the misspelling rule you approved and published on the Query Rewrites page

21. Toggle back on the **Text Tagger** stage by clicking on the grey circle and observe the difference in the relevancy of results

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%203%20Misspelling.png" style="height: 200px; width:300px;"/>

>Note: Notice the search enhancement when we use Query Rewrite principles by turning on the Text Tagger stage. This shows the search enhancement when we use Query Rewrite principles through the Text Tagger stage. Notice the updated search parameters Fusion is using to perform this search in the rawquerystring and querystring sections

22. Hover over the **COLLECTIONS** icon in the sidebar, then click **Jobs**. Click on and run ``relevancy-phrase-extraction``

23. Return to the **Query Rewriting** browser tab 

24. Click **Phrase** and find any entry in the list of rewrites

25. Change the **Status** to **Approved** and the **Published** to **Yes**. Remember which one you published because you'll need it in the next steps.

26. Return to the Fusion tab. Hover over the **QUERYING** icon in the sidebar, then click **Query Workbench**

27. Toggle off the **Text Tagger** stage by clicking on the green circle and execute a search for the entry you approved and published on the Query Rewrites page

28. Toggle back on the **Text Tagger** stage by click on the grey circle and observe the difference in the relevancy of results

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/03%20AI/Lab%203%20Phrase%20Example.png" style="height: 200px; width:300px;"/>

>Note: Notice the search enhancement when we use Query Rewrite principles by turning on the Text Tagger stage. This shows the search enhancement when we use Query Rewrite principles through the Text Tagger stage. Notice the updated search parameters Fusion is using to perform this search in the rawquerystring and querystring sections

29. Make sure to **Save** your open Fusion Workspace tabs!

________
Great job! You now have functioning query rewrites! If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**

This concludes the Query Rewrites Relevancy Lab.
