---
layout: page
title: Predictive Merchandiser - Rewrites Lab
permalink: /pmrewrit/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

# It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Predictive Merchandiser Search Rewrites Lab! <br> Through this set of lab activities, you will practice creating and managing search rewrites using Predictive Merchandiser.

---
<br>

In this lab, you will be following a real scenario to:
* Apply misspelling detection, phrase detection, synonym detection, and head/tail rewrite options using the Merchandiser Dashboard.
* Create a search rewrite from the Rewrites Manager.

<br>

Different from our other labs, we encourage you to try the exercise first, then check to see how you did. If you get stuck, we have provided the following to keep you moving:
* **Hints** provide helpful clues regarding the appropriate task to perform.
* **Solution Steps** walk you through step by step instructions, detailing how to complete the task. 

---
<br>

## Merchandiser Dashboard

For this lab, we are going directly into the Merchandiser Dashboard, where we will be selecting the **Electronics** app that has already been configured for our lab environment. 

1. In the PM interface, click the dropdown arrow and select the **Electronics** app.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_PMselectapp.png"/>

<br>

2. In the "What's your solution type?" window, select **Product Discovery**.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_PMproductdiscovery.png"/>

<br>

><b>Note:</b> It is important to understand that you can create search rewrites from either the Merchandiser Dashboard *or* the Rewrites Manager. We will explore both options through the following lab activities, starting with the Merchandiser Dashboard.

<br>

## Getting Started

After looking through some data, you have underperforming queries you need to resolve. You **begin a task** to start editing your catalog.

How can you do this?

<details>

<summary>Solution Steps</summary> 

3. In the top right corner, click **Start Task**.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_PMstarttask.png"/>
</details>

<br> 

## Synonym Detection

You've recently noticed that when customers search for ```television```, it returns different results than if a customer searches for ```TV```. You and your team have decided that if a customer searches either term, **you want both results lists to display**. 

What can you do so that a user will see results for "TV" or "television" whenever they search either term?

<details>

<summary>Hint</summary> 

* Use the search rewrite Synonym Detection option.
</details>

<details>

<summary>Solution Steps</summary> 

4. In the search field, execute a search for ```TV```, then click the **blue plus** to add a rewrite. 

>If you don't immediately see the icon, click anywhere outside of the search box, then hover your cursor over the search box.  

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_synonymblueplus.png"/>

<br>

5. Select **Synonym** in the list of search rewrite options. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_synonym.png"/>

<br>

6. In the Synonym dialog, enter the following values:
* Click in the **Direction** field and select ```symmetric```.
* In the **Synonym Mappings** field, enter ```television```.

7. Click **Save** to add the new query rewrite.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_synonymfields.png"/>

<br>

>A confirmation message will appear in the bottom right corner of the screen indicating the query rewrite has been successfully created. 

</details>

</br> 

## Misspelling Detection

A lot of users seem to be searching for Frigidare appliances, but aren't getting the results returned that they want because the appliance manufacturer is actually spelled *```Frigidaire```*. 

How can you resolve this spelling error?

<details>

<summary>Hint</summary> 

* Use the search rewrite Misspelling Detection option.
</details>

<details>

<summary>Solution Steps</summary> 

8. In the search field, execute a search for ```Frigidare``` (the incorrect term), then click the **blue plus** to add a rewrite. 

>If you don't immediately see the icon, click anywhere outside of the search box, then hover your cursor over the search box.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_misspellblueplus.png"/>

<br>

9. Select **Misspelling** in the list of search rewrite options.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_misspell.png"/>

<br>

10. In the Misspelling dialog, enter the following values: 
* In the **Corrected Term** field, enter ```Frigidaire```.
* Click in the **Action** field and select ```replace```. 

11. Click **Save** to add the query rewrite.  

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_misspellfields.png"/>

<br> 

>A confirmation message will appear in the bottom right corner of the screen indicating the query rewrite has been successfully created. 

