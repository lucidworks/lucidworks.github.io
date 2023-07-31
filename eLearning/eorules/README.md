---
layout: page
title: Experience Optimizer - Rules Lab
permalink: /eorules/
---

<link rel="stylesheet" href="./lib/public/global-training.css">

# It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Experience Optimizer Rules Lab! <br> Through this set of lab activities, you will practice creating and managing rules using Experience Optimizer.

---
<br>

In this lab, you will be following a real scenario to: 
* Create a rule (broken down into three steps, which will focus on the columns and the information they contain).
* Publish a rule.

<br>

Different from our other labs, we encourage you to try the exercise first, then check to see how you did. If you get stuck, we have provided the following to keep you moving:
* **Hints** provide helpful clues regarding the appropriate task to perform.
* **Solution Steps** walk you through step by step instructions, detailing how to complete the task. 

---
<br>

For this lab, we will be selecting the **Electronics** app that has already been configured for our lab environment. We are going to start by opening the app in Fusion, then navigating to the **Rules Manager** dashboard.

1. On the Fusion launch page, click the **Electronics** app to open it and enter the Fusion workspace. 

2. In the left navigation pane, click **Relevance**, then select **Rules** from the list.

>Clicking **Rules** will open the **Rules Manager** in a new tab in your browser. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_relevance.png" style="height: 300px; width:170px;"/>

<br>

## Creating Rules

Our first exercise will be creating a new rule using the following scenario:

Forrester has just released their 2023 ranking reports, and you want to highlight your organization's ratings. You need to visit your Rules Manager Dashboard to **add a rule for the first quarter**. 

Where do you click to begin?

<details>

<summary>Solution Steps</summary> 

3. In the Rules Manager window, click **Add** to add a new rule.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorules/eorules_addrule.png"/>

</details>
<br>

## Rule General Information

Now that we have the shell started, let's break it down and start with the General column first.

Per our organization's naming conventions, **the rule is always called Forrester - Annual Rankings Release**. To differentiate it from previous rules, you will want to **add the description Forrester Predictions 2023 reports** so that you can easily identify what the rule depicts without clicking into it.

How would you fill out the general rule information using these details?

<details>

<summary>Hint</summary> 

* Name the rule *Forrester - Annual Rankings Release*.  

* Enter the rule description of *Forrester Predictions 2023 reports*.

</details>

<details>

<summary>Solution Steps</summary> 

4. In the General section, enter the following values:
* In the **Name** field, enter ```Forrester - Annual Rankings Release```. 
* In the **Description** field, enter ```Forrester Predictions 2023 reports```.
* Leave the remaining fields blank.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorules/eorules_general.png"/>

</details>
<br>

## Rule Conditions

Next, let's look at the Condition column for this rule. 

In order for this release to be successful, you know that **whenever a user searches the keyword Forrester**, specific documents should be pinned to the first four spaces on the Optimizer Dashboard. 

Additionally, **the highlights run from February 1st through April 30th** of this year. 

How would you fill out the rule conditions using this information? 

<details>

<summary>Hint</summary> 

* Condition Types should be set to Query AND Dates.  

* Match Query Using should be set to Keywords, and Search terms should be set to Forrester.  

* Dates should reflect Feb. 1 - Apr. 30.

</details>

<details>

<summary>Solution Steps</summary> 

5. In the **Condition Types** field, click the dropdown arrow and select both the ```Query``` and ```Date``` options.  

6. Click in the **Dates** field and select the following values:
* For the beginning date, select ```February 1``` of this year, and the starting time of ```12:00```.
* For the ending date, select ```April 30```  of this year, and the starting time of ```12:00```.

7. In the **Match Query Using** field, click the dropdown arrow and select the ```Keywords``` option (if it is not already selected).  

8. In the **Search Terms** field, enter ```Forrester```, then click outside of the field box to add the term.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorules/eorules_condition.png"/>

</details>
<br>

## Rule Actions

Last, let's visit the Action column. 

In the Action column, you know that **specifc documents will be pinned based on their URLs**. 

You have your documents ready to pin in the following positions: <br>
1. https://lucidworks.com/ebooks/predictions-2023-banking-knowledge-management/ <br>
2. https://lucidworks.com/ebooks/forrester-predictions-2023-software/ <br>
3. https://lucidworks.com/ebooks/predictions-2023-commerce-platform/ <br>
4. https://lucidworks.com/ebooks/forrester-predictions-2023-insurance/

How would you use this information to fill out the Action column?

<details>

<summary>Hint</summary> 

* Action should be set to Pinned.  

* Field Name should be set to urlX.  

* Pinned documents should list the above URLs in the order listed.  

* Positions for each document should correspond to the number they are listed with above.

</details>

<details>

<summary>Solution Steps</summary> 

9. In the **Action Type** field, click the dropdown arrow and select **Pinned** from the list.  

10. Leave the **Set Response Values** field empty.  

11. In the **Field Name** field, enter ```urlX```.  

12. In the Pinned Documents section, click **+ADD** four times to generate four **Value** fields.  

13. For each of the **Value** fields, enter each value and position number as listed:
* `https://lucidworks.com/ebooks/predictions-2023-banking-knowledge-management/` with position `1`.
* `https://lucidworks.com/ebooks/forrester-predictions-2023-software/` with position `2`.
* `https://lucidworks.com/ebooks/predictions-2023-commerce-platform/` with position `3`.
* `https://lucidworks.com/ebooks/forrester-predictions-2023-insurance/` with position `4`.

14. Click **Save** to create the new rule.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorules/eorules_action.png"/>

</details>
<br>

## Publishing

You want this rule to automatically display starting  February 1st, and already have approval from your department to make this happen. 

In order for the rule to take effect once the condition criteria are both met, **you'll need to publish the rule**. 

How can you do that?

<details>

<summary>Hint</summary> 

* Publish the new rule you have created.

</details>

<details>

<summary>Solution Steps</summary> 

15. Hover your mouse over the **Published** column for the new rule.  

16. Click **Publish Individual Rule**.  

17. In the Publish dialog, click **Publish** to confirm the action.  

Your page will refresh to indicate the rule has been published. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/eorules/eorules_publish.png"/>

</details>
<br>

---
<br>

## Great job! You have successfully completed the Experience Optimizer Rules Lab, where you have learned how to manually create and manage business rules using Experience Optimizer.

---
<br>

## Hope to see you in our next course!
## Thanks and happy learning!
