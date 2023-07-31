---
layout: page
title: Relevance
permalink: /ffrelev/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

## It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Relevance Lab! <br> Through this set of lab activities, you will see how the BM25 algorithm affects document scoring, then apply boosts to increase the relevance of our returned results.

---
<br>

For this lab, we will use the Online Shoes app from our Queries lab activities. 

1. On the Fusion launch page, click the **Online_Shoes** app to open it and enter the Fusion workspace.

<br>

## Document scoring

As a reminder, Fusion uses two different scoring algorithms to calculate how well a given document matches a query. One of these is BM25, which we are going to see in action here.

2. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list.

 <img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_querying.png" style="height: 300px; width:200px;"/>

<br>

><b>Note:</b> If you don't see any results, click **Load** in the top right corner, then select **Online_Shoes** from the list. 
<br>   
<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffrelev/ffrelev_queryworkbenchload.png" style="height: 150px; width:450px;"/>

<br>   

Let’s look at a couple of things:
* <b>The Query search field:</b> The default search contains <b>:*:</b>, which is the syntax for a query of all results.
* <b>Score: 1 :</b> This is the BM25 score for a document. You will notice it has the same value for each document, based on the fact that we queried all available documents.

 <img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffrelev/ffrelev_queryscorefields.png" />

<br>

Let's enter a query and see how our document scores change.

3. In the search field, execute a query for ```ballet shoes```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffrelev/ffrelev_balletshoequery.png"/>

<br>

For our updated results, take note of the BM25 score for each returned document. Documents whose only difference is their size should have the same (or relatively identical) BM25 scores (as seen in the first and third document in the list), but you will notice as you scroll down through the remaining results, the scores get progressively lower. This is BM25 in action!

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffrelev/ffrelev_balletshoescored.png"> 

<br>

4. In the lower right corner, locate the **View As** field. Click the dropdown arrow, then select **Debug** in the list. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffrelev/ffrelev_debug.png"/>

<br>

The upper part of the Debug view shows some general information about the query itself. We can see that the Dismax parser is being used, and we can also see some boosting happening (indicated by ^5.0) in various places. <br><br>The **explain** section provides a full description of how the relevancy score for each document in the result set was calculated using the BM25 algorithm. Finally, notice that the weight of this document (16.696307 in this image) comes from the combined weights of the two individual words.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffrelev/ffrelev_debugresults.png">

<br>

5. In the **View As** field, click the dropdown arrow, then select **Results** in the list.

<br>

## Boosting with field values

6. Click the green circle next to the **Query Fields** stage to disable it.

><b>Note:</b> We are disabling this stage because we want to use some custom parameters. We will create a new stage while keeping this original Query Fields stage for later use.

<br>

7. Click **Add a Stage** and begin typing ```additional```, then select **Additional Query Parameters** from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffrelev/ffrelev_addstage.png"/>

<br>

8. In the **Label** field, enter ```myQueryParams```.

9. In the Parameters and Values section, click the green plus, then add the following values:
* In the **Parameter Name** field, enter ```fl```.
* In the **Parameter Value** field, enter ```*,score```.
* Click the **Update Policy** field and select ```replace```.

 <img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffrelev/ffrelev_myqueryparamsdetails.png" style="height: 350px; width:300px;"/>

 <br>

10. Click **Apply** to create the new ```myQueryParams``` stage, then click **Cancel** to collapse the configuration window and see a larger view of our results.

<br>

Notice that our results have changed with the addition of the new **myQueryParams** stage. 

<br>

For our last exercise in this lab, let's add a boost directly to the query, and see how the scores are affected. 

11. In the search field, execute a query for ```ballet^10 shoes```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/ffrelev/ffrelev_balletshoesboost.png">

<br>

Notice that the boosting of the term **ballet** has affected our returned results, making the result scores much higher when the document contains the boosted term. Feel free to try other boosting values and note the results.

---
<br>

## Great job! You have successfully completed the Relevance Lab, where you have seen how the BM25 algortihm works, and learned how to apply boosting to manipulate document relevance. 

<br>

>Make sure to **Save** your open Fusion workspace tabs before exiting the application.

<br>

If you would like to save your Fusion app to import and practice with later, you can do it now:
1. In the left navigation panel, click **Apps**, then choose **Return to Launcher** from the list.
2. Hover over your app until a cog appears in the lower right corner.
3. Click the cog icon.
4. In the pop-up window, click **Export app to zip**.

-----
<br>

## Hope to see you in our next course! 
## Thanks and happy learning!
