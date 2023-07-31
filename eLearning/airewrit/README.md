---
layout: page
title: Query Analytics
permalink: /airewrit/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

## It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Query Analytics Lab! <br> Through this set of lab activities, you will practice using query rewriting to enhance the relevancy of search results.

---
<br>

For this lab, we will using the **relevancy-app** that has already been configured for our lab environment. 

1. On the Fusion launch page, click the **relevancy-app** to open it and enter the Fusion workspace.

<br>

## Configuring the App

Before we get started on our lab exercises, we need to run several jobs to prepare our app data.

2. In the left navigation pane, click **Collections**, then select **Jobs** from the list. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collections.png" style="height: 300px; width:185px;"/>

<br>

3. Click `relevancy` to open the job's configuration window. 

4. Click **Run**, then click **Start** in the dialog to start the job.

>A reminder for all the jobs we will run in this lab: the jobs should be run one at a time, and will each take a couple minutes to run. Note that the **Running** indicator displays while the job is in process, and will change to **Success** when the job is complete. If the initial attempt to run the job fails, go ahead and rerun it. 

5. Once the job is complete, click the **X** to close the dialog.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_relevancyjob.png"/>

<br>

6. Repeat steps 3-5 to run the following jobs in the order listed below:
* ```relevancy_signals```
* ```relevancy_click_signals_aggregation```

> Once all jobs have successfully run, you can navigate to the **Query Workbench** (**Querying > Query Workbench**), and check the first few results to ensure the jobs ran successfully.

<br>

## Head/Tail Analysis Rewrites

For our first lab exercise, we are going to examine head-tail queries and how we can add boosting factors to enhance our returned results. 

Let's start with running one more job, which will allow us to compare the head/tail results from some queries.

7. Navigate back to the **Jobs** tab, and repeat steps 3-5 to run the ```relevancy_head_tail``` job.

<br>

Once it has been successfully run, we want to view the results.

8. In the left navigation pane, click **Relevance**, then select **Rules** from the list. 

>Clicking **Rules** will open the **Rules Manager** in a new tab in your browser. <u>Keep this tab open</u>, as we will revisit it throughout the lab exercises.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_relevance.png" style="height: 300px; width:170px;"/>

<br>

9. In the left navigation pane, click **Rewrite** to open the Rewrites Manager dashboard.

10. Click the **Head/Tail** tab, then locate **dsl router** in the list of rewrites.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_dslrouter.png"/>

<br>

Take a minute to review the information in the **dsl router** row. We can see Fusion's suggested improvement (```router^2 dsl^3```) for the query. We can also observe that **Status** is set to **Auto** and that **Published** is set to **Yes**. This is because the Head/Tail suggestion falls into the auto publish category set by the head-tail relevancy job we ran earlier in the lab. 

Let's go ahead and manually approve this suggestion, and see what happens.

11. In the **dsl router** row, click the dropdown arrow in the **Status** field and select **Approved** from the list.

>Notice that changing the status will automatically unpublish the rewrite. 

12. To republish the **dsl router** rule, hover in its **Published** field and click the **green up arrow** option. Click **Publish** in the dialog to confirm the action. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_dlsrouterchanges.png"/>

<br>

We have republished this rule, which will affect the query results the next time a user searches for **dsl router**. Let's go back to Fusion, execute our search, and see how the change affects the returned results.

13. Return to the Fusion tab and navigate back to the **Query Workbench** tab.

14. Click the green circle next to the **Text Tagger** stage to disable it. 

>The Text Tagger stage queries a handler to perform spell correction, phrase boosting, and synonym expansion actions. We want to first view our unfiltered restuls, therefore we are disabling this stage for the moment. 

15. In the lower right corner, locate the **View As** field. Click the dropdown arrow, then select **Debug** in the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_texttagger.png"/>

<br>

16. In the search field, execute a query for ```dsl router```. 

<br>

On review of the search results, notice that Fusion is using the <b>rawquerystring</b> and <b>querystring</b> fields to perform this search. Disabling the Text Tagger stage prevents Fusion from applying the rewrite rule that we just published.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_dslsearch.png"/>

<br>

17. Click the circle next to the **Text Tagger** stage to re-enable it. If the search results display does not automatically update, requery **dsl router** to see the changes to the relevancy of the returned results.

You can see that re-enabling the **Text Tagger** stage has applied our published rule, and the **rawquerystring** and **querystring** fields now display the improved query suggestion to produce the new search results. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_dslimprovedsearch.png"/>

<br>

To see further evidence of how this works, take a moment and toggle the Text Tagger stage on and off. When you view the **explain** field for each option, you can see the change to the document score that occurs when the stage is enabled and the rule is applied. 

## Misspelling Rewrites

Now that we have reviewed head/tails adjustments, let's move on to another query rewrite function, Misspelling Detection.

18. Navigate back to the **Jobs** tab, and repeat steps 3-5 to run the ```relevancy-spell-correction``` job.

