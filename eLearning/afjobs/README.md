---
layout: page
title: Jobs and Scheduling
permalink: /afjobs/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

## It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the Jobs and Scheduling Lab! <br> Through this set of lab activities, you will learn how to use clean-up jobs, REST call jobs, and job management.

---
<br>

For this lab, we will once again use our **Online Shoes** app. 

1. On the Fusion launch page, click the **Online_Shoes** app to open it and enter the Fusion workspace.

<br>

## Cleaning up Fusion logs

2. In the left navigation pane, click **Collections**, then select **Collections Manager** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collections.png" style="height: 300px; width:200px;"/>

<br>

The Collections Manager hosts all of the primary and secondary collections that are associated with an app. We are going to focus first on the system collections, which are automatically created for your app. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjobs/afjobs_systemcollections.png"/>
 
<br>

One of the collections to call out here is the **system_logs** collection. This collection captures system actions and information, and has potential to increase in size exponentially in production. 

If you are not using these logs for further log analytics, or you are interested in analysis of only recent logs, it is a good idea to keep the most recent information (or to get rid to these entirely) in order to prevent running into disk space issues. 

For our first activity, let's clean up these logs.

3. In the left navigation pane, click **Collections**, then select **Jobs** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_collections.png" style="height:300px; width:200px;"/>

<br>

4. In the Jobs pane, click **Add+** and begin typing ```log```, then select **Log Cleanup** from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjobs/afjobs_addjob.png" style="height:200px; width:450px;"/>

<br>

5. In the job configuration window, enter the following values:
* In the **ID** field, enter ```LogCleanupSchedule1```.
* In the **Logs Collection** field, enter ```system_logs```.
* In the **Delete Logs older than N days** field, enter ```1```.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjobs/afjobs_addjobdetails.png" style="height: 150px; width:550px;"/>

<br>

6. Click **Save** to create the new **LogCleanupSchedule1** job.

<br>

In the Jobs list, notice that we have not only the **LogCleanupSchedule1** job that we just created, but we can also see one labeled **delete-old-system-logs**.

Let's take a closer look at the **delete-old-system-logs** job. 

7. Click **delete-old-system-logs** to open the job configuration window. 

You can see that this job is nearly identical to the job we just created. Since we don't need to clutter things up with two of them, let's delete this one.

8. Click **Delete job**, then click **Yes, delete** to confirm the action.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjobs/afjobs_deletejob.png"/>

<br>

## REST Call Jobs

For our next exercise, we are going to explore adding a REST call job to our collection.

9. Click **Add+** and begin typing ```REST```, then select **REST Call** from the autosuggestion list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjobs/afjobs_addrestjob.png" style="height:200px; width:450px;"/>

<br>

10. In the job configuration window, enter the following values:
* In the **ID** field, enter ```Message-Clean-up-Schedule1```.
* In the **Endpoint URI** field, enter ```solr://system_message/update```.
* Click the **Call Method** field and select ```post```.

<br>

We have now created a REST Call job that we can use to further clean up our system collections.

11. In the Query Parameters section, click the green plus to add a row, then enter the following values:
* In the **Property Name** field, enter ```wt```.
* In the **Property Value** field, enter ```json```.

12. In the Request Protocol Headers section, copy and paste the following value into the **Request Entity (as string)** field:

```
<root><delete><query>timestamp_dt:[* TO NOW-30DAYS] AND type_s:history</query></delete><commit /></root>
```

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjobs/afjobs_restjobdetails.png" style="height: 350px; width:550px;"/>

<br>

13. Click **Save** to create the REST Call job.

<br>

## Editing jobs

There are multiple ways to manage and schedule your jobs in Fusion. Let's take a minute and look at a few of the options.

Our first scenario is that our system logs collection does not need to be cleaned so often.

14. Click **LogCleanupSchedule1** to open the job's configuration window.

15. In the **Delete Logs older than N days**, change the value to **5**.

16. Click **Save** to save your changes to the job configuration.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjobs/afjobs_logjobchange.png"/>

<br>

Our second scenario is that our system messages collection is taking up too many resources.

17. Click **Message-Clean-up-Schedule1** to open the job's configuration window.

18. In the **Under Request Entitiy (as string)** field, change the value as noted below: 

```
[* TO NOW-30DAYS] to [* TO NOW-15DAYS]
```

19. Click **Save** to save your changes to the job configuration.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjobs/afjobs_restjobchange.png" style="height: 350px; width:550px;"/>

<br>

## Managing jobs

We can use the Scheduler within the Fusion UI to manage jobs.

20. In the left navigation pane, click **System**, then select **Scheduler** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_system.png" style="height:550px; width:200px;"/>

<br>

In this last scenario, the job history collection is eating far too much memory.

21. Click **delete-old-job-history** to open the scheduler configuration window.

22. In the **Crontab Expression** field, change the value as noted below:

```
0 25 4 ? * SUN  to  0 30 3 ? * SUN,TUE,THU *
```

><b>Note:</b> If your <b>delete-old-job-history</b> has never been run, click <b>New Schedule</b>, then choose <b>Cron String</b> from the list and enter the value noted above.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjobs/afjobs_changescheduler.png"/>

<br>

We have changed the schedule of the job from “4:25:00 AM on every Sunday, every month” to “3:30 AM on Sunday, Tuesday, and Wednesday, every month.”

23. Click **Save** to save your changes to the job configuration.

---
<br>

## Great job! You have successfully completed the Jobs and Scheduling Lab, where you have created clean-up jobs and REST call jobs, and should now be more familiar with job management in Fusion. 

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