</details>

</br> 

## Phrase Detection

Your signals data indicates that customers are having a hard time finding ```HDMI Adapters``` within your inventory. You wonder if it's because **the system isn't recognizing the two words go together**. 

What can you do to ensure the system sees the two words as phrase?

<details>

<summary>Hint</summary> 

* Use the search rewrite Phrase Detection option.
</details>

<details>

<summary>Solution Steps</summary> 

12. In the search field, execute a search for ```HDMI Adapter```, then click the **blue plus** to add a rewrite. 

>If you don't immediately see the icon, click anywhere outside of the search box, then hover your cursor over the search box.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_phraseblueplus.png"/>

<br>

13. Select **Phrase** in the list of search rewrite options.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_phrase.png"/>

<br>

14. In the Phrase dialog, enter the following value:
* In the **Word Count** field, enter the number ```2```.

15. Click **Save** to add the query rewrite. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_phrasefields.png"/>

<br>

>A confirmation message will appear in the bottom right corner of the screen indicating the query rewrite has been successfully created. 

</details>

</br> 

## Head/Tail Analysis 

Some of your data is indicating that when customers search ```32 GB iPad black w/charger``` within your inventory, the return results are less than ideal. You want to ensure that **when this term is searched, the query results represent a better performing query of the same or similar products**.  

Can you rewrite this so that the returned results represent a better performing query?  

<details>

<summary>Hint</summary> 

* Use the search rewrite Head/Tail option.

</details>

<details>

<summary>Solution Steps</summary> 

16. In the search field, execute a search for ```32 GB iPad black w/charger```, then click the **blue plus** to add a rewrite. 

>If you don't immediately see the icon, click anywhere outside of the search box, then hover your cursor over the search box.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_headtailblueplus.png"/>

<br>

17. Select **Head/Tail** in the list of search rewrite options.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_headtail.png"/>

<br>

18. In the Head/Tail dialog, enter the following value:
* In the **Improved Query** field, enter ```32 GB iPad```. 

19. Click **Save** to add the query rewrite.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_headtailfields.png"/>

<br>

>A confirmation message will appear in the bottom right corner of the screen indicating the query rewrite has been successfully created. 

</details>

</br> 

## Rewrites Dashboard

Now that you have set up rewrites from the Merchandiser Dashboard, it's time to view them all in a list that you can export or edit. 

How do we navigate there?

<details>

<summary>Solution Steps</summary> 

20. In the left navigation pane, click **Rewrite** to open the Rewrites Manager dashboard.

21. On the Rewrites Manager page, click **Export** to download a .csv file where you can view the list of requested changes.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_export.png"/>
</details>

<br>

## Adding One More Rewrite

After reviewing, you realize there is one more rewrite you need to include in your list of edits. Customers on more than one occasion have made the typo *`Applw`* when searching for Apple products. **You want to ensure they are able to view all Apple products even when they accidentally spell it wrong**. 

How can you create a rewrite to make sure the returned results reflect the correctly spelled manufacturer?

<details>

<summary>Hint</summary> 

* Use the search rewrite Misspelling Detection option from the Rewrites Manager dashboard.

</details>

<details>

<summary>Solution Steps</summary> 

22. In the Rewrites window, click the **Misspelling** tab, then click **Add** and enter the following values:
* In the **Misspelling** field, enter ```Applw```.
* In the **Suggested Correction** field, enter ```Apple```.

23. In the Published column, click the blue check button to save this rewrite request.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_apple.png"/>

<br>

24. In the top right corner of the page, click **Publish** to publish the rule change.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/pmrewrit/pmrewrit_publish.png"/>

</details>

<br>

---
<br>

## Great job! You have successfully completed the Predictive Merchandiser Rewrites Lab, where you have learned about creating and managing search rewrites using Predictive Merchandiser.

---
<br>

## Hope to see you in our next course!
## Thanks and happy learning!
