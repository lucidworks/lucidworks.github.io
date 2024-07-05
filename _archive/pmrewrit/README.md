---
layout: page
title: Predictive Merchandiser - Rewrites Lab
permalink: /pmrewrit/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

## The environment should begin to load immediately. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

1. When the Fusion Login page displays, login:
    * USERNAME: **admin**
    * PASSWORD: **password123**

## Using real world scenarios, you will create and manage Search Rewrites using Predictive Merchandiser.

You will practice solving everyday problems including: 
- Applying misspelling detection, phrase detection, synonym detection, and head/tail
- Creating rewrites from the Rewrites Manager


If you get stuck, we have provided helpful details to keep you moving. 

* **Hints** provide helpful clues regarding the appropriate task to perform.

* **Solution Steps** walk you through step by step instructions, detailing how to complete the task. 

<br>

## Merhandiser Dashboard

>Note: You will see a loading icon initially on the Merchandiser Dashboard. The next step will point Predictive Merchandiser to the appropriate application to pull from. 

2. Select the app **Electronics**. Select **Product Discovery**.

3. After looking through some data, you have underperforming queries you need to resolve. **Begin a task** to start editing your catalog.

<details>

<summary>Solution Steps</summary> 

1. Click **Start Task** in the upper right corner of the dashboard
</details>

</br> 

## Synonym Detection

4. You've recently noticed that when customers search for television, it returns different results than if a customer were to search for TV. You and your team have decided that if a customer searches either term, **you want both results lists to display**. What can you do so that a user will see results for TV or television whenever they search either term?

<details>

<summary>Hint</summary> 

- Use the search rewrite Synonym Detection
</details>

<details>

<summary>Solution Steps</summary> 

1. Search `TV` and click the **blue plus icon** to add a rewrite. If you don't immediately see the icon click anywhere outside of the search box, then hover your mouse over the search box.  

2. From the list of search rewrite options, select **Synonym**  

3. Choose the direction of **symmetric**  

4. Enter `television` in the Synonym Mappings field  

5. Click the **Save** button  

>The action should immediately take place and a confirmation dialogue box should appear at the top of the screen indicating the rewrite has fired. 

</details>

</br> 

## Misspelling Detection

5. A lot of customers seem to be searching for Frigidare appliances, but aren't getting the results returned that they want because the appliance manufacturer is actually spelled *Frigidaire*. **How can you resolve this spelling error**?

<details>

<summary>Hint</summary> 

- Use the search rewrite Misspelling Detection
</details>

<details>

<summary>Solution Steps</summary> 

1. Search `Frigidare` (the incorrect term) and click the **blue plus icon** to add a rewrite. If you don't immediately see the icon click anywhere outside of the search box, then hover your mouse over the search box.

2. From the list of search rewrite options, select **Misspelling**  

3. Enter `Frigidaire` in the Corrected Term field 

4. Select `Replace` in the Action dropdown

5. Click the **Save** button  

>The action should immediately take place and a confirmation dialogue box should appear at the top of the screen indicating the rewrite has fired. 

</details>
</br> 

## Phrase Detection

6. Your signals data indicates that customers are having a hard time finding HDMI Adapters within your inventory. You wonder if it's because **the system isn't recognizing the two words go together**. What can you do to ensure the system sees the two words as phrase?

<details>

<summary>Hint</summary> 

- Use the search rewrite Phrase Detection
</details>

<details>

<summary>Solution Steps</summary> 

1. Search `HDMI Adapter` and click the **blue plus icon** to add a rewrite. If you don't immediately see the icon click anywhere outside of the search box, then hover your mouse over the search box.    

2. From the list of search rewrite options, select **Phrase**   

3. Enter the number `2` in the phrase Word Count field  

4. Click the **Save** button  

>The action should immediately take place and a confirmation dialogue box should appear at the top of the screen indicating the rewrite has fired. 

</details>
</br> 

## Head/Tail Analysis 

7. Some of your data is indicating that when customers search 32 GB iPad black w/charger within your inventory, the return results are less than ideal. You want to ensure that **when this term is searched, the query results represent a better performing query of the same or similar products**.  Can you rewrite this so that the returned results represent a better performing query?  

<details>

<summary>Hint</summary> 

- Use the search rewrite Head/Tail

</details>

<details>

<summary>Solution Steps</summary> 

1. Search `32 GB iPad black w/charger` and click the **blue plus icon** to add a rewrite. If you don't immediately see the icon click anywhere outside of the search box, then hover your mouse over the search box.

2. From the list of search rewrite options, select **Head/Tail**  

3. Enter `32 GB iPad` in the Improved Query field  

4. Click the **Save** button  

>The action should immediately take place and a confirmation dialogue box should appear at the top of the screen indicating the rewrite has fired. 

</details>
</br> 

## Rewrites Dashboard

8. Now that you have set up rewrites from the Merchandiser Dashboard, it's time to view them all in a list that you can export or edit. How do we navigate there?

<details>

<summary>Hint</summary> 

- Click on the **Rewrites dashboard** icon

</details>
<br>

9. You realized there's one more rewrite you need to include in your list of edits. Customers on more than one occasion have made the typo *applw* when searching for Apple products. **You want to ensure they are able to view all Apple products even when they accidently spell it wrong**. How can you create a rewrite to make sure the returned results reflect the correctly spelled manufacturer?

<details>

<summary>Hint</summary> 

- Use the search rewrite Misspelling Detection

</details>

<details>

<summary>Solution Steps</summary> 

1. Click the **Misspelling** tab  

2. Click **Add**  

3. Enter in `Applw` in the Misspelling  

4. Enter `Apple` as the suggested Correction  

5. Click the **check** to save this rewrite to your list

</details>

<br>

____

>Congratulations! You have completed the walkthrough of Exploring the Rewrites Manager. Click 'Next' in the lower right corner to continue through the course.
