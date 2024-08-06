---
layout: page
title: E-commerce playground
permalink: /e-commerce-playground/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

## About this playground

This playground environment provides a controlled and secure platform to explore and experiment with a pre-configured Fusion application. The application is specifically designed for e-commerce functionalities, including an expansive data source of electronics products and accessories and a library of query rewrites. 

### Datasources

There is one data source in the e-commerce playground: **Electronics**. The data source contains over 40,000 products, from televisions to printers, speakers, and home appliances. 

### What you can do

In this secure application, you have the ability to:

* Create, modify, and delete index and query pipeline stages.
* Work in the Query Workbench. 
* Use the rules editor to create business rules, synonyms, misspelling corrections, and more. 
* Play with Predictive Merchandiser to curate your ideal search experience.

## Things to try

### Explore the data

#### Index pipelines

The index pipeline in this playground is a very basic configuration. There are only three pipeline stages, but Fusion is able to map the data to a useful format for query purposes.

Navigate to **Indexing > Index workbench**. Then, load the **electronics** data source. 

Try adding some index pipeline stages to manipulate the fields and values in the documents before they are sent to Solr. Here are a couple of stages to try:

* **Field Mapping**. The field mapping stage is a powerful stage commonly used to delete, add, set, copy, or move fields on a document. It allows you to perform small or bulk operations, such as deleting all unmapped fields.
* **Regex Field Extraction**. The RegEx field extraction stage is used to pull out information from one field and place it in another. For example, if you have a field with the minimum and maximum temperatures stored in one string, but you wanted to separate the values, you can use this field to do so. 

> The final stage in the index pipeline, **Solr Indexer** is crucial for getting documents to Solr. Turning it off, moving it, or removing it may break the pipeline.
{:.important}


#### Query pipeline

Head to the Query Workbench by navigating to **Querying > Query Workbench**.

From here, you can enter a query and view the results. Try turning stages on and off, then investigate what changed in the results. You can also customize the facets in this view. 

> This query pipeline makes use of facet fields and range facet fields. A range facet is already created for the regular price. Try creating a range facet for the sales price, `salePrice_d`. 
{:.tip}

### Create signals

In the Query Workbench, you can enable click signals to see how clicking on results affects the document's score (relevancy) and position within the results. 

Click **Format Results**, select the **Send click signals** checkbox, and save your change. If you want to generate many signals at once, select the **Show signals generator** checkbox, and a simulate option appears when hold the pointer over a result.

![Send click signals in Query Workbench](../../static/images/qwb-send-signals.png "Send click signals in Query Workbench")

### Compare results before you save changes

You can click the **Compare** button to compare the results list before and after a change. Try boosting a result:

1. Enter a query term in the query work bench.
1. Navigate to the second page of results, and choose one of the results. 
1. Click the **Boost** button. The result is boosted to the first page. 

To keep the boost, save the query pipeline. To discard the boost, close the query workbench, and choose not to save. 


### Create business rules

Navigate to **Relevance > Rules**, to reach the rules editor. Make sure you're on the **Rules** screen, then start creating rules by clicking the **Add** button. 

Some examples are already set up for you. 

> You can test these rules in Predictive Merchandiser. View the condition and the action of a rule. Replicate the action in Predictive Merchandiser, and the action will fire. 
{:.tip}

### Create rewrites

Move to the **Rewrites** screen. Explore some of the rewrites that are already set up for you, such as misspelling and synonyms. 

Add new rewrites, modify the existing ones, or delete everything to start over.

### Play with Predictive Merchandiser

Now that you've created some business rules and rewrites, navigate to Predictive Merchandiser to see how to create them from a natural search experience. 

 
> Click the **Start task** button, if you want to start curating the search experience. 
{:.tip}

Begin by entering a search term in the search box. From the results list, you can choose to block a document from appearing, pin a document in its current position, bury a document lower in the result, or boost a document higher in the result. If you want to pin a document in a specific position, you can drag it where you want it.

<div style="position: relative; padding-bottom: calc(51.78125% + 42px); height: 0;"><iframe src="https://app.supademo.com/embed/ft9Rms9EBaqQFnduqRt5P" allow="clipboard-write" frameborder="0" webkitallowfullscreen="true" mozallowfullscreen="true" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

Rules are created automatically from your interactions, and they are available to edit, delete, or publish in the **Rules** screen.

To create query rewrites, enter a search term in the search box, and click the **Add** button that appears next to the term. Select any of the query rewrite options to create a new query rewrite. 

<div style="position: relative; padding-bottom: calc(51.78125% + 42px); height: 0;"><iframe src="https://app.supademo.com/embed/V82C_bR_syCuDPuK48-PB" allow="clipboard-write" frameborder="0" webkitallowfullscreen="true" mozallowfullscreen="true" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

Like rules, query rewrites you create in Predictive Merchandiser are available in the **Rewrites** screen.

## Challenges

These challenges are meant to be open-ended. How you solve the challenge is entirely up to you. If you're stuck, check the [Lucidworks documentation](https://doc.lucidworks.com/). 

### Create your own landing template

Templates help control the look and feel of Predictive Merchandiser, allowing you to design, test, and implement a wide variety of search experiences.

In Predictive Merchandiser, you can create a custom landing template popular with new or existing zones. 

### Configure triggers for a template

You can trigger a template in Predictive Merchandiser based on conditions such as a time range, specific searches, or the URL context. If the required conditions are met, the template will load instead of the default, giving you fine-tuned control over the zone setup and layout. 

### Start working with tags

Tags are useful for applying rules when for a specific template zone. This advanced option is configured in the Templates screen. Learn how to incorporate tags in your application. 

## What's next?

The site search playground is designed for you to continue exploring. Try building new functionalities, delve into the data flow within Fusion, and see how you can craft the perfect search experience. 

If you're ready to move on, we recommend the following resources: 

* [Fusion Signals](https://academy.lucidworks.com/advanced-signals)
* [Predictive Merchandiser learning path](https://academy.lucidworks.com/path/predictive-merchandiser-learning-path)
* [Refining Search Results learning path](https://academy.lucidworks.com/path/refining-search-results)
* [Lucidworks documentation](https://doc.lucidworks.com/)