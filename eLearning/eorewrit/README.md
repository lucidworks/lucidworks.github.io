---
layout: page
title: Experience Optimizer - Rewrites Lab
permalink: /eorewrit/
---

<link rel="stylesheet" href="./lib/public/global-training.css">

# It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Experience Optimizer Search Rewrites Lab! <br> Through this set of lab activities, you will practice creating and managing search rewrites using Experience Optimizer.

---
<br>

In this lab, you will be following a real scenario to: 
* Apply misspelling detection, phrase detection, synonym detection, and head/tail rewrite options using the Optimizer Dashboard.
* Create a search rewrite from the Rewrites Manager. 

<br>

Different from our other labs, we encourage you to try the exercise first, then check to see how you did. If you get stuck, we have provided the following to keep you moving:
* **Hints** provide helpful clues regarding the appropriate task to perform.
* **Solution Steps** walk you through step by step instructions, detailing how to complete the task. 

---
<br>

## Optimizer Dashboard

For this lab, we are going directly into the Experience Optimizer Dashboard, where we will be selecting the **Site Search** app that has already been configured for our lab environment.

1. Click the dropdown arrow and select the **Site Search** app. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_PMselectapp.png"/>

<br>

2. In the "What's your solution type?" window, select **Knowledge Management**.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_EOknowmgmt.png"/>

<br>

><b>Note:</b> It is important to understand that you can create search rewrites from either the Optimizer Dashboard *or* the Rewrites Manager. We will explore both options through the following lab activities, starting with the Optimizer Dashboard.

<br>

## Getting Started

After looking through some data, you have underperforming queries you need to resolve. You **begin a task** to start editing your catalog.

How can you do this?

<details>

<summary>Solution Steps</summary> 

3. In the top right corner, click **Start Task**.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eodash/eodash_starttask.png"/>
</details>

<br>

## Synonym Detection

You've recently noticed that when users search for ``data science``, it returns different results than if a user were to search for ``data analytics``. You and your team have decided that if a user searches either term, **you want both results lists to display**. 

What can you do so that a user will see results for "data analytics" or "data science" whenever they search either term?

<details>

<summary>Hint</summary> 

* Use the search rewrite Synonym Detection option.
</details>

<details>

<summary>Solution Steps</summary> 

4. In the search field, execute a search for `data analytics`, then click the **blue plus** to add a rewrite. 

>If you don't immediately see the icon, click anywhere outside of the search box, then hover your cursor over the search box.  

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_synonymblueplus.png"/>

<br>

5. Select **Synonym** in the list of search rewrite options.  

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_synonym.png"/>

<br>

6. In the Synonym dialog, enter the following values:
* Click in the **Direction** field and select ``symmetric``.
* In the **Synonym Mappings** field, enter `data science`.  

7. Click **Save** to add the new query rewrite.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_synonymfields.png"/>

<br>

>A confirmation message will appear in the bottom right corner of the screen indicating the query rewrite has been successfully created. 

</details>

</br> 

## Misspelling Detection

A lot of users seem to be searching for **Fuison**, but aren't getting the results returned that they want because the product is actually spelled *``Fusion``*. 

How can you resolve this spelling error?

<details>

<summary>Hint</summary> 

* Use the search rewrite Misspelling Detection option.
</details>

<details>

<summary>Solution Steps</summary> 

8. In the search field, execute a search for `Fuison` (the incorrect term), then click the **blue plus** to add a rewrite. 

>If you don't immediately see the icon, click anywhere outside of the search box, then hover your cursor over the search box.  

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_misspellblueplus.png"/>

<br>

9. Select **Misspelling** in the list of search rewrite options.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_misspell.png"/>

<br>

10. In the Misspelling dialog, enter the following values:
* In the **Corrected Term** field, enter `Fusion`.
* Click in the **Action** field and select ``replace``. 

11. Click **Save** to add the query rewrite.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_misspellfields.png"/>

<br>

>A confirmation message will appear in the bottom right corner of the screen indicating the query rewrite has been successfully created. 

