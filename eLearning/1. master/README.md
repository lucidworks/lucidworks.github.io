---
layout: page
title: title of the lab - for example, Experience Optimizer - Templates Lab
permalink: /example link - eotemplate/
---

<link rel="stylesheet" href="./lib/public/global-training.css">

# It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Experience Optimizer Templates Lab! <br> Through this set of lab activities, you will practice creating and managing templates using Experience Optimizer.

---
<br>

Add your content here!! 

## Example formatting - creating header rows:
Use #, ##, or ### to create headings. Each one will have 

## Example formatting - creating a bulleted list: 
* Bullet 1
* Bullet 2

## Example formatting - creating a numbered list:
1. The numbers will automatically go in sequence unless they are separated by unnumbered text. 
2. Number 2
3. Number 3

Unnumbered text
4. To see how this works, try changing the 4 in this row to number 1 (or anything else)

## Example formatting - creating breaks:
To create breaks (spacing between paragraphs, pictures, etc) used bracketed br. See the following example:

Here's my first line of text.

<br>

Here's my second line of text.

## Example formatting - Italics:
*Use single asterisk at each end to markdown something in italics* or <i>Use bracketed i</i>.

## Example formatting - Bold:
**Use double asterisks at each end to markdown something in bold** or <b>Use bracketed b</b>.



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

3. In the left navigation pane, click **Templates** to open the Template Manager.

<br>

## Getting Started

Employees have requested a *Trending Articles* zone on the Search Results page that will allow them to see what documents are the most popular at that time. In order to do this you'll need to edit the template to add a new zone. 

How can you begin?

<details>

<summary>Hint</summary> 

* Add a new Zone to the Search Results template within the landing template category

</details>

<details>

<summary>Solution Steps</summary> 

4.  Expand **landing**

5. Click **Search Results**

6. Click **+ New** in the Zones section. 

</details>
<br>

You want to call this Zone **Trending Articles** so that you can differentiate it from the existing zones in your account. You'd like documents to display as a results list and you need the documents to be pulled from the **sitesearch2** query profile that your search engineers have created for you. 

What steps can you take to begin configuring this zone?

<details>

<summary>Hint</summary> 

* Assign the zone a Display Name, Type, and associate it to a Query Profile. 

</details>

<details>

<summary>Solution Steps</summary> 

7. Enter `Trending Articles` as the DISPLAY NAME

8. Ensure that `Result-List` is selected as the TYPE

9. Click the QUERY PROFILE drop down list and select **sitesearch2** as the associated query profile

10. Click **Next Step** to move to Step 2

</details>
<br>

In order to make this zone stand out from the main results list, you decide to have the results displayed as list of articles. Additionally, You want your display fields to have the article nameX_s, descripion, and image on each grid tile. How will you configure this?

<details>

<summary>Hint</summary> 

* Configure the Results Layout and Display Fields for this zone. 

</details>

<details>

<summary>Solution Steps</summary> 

11. Ensure that `list` is selected as the RESULTS LAYOUT

12. Enter `nameX_s` in the Field Name for the Title Field Display

13. Enter `image` in the Field Name for the Image Field Display

14. Enter `description` in the Field Name for the Description Field Display

15. Click **Save** in the New Zone window.
</details>

<br>

You want Trending Articles to display above the Main Results Zone. 

16. To rearrange the zones, click **the arrows directly next to Trending Articles** and drag the zone above the Main Results Zone. Click **Save**.

<br>

Notice that your template goes into the *Stale* state. You want to preview your template before you publish it to your end users. Where can you do this?

<details>

<summary>Hint</summary> 

- Visit the Optimizer Dashboard

</details>

<details>

<summary>Solution Steps</summary> 

17. Click the **Optimizer** icon see the template in action. 

</details>
<br>

Now that everything looks good, you are ready to publish. 

How can you pulish this template so that your users will see the new zone?

<details>

<summary>Hint</summary> 

* Return to the Templates dashboard to publish. 

</details>

<details>

<summary>Solution Steps</summary> 

18. Click the **Templates** icon.

19. Open the **Search Results** template

20. Click **Publish**, then click **Confirm and Publish**

</details>

<br>

---
<br>

## Great job! You have successfully completed the Experience Optimizer Templates Lab, where you have learned about creating and managing templates using Experience Optimizer.

---
<br>

## Hope to see you in our next course!
## Thanks and happy learning!