Once it has been successfully run, we want to navigate to the Rewrites Manager and view the job's results.

19. Navigate back to the **Rewrites Manager** browser tab.

20. Click the **Misspelling** tab, then locate the **lenevo** entry in the list of rewrites.

Take a minute to review the information in the **lenevo** row. We can see Fusion's suggested improvement (```lenovo```) for the query. We can also observe that **Status** is set to **Pending** and that **Published** is set to **No**.  

>Unlike the Head/tail job, our misspelling corrections require us to review and manually approve them.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_lenovo.png"/>

<br>

Let's go ahead and manually approve this suggestion, and see what happens to our search results.

21. In the **lenevo** row, click the dropdown arrow in the **Status** field and select **Approved** from the list.

22. To publish the **lenevo** rule, hover in its **Published** field and click the **green up arrow** option. Click **Publish** in the dialog to confirm the action. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_lenovochanges.png"/>

<br>

We have republished this rule, which will affect the query results the next time a user searches for **lenevo**. Let's go back to Fusion, execute our search, and see what happens.

23. Return to the Fusion tab and navigate back to the **Query Workbench** tab.

24. Click the green circle next to the **Text Tagger** stage to disable it.

25. In the **View As** field, click the dropdown arrow and select **Results** in the list.

26. In the search field, execute a query for ```lenevo``` (the misspelled term).

When we disable the Text Tagger stage and execute the search, notice that we do not return any results for the misspelled term (which is exactly what we would expect to happen).

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_lenovosearch.png"/>

<br>

27. Click the circle next to the **Text Tagger** stage to re-enable it. If the search results display does not automatically update, requery **lenevo** to see the changes to the relevancy of the returned results.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_lenovoimprovedsearch.png"/>

<br>

Once again, notice how even though we searched for the misspelled term, the search is enhanced (and the misspelling rule is applied) when we enable the Text Tagger stage, and we return the results we are looking for.

To see this in further detail, you can change the **View As** field to **Debug** and explore the stage. Notice the **rawquerystring** and **querystring** fields display the improved query suggestion, which now produces search results. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_lenovoimprovedsearch2.png"/>

<br>

## Phrase Detection Rewrites

For our last exercise, let's practice using the Phrase Detection rewrite strategy.

28. Navigate back to the **Jobs** tab, and repeat steps 3-5 to run the `relevancy-phrase-extraction` job.

Once it has been successfully run, we want to navigate to the Rewrites Manager and view the job's results.

29. Navigate back to the **Rewrites Manager** browser tab. 

30. Click the **Phrase** tab, then locate the `dell inspiron` entry in the list of rewrites.

Take a minute to review the information in the **dell inspiron** row. We can see Fusion's suggestion that (`dell inspiron`) is a phrase frequently entered by users. We can also observe that **Status** is set to **Pending** and that **Published** is set to **No**.  

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_dell.png"/>

<br>

One more time, let's go ahead and manually approve this suggestion, and see how it affects our search results.

31. In the **dell insipiron** row, click the dropdown arrow in the **Status** field and select **Approved** from the list.

32. To publish the **dell inspiron** rule, hover in its **Published** field and click the **green up arrow** option. Click **Publish** in the dialog to confirm the action. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_dellchanges.png"/>

<br>

We have republished this rule, which will affect the query results the next time a user searches for **dell inspiron**. Let's go back to Fusion, execute our search, and see what happens.

33. Return to the Fusion tab and navigate back to the **Query Workbench** tab.

34. Click the green circle next to the **Text Tagger** stage to disable it.

35. In the search field, execute a query for ```dell inspiron``` (our phrase).

When we disable the Text Tagger stage and execute the search, notice that we see **dell inspiron** products at the top of our search results. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_dellsearch.png"/>

<br>

Before we re-enable the Text Tagger stage, let's observe what is happening behind the scenes.

36. In the **View As** field, click the dropdown arrow and select **Debug** in the list.

At first glance, the **rawquerystring** and **querystring** fields display our search term, as expected. When we take a closer look at the **parsedquery** field, we can see that the search looked for each term separately, instead of treating them as a phrase (which is what we want to happen).

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_dellsearch2.png"/>

<br>

37. Click the circle next to the **Text Tagger** stage to re-enable it. If the search results display does not automatically update, requery **dell inspiron** to see the changes to the relevancy of the returned results.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/airewrit/airewrit_dellimprovedsearch.png"/>

<br>

If you were to click the **View As** field, select the **Results** option and view the results, you would most likely see that the top documents returned did not change. However if you look closely at the **parsedquery** field when the Text Tagger stage is applied, you can see that the improved search query is now treating **dell insipron** as a phrase, which in turn gives the affected documents a higher score, which will improve the overall search ressults returned for the user.

Feel free to continue practicing with the rewriting strategies covered in this lab, approving and publishing the rule, then using Query Workbench to validate your relevancy changes.

---
<br>

## Great job! You have successfully completed the Query Analytics Lab, where you have practiced creating functioning query rewrites.

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