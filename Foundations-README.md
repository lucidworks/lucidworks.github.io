---
layout: page
title: Foundations Readme
permalink: /Foundations/
---

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol.Please do not click *Start Lab* again. It may take a few mintues for the Fusion environment to fully display.

When the Fusion Login page displays, login:
* USERNAME: ```admin```
* PASSWORD: ```password123```


## Welcome to the Indexing Lab, in this lab  you will ingest a datasource, index your data and make schema changes. When we're done you'll have a functioning Fusion collection! .....Let's get started by creating a Fusion App...

 

1. Click on **Create new app**, name it ```Online_Shoes``` and click **Create App**. It will take a few seconds to create. 
   
2. Click on your newly created app **Online_Shoes** to enter the *Fusion workspace*, this is where you can configure how an app ingests, indexes, queries, and analyzes data 

# Ingest your Data

4. Hover over the **INDEXING** icon in the sidebar, then click **Datasources**

 <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%205%20ff%20ingest.png" style="height: 300px; width:400px;"/>
   
5. Click **Add+**, from the drop-down menu, click on **File Upload** 
   
6. Let's add some parameters:
    * In **DATASOURCE ID** add: ```shoes```
    * In **FILE ID**, add: ```data.json.zip``` then click **Save**

7. Click **Run**, then click **Start**

>Note: Success! The job will take about 2 minutes, when it's done, the "running" icon will change to a "sunshine".

8. Click **Save**, then close the job box

 <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%209%20ff%20ingest%20close%20job%20box.png" style="height: 170px; width:300px;"/>


# Index your data 

9.  Hover over **INDEXING**, click on **Index Workbench**
   
10.   Click **Load** then click on **Shoes** from the drop-down

 <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%209%20FF%20ingest.png" style="height: 100px; width:400px;"/>

>Note: Here we see simulated results for our shoes data, with the fields for the first result expanded. Take a minute to explore the data!

11.   Hover over **COLLECTIONS** in the sidebar, then click **Fields**

 <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%2012%20ff%20ingests%20fields.png" style="height: 200px; width:300px;"/>

>Note: This is a detailed list of fields. What is the most commmon field type for this data? Let's explore one of these fields a bit more

12.   Scroll down and find the ***_dt** field, click on it to expand the Edit Field window, can you find the field type?

<details>
<summary>Check your answer!</summary> 

This field type is **pdate**
</details>
<br />

13.  Click on the field row again to close it, then click the **"play"** button to drop down a detailed list of all the individual fields that are using this dynamic field

 <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%2012%20play%20button%20explore%20dynamic%20fields.png" style="height: 300px; width:500px;"/>


# Manage your Schema

14.   Click **Add a Field+** and add these parameters:
* **Field Name**: ```item-data```
* **Field Type**: text_en
* Check **Indexed** and **Multivalued** 
* Uncheck **Stored**
* Click **Save**

15.   Let's create a static field for Brand. Start by clicking **Add a Field**, and include these parameters:
* **Field Name**: ```brand```
* **Field Type**: string
* Ensure **Indexed** and **Stored** are checked
* Click **+ Copy Fields to** 
* **Copy Fields To**: item-data
* Click **Save**
  
<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%2016%20copy%20fields%20ff%20ingest.png" style="height: 100px; width:500px;"/>

>Note: You now have two new static fields: brand and item-data. However, they have no values in the Num Docs column. At this point, you also have multiple windows open in your Fusion workspace. Each window is shown in the tabs along the bottom of the UI. You can navigate to each window by clicking the tabs. Find and return to the **Datasources** window  <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%2016%20note%20ff%20ingest.png" style="height: 50px; width:600px;"/>


16.  Because we made changes to the Schema, we need to re-index our data. Open the **shoes** datasource

17.  Click **Clear Datasource**, then click **Yes, clear**

18.  Click **Run** then click **Start**. Again, the job will take a few minutes to complete. When the job finishes running, click **Save**

19.  Return to the **Fields** window. Your new fields should have Num Docs values

20.  Add the following fields and their parameters by repeating **step 15** for each row:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Ingestion/step%2019%20field%20params.png" style="height: 350px; width:700px;"/>

>Note: We're taking these steps to prepare our data for the ingestion and indexing process. This then improves our query relevance in future labs.

21. We need to re-index again! Return to the **Datasources** window, open the **shoes** datasource, then Click **Clear Datasource**

22. Click **Run** then click **Start**, when the job finishes running, click **Save**

23. Return to the **Fields** window. Close it and reopen it to refresh. Notice that almost all the new static fields have Num Docs values

24. Return to the **Index Workbench**, and click on the arrow next to the **Parser** icon

25. Take a minute to review the **Simulated Results**, then click on the green circle next to the **CSV** parser to deselect it

<details>
<summary>What Happened?</summary> 

Nothing! there was no change to your results - this data is in JSON format!
</details>

26.  Click on the green circle next to the **JSON** parser to deselect it. Notice that now all fields other than _lw_* fields have been moved into one field labeled body_t. This is not what we want! 

