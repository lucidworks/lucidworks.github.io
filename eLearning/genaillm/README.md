---
layout: page
title: LLM Lab (in-dev)
permalink: /genaillm/
---



> ## ⚠️ About the Fusion lab environment
> 
> While the environment is loading, do not click **Start Lab** again. It may take a few minutes for the Fusion environment to appear.
>  
> When the Fusion login page appears, use the following provided username and password.


## Lab instructions
  
In this lab, you will be exploring how you can use Fusion together with Large Language Models (LLM).
 
1. From the app launcher, click on the app **lab-genai**.
2. Hold the pointer over over the **Querying** menu, then select **Query Workbench**.

    We will be exploring some of the query pipelines that are shown on the left.

    **ChatGPT - [Initialize]** stage

3. **Click on the ChatGPT - [Initialize]** stage.
4. Click into the script body. The script has two sections that we will look at, which are notated with JavaScript comments which start with `//`.


5. Take a look at the *Set initial values and store in context object* code section. This is where we provide the API key for your chosen LLM provider.
 
    > ## ⚠️ Note
    > The API key is not genuine, due to security constraints.

6. Look at the *Get API Key stored in Fusion configuration settings* stage. Here we are retrieving the Fusion API key. We can then initialize the connection between Fusion and our LLM in the next stage.
 
    **ChatGPT - [Prompt] Destination Locations** stage
 
7. Click on the **ChatGPT - [Prompt] Destination Locations** stage.
 
    This stage allows Fusion and our LLM to actively communicate with each other. We will focus on a couple of sections of this code.
 
    Note that this stage is not currently operational without valid API keys.

 
8. The first major piece here is to validate the API key as seen in the *API key validation* section of the code.


9.  Next, we will take a closer look at a couple of sections of **Build REST call for ChatGTP**.


    > ## ⚠️ Note
    > This stage is only necessary because we are not using a real LLM API key. As such, this type of stage would not be used out in the wild and is strictly used for this lab environment. We will not need to dive into this stage further.
 
    * The *Prompt instructions code* section is where we limit our results being returned from the LLM. In this case, we are only interested in city locations, destinations, and activities and we only want results from within the United States.
    * The next sections in the code are in a standard REST call layout: define the JSON body, give header options, execute the call, get a response, and parse it in your desired format.
 
    ChatGPT - [Mock Prompt] Destination Locations
 
    **Lucidworks - NER - Map to Entities** and **Lucidworks - NER - Boost Entities** stages
 
1.  Click on the **Lucidworks - NER - Map to Entities** stage.
 
    * Look at the Tagger Collection. It is pointing at _lab-genai_query_rewrite_staging_ collection. We will look at this collection in a moment.
    * Scroll down and look under Additional Params to be Included in the Text Tagger Request. Notice that we have a filter query (`fq`) on the ner2 tag.
 
1.  Hover over the collections dropdown, then select the _lab-genai_query_rewrite_staging_ collection. If you are prompted to save your changes, do not save.

 
1.  Hover over the **Querying** menu, then select **Query Workbench**. The results shown are our named entities derived from the `state_s` field.

 
2.  Click **Show fields** on any of the results.
 
    * You can see the output and the `surface_form` being associated with the various states.
    * Additionally, you can see the ner2 tag that is being used in the query pipeline.

 
14. The first of these NER stages maps our entities while the second stage applies some boosting to these mapped entities.


15. Click on the **Lucidworks - NER - Boost Entities** stage. You can see various instructions for how to boost results here:
    * // First part matches both.
    * // Second part matches both.
    * // Modify to include "OR" operator if multiple fields of the same type.
    * // Add fq with "OR" operator.

 
## Queries Examples
 
Before proceeding make sure that the **ChatGPT - [Mock Prompt] Destination Locations** stage is turned off.

