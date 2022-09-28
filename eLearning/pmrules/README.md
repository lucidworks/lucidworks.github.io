---
layout: page
title: Predictive Merchandiser - Rules Lab
permalink: /pmrules/
---

<link href="lib/public/global-training.css" rel="stylesheet"></link>

## The environment should begin to load immediately as indicated by the Vocareum loading symbol. Please do not click *Start Lab* again. It may take a few mintues for the Fusion environment to fully display.

1. When the Fusion Login page displays, login:
    * USERNAME: **admin**
    * PASSWORD: **password123**

## Using real world scenarios, you will create and manage Rules from the Rules Manager.

You will practice solving everyday problems including: 
- Creating a rule using the Rules Manager. This rule will be broken into three steps, detailing what each column on the Add Rule page represents. 
- Publishing the rule


If you get stuck, we have provided helpful details to keep you moving. 

* **Hints** provide helpful clues regarding the appropriate task to perform.

* **Solution Steps** walk you through step by step instructions, detailing how to complete the task. 

## Rules Dashboard

2. Select the app **Electronics**. 


3. Let's begin creating a new rule. The holiday season is approaching and you need to visit your Rules Dashboard in order to **add a rule for the annual seasonal sale**. Every year, your company pins the most popular items based on trends from top influencers on social media. Let’s get started! What do you click to begin?

<details>

<summary>Solution Steps</summary> 

1.  Click **+Add** in the upper right corner of the Rules Manager
> Note that you may need to adjust the size of your window in order to see all elements of the Rules dashboard.
</details>
<br>

## General Information

4. Let's break this rule down and start with the General column first. Per the company standard, **the rule is always called *Product Group* - Annual Holiday Sale**.  Based on recommendations from the top influencers on social media, the product group just so happens to be **Wireless Headphones**. 

    Additionally, **you’ll want to add the description *Surplus wireless headphones Winter Holiday Sale Nov. - Dec. Four products pinned*** to differentiate the rule from others so that you can easily identify what the rule depicts without clicking into it. Company policy does not require you to fill out any additional fields in the General column of the New Rule page. How can you fill out the general rule information using these details?

<details>

<summary>Hint</summary> 

- Name the rule *Wireless Headphones - Annual Holiday Sale*  

- Enter the rule description of *Surplus wireless headphones Winter Holiday Sale Nov. - Dec. Four products pinned*

</details>

<details>

<summary>Solution Steps</summary> 

1. Enter the rule name `Wireless Headphones - Annual Holiday Sale` in the open text box  

2. Enter the description `Surplus wireless headphones Winter Holiday Sale Nov. - Dec. Four products pinned` in the open text box  

3. Disregard the remainder fields in the general column


</details>
<br>

## Conditions
5. Next, let's look at the Condition column for this rule. In order for this sale to be successful, you know that **whenever a customer searches the keyword Headphones**, that specific products should be pinned to the first four spaces on the Merchandiser Dashboard. Additionally, **this sale runs from November 1st through December 24th** of this year. How can you fill out the rule conditions using this information? 

<details>

<summary>Hint</summary> 

- Condition Types should be set to Query AND Dates  

- Match Query Using should be set to Keywords and Search terms should be set to headphones  

- Dates should reflect Nov. 1 - Dec. 24

</details>

<details>

<summary>Solution Steps</summary> 

1. Use the **drop down** under CONDITION TYPES and check **`Query`** and **`Date`**  

2. If it is not already set, use the dropdown for Match Query and select **`Keyword`**  

3. In the open text box under Search Terms, enter Headphones and click **enter/return** on your keyboard  

4. Click the **Dates** text box  

5. Select **`November 1st`** of this year as the starting date and **`December 24th`** as the ending date

</details>
<br>

## Rule Actions
6. Last, let's visit the Action column. In the Action column, you know that **specifc products will be pinned based on their product IDs**. You have your product IDs ready to pin in the following positions: 
    1. First - 3857133
    2. Second - 3730573
    3. Third - 5414492
    4. Fourth - 4564402  
How can you use these product IDs to fill out the Action column?


<details>

<summary>Hint</summary> 

- Action should be set to Pinned  

- Field Name should be set to id  

- Pinned documents should list the above ID numbers in the order listed  

- Positions for each producd ID should correspond to the number they are listed with above

</details>

<details>

<summary>Solution Steps</summary> 

1. In the ACTION TYPE drop down list, select **Pinned**  

2. Ignore SET RESPONSE VALUES  

3. If it’s not already displayed, type out `id` in FIELD NAME  

4. Click the **+ADD** button next to PINNED DOCUMENTS to add **four** empty fields  

5. Copy and paste each id number listed above into their own respective value box. Type out the respective positions for each value so the list reads:   

    - *`3857133`* position *`1`*

    - *`3730573`* position *`2`*

    - *`5414492`* position *`3`*

    - *`4564402`* position *`4`*
    
6. Click **Save** in the upper right corner to save the rule


</details>
<br>

## Publishing

7. You want this rule to automatically display come November 1st and have approval from your department to make this happen. In order for the rule to take effect once the condition criteria are both met, **you'll need to publish the rule**. How can you do that?

<details>

<summary>Hint</summary> 

- Publish the new rule you have created

</details>

<details>

<summary>Solution Steps</summary> 

1. Hover your mouse over the rule  

2. Click the **Publish Individual Rule** button  

3. Click **Publish** to confirm  

Your page will refresh to indicate the rule has been published. 

</details>

<br>

____

>Congratulations! You have completed the walkthrough of Exploring the Rules Manager. Click 'Next' in the lower right corner to continue through the course.