27. Click on the circle next to the **JSON** parser stage to reselect the parser stage. Your results will revert to much more usable fields again.

>Note: This exercise demonstrates the critical importance of parsers in the ingestion process. In a real-world setting, you would likely need many different parsers

28. Make sure to **Save** your open Fusion Workspace tabs!

_______________________________________________________________________________

Great job! You now have a functioning Fusion app with data and a customized Schema! If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app, a cog will appear in the lower right corner, click it
3. On the box that opens, click **Export app to zip**
   
This concludes the Ingestion Lab. 



<link href="../lib/public/global-training.css" rel="stylesheet"></link>

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol.Please do not click *Start Lab* again. It may take a few mintues for the Fusion environment to fully display.

When the Fusion Login page displays, login:
* USERNAME: ```admin```
* PASSWORD: ```password123```

## Welcome to the Queries Lab, in this lab you will tune queries so users get relevant results when they search! .....Let's get started by accessing the Online Shoes app...


1. At the Fusion Launcher, click on the **Online_Shoes** app

# Query Results

3. Hover over the **QUERYING** Icon, and click on **Query Workbench**

 <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Queries/step%202%20ff%20queries.png" style="height: 200px; width:300px;"/>

>Note: Here we can see the first ten documents returned from the shoes dataset. However, these results are in a raw form and are difficult to read. We can change this by changing the Display Fields. 

4.  Click on the **Display Fields** dropdown

5. Can you find the **Name** and **Description** parameters?

<details>

<summary>Check your answers!</summary> 

* NAME: id
* DESCRIPTION: descriptions

</details>

<br />

6. Change the parameters in the **Display Fields** window:
* NAME: ```name```
* DESCRIPTION: ```categories```

7. Click **Display Fields** again to see the updated results

>Note: These results are much more intuitive and easier for us to understand. But what order are they in? Let's do some sorting

8. Click in the **Sort Fields** box, type ```categories``` and click the autosuggestion in the dropdown

9. Click on **Descending** and change it to **Ascending**. We can see the first 8 results are sorted by number and the last two results begin with "ac", you can click **Next** to confirm this trend continues.

10. Clear the **Sort Field**

# Faceting

11. Click on **Add a field facet**
    
12. Type in ```sizes``` and click on **sizes** in the dropdown    

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Queries/step%2010%20FF%20queries.png" style="height: 200px; width:400px;"/>

<br />
<br />

>Note: A sizes field facet is now shown. The sizes themselves are on the left with the document count on the right in parenthesis. The facet order is based upon number of occurrences descending. Clicking on View next 10 will bring up the next set of less numerous facets

13. Add the following facets by clicking on **Add a field facet** and selecting them from the drop down:
* categories
* colors
* brand

14. It is likely that your facets will not be in the same order as the image here. Click and drag the “hamburger” icon to the right of each facet to match the image.

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Queries/step%2013%20ff%20queries.png" style="height: 500px; width:400px;"/>

<br />
<br />

>Note: In a production environment, the specific order of each facet may be critical!

15. With our field facets  in place we can get more specific with our result set. For instance, if you wanted a size 7 women’s boot in black, **click:**
* **sizes**: 7
* **categories**: Clothing, Shoes & Accessories, Women's Shoes, Boots
* **colors**: black

16. Review your new results. There are three items from three brands

17. What if you want a similar boot, but in taupe rather than black? **Click**:
* **colors**: Clear all
* **colors**: Taupe 

18. There is now a single result, found by faceting only. Explore these facets further before moving on

19. Reset you facets by clicking **Clear all**, then query all results by searching **\*:\***

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Queries/Step%2018%20FF%20Queries.png" style="height: 200px; width:500px;"/>

<br />

<br />

# Tuning Queries

20. Query for ```red boots``` and explore the first 10 results

>Note: Notice that we do see some boots in the result set. However, there are also heels, flats, sandals, and even a red dress! Looking at the field facets we can see that in our returned results there are more black and brown facets then there are red ones. An end user could use field facets to get better results, or even execute a more precise query. However, we want the end user to find what they are looking for as seamlessly as possible. 

21. Lets use the **Query Fields** pipeline stage to clean these results up for the end users. Click on the **Query Fields** pipeline stage. A configuration window will open

22. Under **Search Fields**, click the green + sign to add a new field, In the box that appears: Type in ```colors``` and select it from the dropdown


<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Queries/step%2021%20FF%20queries.png" style="height: 350px; width:450px;"/>

<br />
<br />


23. Repeat step 21 to add two more **Search Fields**: ```brand``` and ```name```, then click **Appy**

>Note: By applying new search fields into the Query Fields stage, we can already see changes in the results list

24. Click: **Cancel** inside the Query Fields parameters window to collapse it down. This will allow for an unobstructed view of our fresh results


<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Queries/step%2022%20FF%20queries.png" style="height: 350px; width:450px;"/>

<br />
<br />