</details>

</br> 

## Phrase Detection

Your signals data indicates that users are having a hard time finding articles about ``artificial intelligence`` within your database. You wonder if it's because **the system isn't recognizing the two words go together**. 

What can you do to ensure the system sees the two words as phrase?

<details>

<summary>Hint</summary> 

* Use the search rewrite Phrase Detection option.
</details>

<details>

<summary>Solution Steps</summary> 

12. In the search field, execute a search for `artificial intelligence`, then click the **blue plus** to add a rewrite. 

>If you don't immediately see the icon, click anywhere outside of the search box, then hover your cursor over the search box.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_phraseblueplus.png"/>

<br>

13. Select **Phrase** in the list of search rewrite options.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_phrase.png"/>

<br>

14. In the Phrase dialog, enter the following value:
* In the **Word Cout** field, enter the number `2`.  

15. Click **Save** to add the query rewrite.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_phrasefields.png"/>

<br>

>A confirmation message will appear in the bottom right corner of the screen indicating the query rewrite has been successfully created. 

</details>

</br> 

## Head/Tail Analysis 

Some of your data is indicating that when customers search ``AI powered search initiatives`` within your inventory, the return results are less than ideal. You wonder if it's because the system isn't returning the best results to the user. You want to ensure that **when this term is searched, the query results represent a better performing query of the same or similar documents**.  

Can you rewrite this so that the returned results represent a better performing query?  

<details>

<summary>Hint</summary> 

* Use the search rewrite Head/Tail option.

</details>

<details>

<summary>Solution Steps</summary> 

16. In the search field, execute a search for `AI powered search initiatives`, then click the **blue plus** to add a rewrite. 

>If you don't immediately see the icon, click anywhere outside of the search box, then hover your cursor over the search box.  

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_headtailblueplus.png"/>

<br>

17. Select **Head/Tail** in the list of search rewrite options.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_headtail.png"/>

<br>

18. In the Head/Tail dialog, enter the following value:
* In the **Improved Query** field, enter `AI powered search`.

19. Click **Save** to add the query rewrite.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_headtailfields.png"/>

<br>

>A confirmation message will appear in the bottom right corner of the screen indicating the query rewrite has been successfully created. 

</details>

</br> 

## Rewrites Dashboard

8. Now that you have set up rewrites from the Optimizer Dashboard, it's time to view them all in a list that you can export or edit. How do we navigate there?

<details>

<summary>Solution Steps</summary> 

20. In the left navigation pane, click **Rewrite** to open the Rewrites Manager dashboard.

21. On the Rewrites Manager page, click **Export** to download a .csv file where you can view the list of requested changes.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_export.png"/>
</details>

<br>

## Adding One More Rewrite

After reviewing, you realize there is one more rewrite you need to include in your list of edits. Users on more than one occasion have made the typo *`smartanswers`* when searching for Smart Answers documents. **You want to ensure they are able to view all Smart Answers documents even when they accidently spell it wrong**. 

How can you create a rewrite to make sure the returned results reflect the correctly spelled manufacturer?

<details>

<summary>Hint</summary> 

* Use the search rewrite Misspelling Detection option from the Rewrites Manager dashboard.

</details>

<details>

<summary>Solution Steps</summary> 

22. In the Rewrites window, click the **Misspelling** tab, then click **Add** and enter the following values:
* In the **Misspelling** field, enter `smartanswers`.
* In the **Suggested Correction** field, enter `Smart Answers`.  

23. In the Published column, click the blue check button to save this rewrite request.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_smartanswers.png"/>

<br>

24. In the top right corner of the screen, click **Publish** to publish the rule change.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorewrit/eorewrit_publish.png"/>

</details>

<br>

---
<br>

## Great job! You have successfully completed the Experience Optimizer Rewrites Lab, where you have learned about creating and managing search rewrites using Experience Optimizer.

---
<br>

## Hope to see you in our next course!
## Thanks and happy learning!