---
layout: page
title: Natural Language Processing
permalink: /nlp/
---

<link rel="stylesheet" href="./lib/public/global-training.css">

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

When the Fusion Login page displays, login: <br>
    * USERNAME: ```admin```
    <br>
    * PASSWORD: ```password123```


# Welcome to the Natural Language Processing Lab. In this lab  you will learn how to use deploy a spaCy model, create a machine learning job, and add fields to the Query Workbench. Let's get started!


> Note: You may need to adjust the size of the instructions panel to fully view results in the UI. Toggle the window sizes as needed.

1. Click on the app **Labs** to enter the *Fusion workspace*

2. Hover over the COLLECTIONS icon and click **Jobs**

3. Click  **Add+**

4. Begin typing “create seldon” and select **Create Seldon Core Model Deployment** from the dropdown

5. In the Create Seldon Core Model Deployment window enter the following info for the fields shown below:

    a. JOB ID: ```Labs-spacy```

    b. MODEL NAME: ```spacy```

    c. DOCKER REPOSITORY: ```lucidworks```

    d. IMAGE NAME: ```spacy-seldon:v1.0```

    e. OUTPUT COLUMN NAMES FOR MODEL: <br>
    ```[token_offsets, pos_labels, ner_offsets, ner_labels, lemma_offsets, sentence_offsets]```

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/NLP/1_5.png" style="height: 272px; width:600px;"/>

<br>

6. Click **Save**

7. Click **Run**, then click **Start**

>Note: Success! The job will take about a minute, when it's done, the "running" icon will change to a "sunshine". 

8. Click **Save** in the Run Job window

9. Hover over the INDEXING icon and click **Index Pipelines**

10. Click the **Add+** button

11. For **Pipeline ID**, enter ```labs-spacy```

12. Click **Add a new pipeline stage**

13. Begin typing "machine" and select **Machine Learning** from the dropdown

14. In the Machine Learning window enter the following info for the fields shown below:

    a. Label: ```Extract Entities```

    b. Model ID: select **spacy** from the dropdown

15. Click into the field for **Model input transformation script**

16. Scroll to line 46 of the code. Cut and paste the ```*/``` before line 42, as shown below:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/NLP/2_6.png" style="height: 85px; width:600px;"/>

<br>

>Note: This will "comment out" everything before line 15, making it inactive

17. Replace line 44 of the script with the following:


`modelInput.put("input", doc.getFieldValues("longDescription"))`


Your script should resemble the image below:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/NLP/2_7.png" style="height: 569px; width:600px;"/>

<br>

18. Once you are finished modifying the script, close the script window

19. Returning to the Machine Learning window, click into the field for **Model output transformation script**

20. Scroll to line 16 of the code. Cut and paste the ```*/``` before line 14, as shown below:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/NLP/3.png" style="height: 126px; width:600px;"/>

<br>

21. Remove the existing text after the ```*/```, and replace it with the following code:


`doc.addField("ner_labels_ss", modelOutput.get("ner_labels"))
doc.addField("ner_offsets_ss", modelOutput.get("ner_offsets"))
doc.addField("pos_offsets_ss", modelOutput.get("pos_offsets"))
doc.addField("pos_labels_ss", modelOutput.get("pos_labels"))
doc.addField("lemma_offsets_ss", modelOutput.get("lemma_offsets"))
doc.addField("sentence_offsets_ss", modelOutput.get("sentence_offsets"))`

<br>

>Note: This is how we will create new fields to appear in the Query Workbench!

<br>

22. Your Model output transformaton script should now resemble the following:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/NLP/4_5.png" style="height: 313px; width:600px;"/>

<br>

23. Once you are finished modifying the script, close the script window

24. Click the **Save** button in the upper right corner of the Machine Learning Pipeline window

25. Hover over the COLLECTIONS icon and click **Jobs**

26. Click the job **BestBuy_catalog**

27. Under the READ OPTIONS section, in the SEND TO INDEX PIPELINE field, enter ```labs-spacy```

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/NLP/5.png" style="height: 337px; width:600px;"/>

<br>

28. Click the **Save** button. Then, click **Run**, and **Start**. 

    a. *Note that this could take up to 5 minutes to completely run.* Once the job status indicates success, click **Save**

29. Hover over QUERYING and click **Query Workbench**

30. Under the first result, click **show fields**

31. When we scroll down a little, we can now see the fields we added in the Index Pipeline

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/NLP/6.png" style="height: 300px; width:600px;"/>

<br>

Now, let's add some field facets using our new fields

32. In the Query Workbench window, click **Add a field facet**

33. Begin typing "pos" and select **pos_labels_ss**

The field facet then shows the different parts-of-speech labels that are in the long descriptions of each product

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/NLP/7.png" style="height: 403px; width:256px;"/>

<br>

34. Click **Add a field facet** again, and begin typing "lemma". Select **lemma_offsets_ss**

This field facet organizes when, and how many times, a person, quantity, organization, time (and much more) are mentioned in the long descriptions of each product

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/NLP/8.png" style="height: 278px; width:250px;"/>


Make sure to **Save** your open Fusion Workspace tabs!

________
Great job! You have successfully explored how to use NLP capabilities in Fusion! If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**

>Click **Next** in the lower right corner of the screen to continue on in the course