>Note: Our results now have a symbol on the right indicating that they were added to the page or that a result was dropped in the ranking.
The results contain more boot entries now, and red is the predominant color.
Finally, if we compare these results to those shown from our first search, the number of docs returned has also decreased.


25. Click on Query Fields to open the parameters window. Enter the following into the Field Boost boxes:
* **colors Field Boost**: ```1```
* **name Field Boost**: ```5```

26. Click: **Apply**, then return to the results page and review the new results

>Note: All the results now are red or a combination of red and another color.
Most of our results now have ”boots” in the name.
The last result is bothersome though, considering that we are trying to sell shoes

27. Hover over the last result, click **Block**. The polka dot corset will disappear from the results list


>Note: Our results are now much more user friendly. Feel free to continue to play around with the results.

28. Make sure to **Save** your open Fusion Workspace tabs!

# Extra Credit!

Using the skills that you’ve gained in this lab, find this shoe in the dataset:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Queries/Extra%20credit%20FF%20queries.png" style="height: 300px; width:400px;"/>

<br />
<br />

* You can use the search bar and the field facets or any combination of the two.
* There will be any number of ways to find this shoe. 

<details>

<summary>Need a Hint?</summary> 

Use facets to help narrow down the results. For example, can you determine the  color and brand from the picture?

</details>

<br />

<details>

<summary>Solution!</summary> 

Full query: Marc Fisher Tinsel Women Open Toe Synthetic Platform Sandal
 
</details>

<br />

_______________________________________________________________________________

Great job! You now know how to tune queries to ensure users get more relevant results, on the first try. If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app, a cog will appear in the lower right corner, click it
3. On the box that opens, click **Export app to zip** 
   
This concludes the Queries Lab.



<link href="lib/public/global-training.css" rel="stylesheet"></link>

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol.Please do not click *Start Lab* again. It may take a few mintues for the Fusion environment to fully display.

When the Fusion Login page displays, login:
* USERNAME: ```admin```
* PASSWORD: ```password123```

## Welcome to Relevance Lab, in this lab you will see BM25 in action and apply boosts to manage relevance.....Let's get started by accessing the Online Shoes app...


1. At the Fusion Launcher, click on the **Online_Shoes** app
   
2. Hover over the **QUERYING** icon, then click on **Query Workbench**

3. If you don't see any results, click **Load**, then click **Online_Shoes**
   

# BM25

>Note: Let’s look at a couple of things here:
* The Query box: By default, the Query Workbench contains **\*:\***, This is the syntax for a query of all results.
* Score:1 in grey: This is the BM25 score for each document. You will notice that it has the same value for each doc. That is because we are querying for all docs.

 <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Relevance/step%205%20FF%20relevance.png" style="height: 200px; width:300px;"/>

<br />
<br />

5. Query for ```ballet shoes```

>Note: Notice the BM25 score for each doc. The first two values are the same because they are the same shoe in different sizes. But notice as you scroll down through the remaining results, the scores get progressively lower. This is BM25 in action!

6. In the lower right, find the **View As** box and click on **Results**, in the pop-up, click on **Debug** 

>Note: The upper part of the Debug view shows some general information about the query itself. We can see what type of parser is being used: Dismax. We can also see some boosting happening, (indicated by ^5.0) in various places. The explain section provides a full description of how the relevancy score for each document in the result set was calculated using the BM25 algorithm. Finally, notice that the weight of this document (16.696402 in this image) comes from the combined weights of the two individual words.

7. Change **View As**: back to **Results** 

# Boosting on Field Values

8. Click on the **Query Fields** stage on the left. Disable **Query Fields** by deselecting the green circle.

>Note: We are disabling this stage because we want to use some custom parameters. We will create a new stage while keeping this original Query Fields stage for later use

9. Click on **Add a Stage**, then begin typing ```additional``` for the auto-suggestion of **Additional Query Parameters** to appear. Click on **Additional Query Parameters**

10. A **myQueryParams** box will open, fill it out with the following:
* Label: ```myQueryParams```
* Parameters and Values: click the green plus icon
* Parameter Name: ```fl```
* Paramter Value: *,score
* Update Policy: replace
* Click **Apply**

 <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/01%20FF/Relevance/step%2010%20FF%20relevance.png" style="height: 350px; width:300px;"/>

<br />
<br />

11. Return to your **Results** (you may need to click **Cancel** in the myQueryParams box after clicking **Apply** to view your results)

>Note: Notice that our results have changed. Also take note of the Score of these documents, as they will change significantly in the next step.

12. Query for: ```ballet^10 shoes```

>Note: The results change. Notice the boosting of the term **ballet** makes the result scores much higher when the document contains the term. Try other boosting values and note the results.

13. Make sure to **Save** your open Fusion Workspace tabs!

___________________________________________________________________________________

Great job! You now know how the BM25 algortihm works and how to apply boosting to manipulate relevance.  If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app, a cog will appear in the lower right corner, click it
3. On the box that opens, click **Export app to zip**
   
This concludes the Relevance Lab.
