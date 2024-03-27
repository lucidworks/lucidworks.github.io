---
layout: page
title: Site Search playground
permalink: /playground/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

<!-- NOTES

**To-do**

* Add comments to all stages, existing rules, etc.

**Basic things they can do**

* Examine conflicting rules

**Useful admonitions**

> [!NOTE]  
> Highlights information that users should take into account, even when skimming.

> [!TIP]
> Optional information to help a user be more successful.

> [!IMPORTANT]  
> Crucial information necessary for users to succeed.

> [!WARNING]  
> Critical content demanding immediate user attention due to potential risks.

> [!CAUTION]
> Negative potential consequences of an action.


-->

## About this lab

This lab environment provides a controlled and secure platform to explore and experiment with a pre-configured Fusion application. The application is specifically designed for e-commerce functionalities and is populated with diverse datasets, offering users a rich sandbox for testing and learning.


### Datasources

* **Pages.** Core Lucidworks website content containing informative sections about the Lucidworks' purpose, services, or general information.
* **Blog.** Regularly updated articles or posts covering a broad range of industry-related topics, news, or insights.
* **E-books.** Downloadable publications offering in-depth information or guides on specific industry-related subjects.
* **Events.** Information about gatherings, conferences, workshops, or other occurrences related to our industry, both past, present, and future.
* **Videos.** Visual content covering informative presentations, demonstrations, or discussions on industry-specific topics.


### Tour

<!-- Supademo embed. -->

### What you can do

In this secure application, you have the ability to:

* Create, modify, and delete index and query pipeline stages.
* Work in the Query Workbench. 
* Use the rules editor to create business rules, synonyms, misspelling corrections, and more. 
* Play with Experience Optimizer to curate the ideal search experience.

## Things to try

### Explore the data

Head to the Query Workbench by navigating to **Querying > Query Workbench**.

From here, you can enter a query and view the results. You can also customize the facets in this view.

Try turning stages on and off, then investigate what changed in the results.

### Create signals

In the Query Workbench, you can enable click signals to see how clicking on results affects the document's score (relevancy) and position within the results. 

Click **Format Results**, select the **Send click signals** checkbox, and save your change. If you want to generate many signals at once, select the **Show signals generator** checkbox, and a simulate option appears when hold the pointer over a result. 

### Create business rules

Navigate to **Relevance > Rules**, to reach the rules editor. Make sure you're on the **Rules** screen, then start creating rules by clicking the **Add** button. 

Some examples are already set up for you. 

> [!TIP]
> You can test these rules in Experience Optimizer. View the condition and the action of a rule. Replicate the action in Experience Optimizer, and the action will fire. 

### Create rewrites

Move to the **Rewrites** screen. Explore some of the rewrites that are already set up for you, such as misspelling and synonyms. 

Add new rewrites, modify the existing ones, or delete everything to start over.

### Play with Experience Optimizer

ASDF

### Create your own template

Templates help control the look and feel of Experience Optimizer. 

## Challenges

### Resolve conflicting rules

The rules editor automatically detects rules that may conflict with each other. In the business rules screen, you'll find several. 

Fix the rules to resolve the warnings.

### Create a typeahead template for Experience Optimizer

A good typeahead experience makes searching faster and more efficient for users.

> [!TIP]
> To get a jump start, begin with Experience Optimizer.
> 
> 1. Click the **Start Task** button. 
> 1. Click the search bar. 
> 1. Choose the option to create a new typeahead template.