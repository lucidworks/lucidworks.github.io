---
layout: page
title: Queries
permalink: /ffquery/
---

<link rel="stylesheet" href="/lib/public/global-training.css">


## The environment should begin to load immediately. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

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


23. Repeat step 21 to add two more **Search Fields**: ```brand``` and ```name```, then click **Apply**

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

