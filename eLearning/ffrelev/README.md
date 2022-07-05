---
layout: page
title: Relevance
permalink: /ffrelev/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

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
