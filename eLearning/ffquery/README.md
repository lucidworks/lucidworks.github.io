---
layout: page
title: Queries
permalink: /ffquery/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

## It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Queries Lab! <br> Through this set of lab activities, you will learn to use the Query Workbench to add facets and tune query results, so users get relevant results when they search! 

---
<br>

For this lab, we will once again use the **Online Shoes** app created in our Indexing Data lab. 

1. On the Fusion launch page, click the **Online_Shoes** app to open it and enter the Fusion workspace.

<br>

## Displaying query results

2. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list.

 <img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_querying.png" style="height: 300px; width:200px;"/>

<br>

We can see the first ten documents returned from the shoes dataset, however the results are in a raw form and are difficult to read.

We can change this by changing the results display fields. 

3. Click **Display Fields** and change the following values:
* In the **NAME** field, enter ```name```.
* In the **DESCRIPTION** field, enter ```categories```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_displayfields.png"/>

<br>

4. Click **Display Fields** again to close the dropdown and view the updated results. 

<br>

These results are much more intuitive and easier for us to understand. But what order are they in? 

Next, Let's sort our results based on one of the fields in our documents.

5. Click in the **Sort Fields** and begin typing ```categories```, then select **categories** from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_sort.png"/>

<br>

6. Click on **Descending** and change it to **Ascending**. 

<br>

In our results, we can see the first 8 results are sorted by their numerical value, and the last two results begin with "Acc", and so on. (Click **Next** to confirm this trend continues).

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_sortresults.png" style="height: 300px, width:500px;"/>

<br>

7. Clear the contents of the **Sort Field** before continuing on in the lab.

<br>

## Adding facets

In addition to changing our display fields and applying sorting options, we can create field facets that will help our users further narrow down the displayed search results.  

8. In the Query Workbench window, click **Add a field facet**.
    
9. Begin typing ```sizes```, then select **sizes** in the autosuggestion list. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_addfieldfacet.png" style="height: 240px; width:380px;"/>

<br>

A sizes field facet is now shown. The sizes themselves display on the left, with the document count in parentheses to the right. The facet order is in descending order based upon number of occurrences for the facet value. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_sizesfacet.png" style="height: 240px; width:380px;"/>

<br>

10. Add the following facets by clicking on **Add a field facet** and selecting them from the autosuggestion list:
* <b>categories</b>
* <b>colors</b>
* <b>brand</b>

<br>

><b>Note:</b> In a production environment, the specific order of your facets may be critical, therefore the display order of facets can be rearranged. Click the facet's hamburger icon, then drag and drop the facets into the order you want them to appear in your list. 
<br>   
<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_dragdrop.png" style="height: 254px; width:380px;"/>

<br>

With our field facets in place, we can get more specific with our result set. For instance, let's try looking for a women’s boot that is a size 7, in black.

11. Click the following selections in the facets list:
* **sizes**: 7
* **categories**: Clothing, Shoes & Accessories, Women's Shoes, Boots
* **colors**: black

<br>

Revewing our results, we can see that there are three items from three brands that will fit all of these facets. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_blackbootsresults.png" style="height: 290px; width:500px;"/>

<br>

Let's try another one. What if you want a similar boot, but in taupe rather than black?

12. Click the following selections in the facets list:
* **colors**: Clear all, then select Taupe

<br>

We can now see that there is a single result that meets our facet selections. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_taupebootsresults.png" style="height: 290px; width:500px;"/>

<br>

Feel free to explore more by clicking to add or clear facets and viewing the returned results. 

13. Reset you facets by clicking **Clear all**, then query all results by searching **\*:\*** before continuing on in the lab.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_clearfacets.png" style="height: 240px; width:300px;"/>

<br>
<br>

## Tuning query results

At first, your query results can often return documents that are not applicable to the search being performed. This exercise looks at how to tune your queries to return more accurate results.

14. In the search field, execute a query for ```red boots```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_redboots.png" style="height: 240px; width:300px;"/>

<br>

Reviewing our results, you will notice that we do see some boots in the result set. However, there are also heels, flats, sandals, and even a red dress! Looking at the field facets, we can see that in our returned results there are more black and brown facets then there are red ones. 

An end user could use field facets to get better results, or even execute a more precise query. However, we want the end user to find what they are looking for as seamlessly as possible. 

<br>

Next, we'll use our **Query Fields** pipeline stage to clean up our results. 

15. Click **Query Fields** to open the pipeline stage configuration window.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_queryfields.png" style="height: 200px; width:410px;"/>

<br>

16. Under **Search Fields**, click the green plus to add a new field. In the field, begin typing ```colors```, then select **colors** from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_querysortfields.png" style="height: 300px; width:410px;"/>

<br>

17. Repeat step 17 to add two more **Search Fields**: ```brand``` and ```name```.

18. Click **Apply** to save your changes to the pipeline stage, then click **Cancel** to collapse the configuration window and see a larger view of our results.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_applyqueryfields.png" style="height:300px; width:330px;"/>

<br>

Notice that the addition of these new search fields to our Query Fields pipeline stage has prompted changes in the displayed results. 

If we were to compare these results to those displayed from our first search, we would see that:
* The number of documents returned has decreased
* The results contain more boots entries now
* Red is the predominant color

Also notice that our results now diplay indicators that highlight documents that were added to the page or dropped in the ranking based on the addition of the new search fields.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_indicators.png" style="height:300px; width:400px;"/>

<br>

This has definitely helped refine our results, but let's apply some boosts to help return the most relevant documents higher in the ranking.

19. Click **Query Fields** to reopen the pipeline stage configuration window. 

20. In the **Field Boost** fields, enter the following values:
* In the **colors Field Boost**, enter ```1```.
* In the **name Field Boost**, enter ```5```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_fieldboosts.png" style="height:400px; width:340px;"/>

<br>

21. Click **Apply** to save your changes to the pipeline stage, then click **Cancel** to collapse the configuration window and see a larger view of our new results.

<br>

Notice that all the results now are red (or a combination of red and another color), and most of our results now have ”boots” in the name. The last result -Red Burlesque Polka Dot Corset - is bothersome though, considering that we are trying to search for boots.

<br>

Let's block this document from showing up in our search results.

22. Hover over the last result and click **Block**. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_block.png" style="height= 300px; width: 300px;"/>

<br>

The action means that polka dot corset will no longer appear in our results list, and our results are now much more user friendly. 

Feel free to continue to play around with the results before continuing on in the lab.

---
<br>

## Extra Practice!

Using the skills that you’ve gained in this lab, find this shoe in the dataset:

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffquery/ffquery_extrapracticeshoe" style="height: 300px; width:400px;"/>

<br>

Help to start:
* There are multiple ways to find this shoe.
* You can use the search bar and the field facets (or any combination of the two).

<details>

<summary>Need a hint?</summary> 

Use facets to help narrow down the results. For example, can you determine the color and brand from the picture?

</details>

<details>

<summary>Solution!</summary> 

Full query: Marc Fisher Tinsel Women Open Toe Synthetic Platform Sandal
 
</details>

---
<br>

## Great job! You have successfully completed the Queries lab, where you learned to use the Query Workbench to refine the search results for your end-users using facets and tuning. 

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
