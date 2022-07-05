---
layout: page
title: Jobs and Scheduling
permalink: /afjobs/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

When the Fusion Login page displays, login:
    
* USERNAME: ```admin```
* PASSWORD: ```password123```


# In this lab  you will learn how to use clean-up jobs, REST call jobs, and job management. Let's get started!


> Note: You may need to adjust the size of the instructions panel to fully view results in the UI. Toggle the window sizes as needed.

1. Click on the app **Online_Shoes** to enter the *Fusion workspace*

2. Hover over the Collections icon and click **Collections Manager**

Notice the system_logs collection. This collection has potential to increase in size exponentially in production. 

If you are not using these logs for further log analytics, or you are interested in analysis of only recent logs, it is better to get rid to these to prevent running into disk space issues. 

 <img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Jobs_and_scheduling/systems_logs.png" style="height: 250px; width:550px;"/>
 
 <br>

3. Hover over Collections icon and click **Jobs**

4. Click  **Add+**

5. Begin typing “log” and select **Log Cleanup** from the dropdown

6. In the Log Cleanup window:

    a. ID: **LogCleanupSchedule1**

    b. Logs Collection: **system_logs**

    c. Delete Logs older than N days: **1**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Jobs_and_scheduling/log_cleanup.png" style="height: 150px; width:550px;"/>

<br>

7. Click **Save**

Notice now in the Jobs list that we have not only the LogCleanupSchedule1 job, but another job labeled 
**delete-old-system-logs**

8. Click on **delete-old-system-logs** to take a closer look at this job

Notice that this job is nearly identical to the job we just created. 

9. Click **Delete job**

10. In the window that appears click **Yes, delete**


# REST Call Jobs

11. Hover over Collections icon and click **Jobs**

12. Click  **Add+**

13. Begin typing “REST” and select **REST Call** from the dropdown

14. In the Rest Call window:

    a. ID: ``Message-Clean-up-Schedule1``

    b. Endpoint URI: ``solr://system_message/update``

    c. Call Method: **post**

We are now using a REST Call job to further clean up our Systems Collections.

15. Click **+** under Query Parameters

    a. Property Name: ``wt``

    b. Property Value: ``json``

16. Under Request Protocol Headers: 

    a. Request Entity (as string) 

 **Copy** the string and paste it into the Request Entity

```
    <root><delete><query>timestamp_dt:[* TO NOW-30DAYS] AND type_s:history</query></delete><commit /></root>
```

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Jobs_and_scheduling/rest_call_query_params.png" style="height: 350px; width:550px;"/>

<br>

17. Click **Save**

# Job Management

There are multiple ways to manage and schedule your jobs. We will look at a few.

Our first scenario is that our system logs collection does not need to be cleaned so often.

18. Click on **LogCleanupSchedule1**

19. Delete Logs older than N days: **5**

20. Click **Save**

Our second scenario is that our system messages collection is taking up too many resources.

21. Click on **Message-Clean-up-Schedule1**

22. Under Request Entitiy (as string), change: 

    ```[* TO NOW-30DAYS]``` to ```[* TO NOW-15DAYS]```

23. Click **Save**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Jobs_and_scheduling/message_cleanup.png" style="height: 350px; width:550px;"/>

<br>

We can use the Scheduler within the Fusion UI to manage jobs.

24. Hover over SYSTEM and click: **Scheduler**

In this last scenario, the job history collection is eating far too much memory.

25. Click on **delete-old-job-history**

26. Under Cronbtab Expression, change: 
    ```0 25 4 ? * SUN``` to

	```0 30 3 ? * SUN,TUE,THU *```

27. Click **Save**

We have changed the schedule of the job from “4:25:00 AM on every Sunday, every month” to “3:30 AM on Sunday, Tuesday, and Wednesday, every month.”

## Congratulations! You have successfully created clean-up jobs and REST call jobs, and should now be more familiar with job management.


If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**

