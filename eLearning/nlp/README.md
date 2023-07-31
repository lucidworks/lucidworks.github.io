---
layout: page
title: Natural Language Processing
permalink: /nlp/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

# It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Natural Language Processing Lab! <br> Through this set of lab activities, you will learn how to use deploy a spaCy model, create a machine learning job, and add fields to the Query Workbench.

---
<br>

For this lab, we will be using the **Labs** app that has already been configured for our lab environment.

1. On the Fusion launch page, click the **Labs** app to open it and enter the Fusion workspace.

<br>

## Creating Seldon Jobs

Let's begin by creating a Seldon Core job, which will deplay a model into our Fusion cluster. 

2. In the left navigation pane, click **Collections**, then select **Jobs** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collections.png" style="height: 300px; width:200px;"/>

<br>

3. In the Jobs pane, click **Add+** and begin typing ```create seldon```, then select **Create Seldon Core Model Deployment** from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_seldonjobcreate.png"/>

<br>

4. In the job configuration window, enter the following values:
* In the **JOB ID** field, enter ```Labs-spacy```.
* In the **MODEL NAME** field, enter ```spacy```.
* In the **DOCKER REPOSITORY** field, enter ```lucidworks```.
* In the **IMAGE NAME** field, enter ```spacy-seldon:v1.0```.
* In the **OUTPUT COLUMN NAMES FOR MODEL** field enter
```[token_offsets, pos_labels, ner_offsets, ner_labels, lemma_offsets, sentence_offsets]```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_seldonjobdetails.png"/>

<br>

5. Click **Save** to create the new job.

6. Click **Run**, then click **Start** in the job dialog to start the **Labs-spacy** job.

>The job will take a couple minutes to run. Note that the **Running** indicator displays while the job is in process, and will change to **Success** when the job is complete.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/aipbl/aipbl_BBcat_runjob.png"/>

<br>

7. Once the job is complete, click **X** to close the job dialog.

<br>

## Applying Machine Learning

Now that we have created our job, our next step will be to add the machine learning stage that will create new NLP-related fields during data ingestion.

8. In the left navigation pane, click **Indexing**, then select **Index Pipelines** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_indexing.png" style="height: 300px; width:200px;"/>

<br>

9. In the Index Pipelines pane, click **Add+** to open the configuration window.

10. In the **Pipeline ID** field, enter ```labs-spacy```.

11. In the pipeline pane, click **Add a new pipeline stage** and begin typing ```machine```, then select **Machine Learning** from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_pipelinecreate.png"/>

<br>

12. In the Machine Learning window, enter the following values:
* In the **Label** field, enter ```Extract Entities```.
* Click the **Model ID** field and select ```spacy``` from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_pipelinedetails1.png"/>

<br>

13. Click the **Model input transformation script** field to open the script's configuration window.

14. Scroll to line 46 of the code. Cut the ```*/``` value, then paste it in the code before line 42, as shown below:

>This will "comment out" everything before line 42, making it inactive.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_modelinputsnippet1.png"/>

<br>

15. Replace line 44 of the script with the following:

```
modelInput.put("input", doc.getFieldValues("longDescription"))
```

Your Model input transformatio script should now resemble the image below:

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_modelinputsnippet2.png"/>

<br>

16. Once you are finished modifying the model input transformation script, click **X** to close the script window.

17. Click the **Model output transformation script** field to open the script's configuration window.

18. Scroll to line 16 of the code. Cut the ```*/``` value, then paste it in the code before line 14, as shown below:

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_modeloutputsnippet1.png"/>

<br>

19. Remove the existing text after the ```*/```, and replace it with the following code:

>This is how we will create new documents fields that we will observe later in the Query Workbench!

```
doc.addField("ner_labels_ss", modelOutput.get("ner_labels"))<br>
doc.addField("ner_offsets_ss", modelOutput.get("ner_offsets"))<br>
doc.addField("pos_offsets_ss", modelOutput.get("pos_offsets"))<br>
doc.addField("pos_labels_ss", modelOutput.get("pos_labels"))<br>
doc.addField("lemma_offsets_ss", modelOutput.get("lemma_offsets"))<br>
doc.addField("sentence_offsets_ss", modelOutput.get("sentence_offsets"))
```

Your Model output transformaton script should now resemble the image below:

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_modeloutputsnippet2.png"/>

<br>

20. Once you are finished modifying the model output transformation script, click **X** to close the script window.

21. Click **Save** to create the pipeline stage.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_pipelinedetails2.png"/>

<br>

22. Navigate back to the Jobs tab, and click **BestBuy_catalog** to open the job's configuration window.

23. In the **Send to Index Pipeline** field, enter ```labs-spacy```.

24. Click **Save** to save your changes to the **BestBuy_catalog** job. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_BBcatjobedits.png"/>

<br>

Now that everything is set up, it's time to apply the new pipeline configuration and ingest our data.  

25. Click **Run**, then click **Start** in the job dialog to start the **BestBuy_catalog** job.

>This particular job can take up to 15 minutes to run, due to the constraints of the lab environment. Fortunately we only need to wait for 3-5 minutes before we start seeing results.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_BBcatrunjob.png"/>

<br>

26. Once the job is complete, click **X** to close the job dialog.

27. In the left navigaiton pane, click **Querying**, then select **Query Workbench** from the list.

28. In the search results window, click **show fields** under the first document.

<br>

When we scroll down a little, we can now see the fields we added via the Extract Entities stage we added to the index pipeline.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_nerfield.png"/>

<br>

## Reviewing Results 

Finally, let's use add some field facets using these new fields, and review our search results.

29. In the Query Workbench window, click **Add a field facet** and begin typing ```pos```, then select **pos_labels_ss** in the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_posfacet_.png"/>

<br>

This field facet displays the different parts-of-speech labels that are included in the long descriptions of each document in our search results.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_posresults.png"/>

<br>

30. Click **Add a field facet** again, begin typing ```lemma```, then select **lemma_offsets_ss** in the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_lemmafacet.png"/>

<br>

This field facet organizes when and how many times a person, quantity, organization, time (and much more) are mentioned in the long descriptions of each document in our search results.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/nlp/nlp_lemmaresults.png"/>

<br>

Feel free to explore by clicking on the facets to change the search results, adding search queries, or adding and removing field facets as necessary before exiting the lab.

---
<br>

## Great job! You have successfully completed the Natural Language Processing Lab, where you have explored how to use NLP capabilities in Fusion.

<br>

>Make sure to **Save** your open Fusion workspace tabs before exiting the application.

<br>

If you would like to save your Fusion app to import and practice with later, you can do it now:
1. In the left navigation panel, click **Apps**, then choose **Return to Launcher** from the list.
2. Hover over your app until a cog appears in the lower right corner.
3. Click the cog icon.
4. In the pop-up window, click **Export app to zip**.

---
<br>

## Hope to see you in our next course! 
## Thanks and happy learning!