---
layout: page
title: Site Search playground
permalink: /site-search-playground/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

<!-- NOTES

**To-do**

* Add comments to all stages, existing rules, etc.
* Clean up empty pipeline stages.

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

1. **Pages.** Core Lucidworks website content containing informative sections about the Lucidworks' purpose, services, or general information.
1. **Blog.** Regularly updated articles or posts covering a broad range of industry-related topics, news, or insights.
1. **E-books.** Downloadable publications offering in-depth information or guides on specific industry-related subjects.
1. **Events.** Information about gatherings, conferences, workshops, or other occurrences related to our industry, both past, present, and future.
1. **Videos.** Visual content covering informative presentations, demonstrations, or discussions on industry-specific topics.


### Tour

> [!IMPORTANT]  
> Add a Supademo tour here. 

<!-- Supademo embed. -->

### What you can do

In this secure application, you have the ability to:

* Create, modify, and delete index and query pipeline stages.
* Work in the Query Workbench. 
* Use the rules editor to create business rules, synonyms, misspelling corrections, and more. 
* Play with Experience Optimizer to curate your ideal search experience.

## Things to try

### Explore the data

#### Datasources

Each datasource is set up in a similar way, but there are some key differences. For example, some datasources have unique values declared in **Exclusive regexes**.

> [!NOTE]  
> In many cases, key datasource configurations can be found in the advanced view. Toggle **Advanced** on to view these settings. 

#### Index pipelines

Each datasource is pointed to a unique index pipeline, following a predictable naming pattern. For example, the blog datasource points to an index pipeline called `data-lucidworks-blog`.

Navigate to **Indexing > Index pipelines**, then choose one of the `data-lucidworks-DATA_TYPE` pipelines. 

Note that they all have **Call pipeline** stages called "Intake" and "Outtake." By routing data through these separate, shared index pipelines, Fusion ensures that the data is processed the same at certain phases of indexing. This avoids the need to duplicate work across multiple index pipelines. 

#### Query pipeline

Head to the Query Workbench by navigating to **Querying > Query Workbench**.

From here, you can enter a query and view the results. Try turning stages on and off, then investigate what changed in the results. You can also customize the facets in this view.

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

Now that you've created some business rules and rewrites, navigate to Experience Optimizer to see how to create them from a natural search experience. 

> [!NOTE]  
> Click the **Start task** button, if you want to start curating the search experience. 

Begin by entering a search term in the search box. From the results list, you can choose to block a document from appearing, pin a document in its current position, bury a document lower in the result, or boost a document higher in the result. If you want to pin a document in a specific position, you can drag it where you want it.

Rules are created automatically from your interactions, and they are available to edit, delete, or publish in the **Rules** screen.

To create query rewrites, enter a search term in the search box, and click the **Add** button that appears next to the term. Select any of the query rewrite options to create a new query rewrite. 

Like rules, query rewrites you create in Experience Optimizer are available in the **Rewrites** screen.


### Create your own template

Templates help control the look and feel of Experience Optimizer. 

## Challenges

### Resolve conflicting rules

The rules editor automatically detects rules that may conflict with each other. In the business rules screen, you'll find several. 

Fix the rules to resolve the warnings.

### Start working with tags

Tags are useful for applying rules when for a specific template zone. This advanced option is configured in the Templates screen. 

### Configure triggers for a template



<!-- 

### Create a typeahead template for Experience Optimizer

A good typeahead experience makes searching faster and more efficient for users.

> [!TIP]
> To get a jump start, begin with Experience Optimizer.
> 
> 1. Click the **Start Task** button. 
> 1. Click the search bar. 
> 1. Choose the option to create a new typeahead template.

-->