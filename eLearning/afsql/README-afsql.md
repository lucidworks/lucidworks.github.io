---
layout: page
title: Advanced Readme
permalink: /afsql/
---

<link rel="stylesheet" href="./lib/public/global-training.css">

# Start your environment by clicking **Start Lab** above. 

## The environment should begin to load immediately as indicated by the Vocareum loading symbol. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

When the Fusion Login page displays, login:
   * USERNAME: ```admin```
   * PASSWORD: ```password123```

# In this lab  you will learn how to connect to Jupyter, and explore data in Jupyter. Let's get started!

> Note: You may need to adjust the size of the instructions panel to fully view results in the UI. Toggle the window sizes as needed.

#  Connecting to Jupyter

1. Click **Jupyter** at the top of the screen. Note that a new tab will open with Fusion Jupyter.

This is what you will see after logging in:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Fusion%20SQL%206/SQL_1.png" style="height: 150px; width:600px;"/>

<br>

We will create a new jupyter notebook

2. Click the **New** button in the upper right

3. Select **Python 3** for the notebook type

4. Click **Untitled** (or the name of the notebook) to rename the notebook

5. In the Rename Notebook window, name your notebook: **Fusion_SQL** followed by your first name and last initial

    * Example: Fusion_SQL_John_B
    
A new notebook will now become available

6. For Input, enter: ``%load_ext fusionsql``. Then press Shift + Return on your keyboard

This loads the Fusion SQL interpreter into your notebook

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Fusion%20SQL%206/SQL_2.png" style="height: 250px; width:300px;"/>

<br>

7. Input the following into the notebook. After entering each line, press Enter or Return: 	

    a. ```username="admin"```

    b. ```hostandport="proxy:6764"```

8. Hit Shift + Return

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Fusion%20SQL%206/SQL_3.png" style="height: 250px; width:300px;"/>

<br>

This tells the notebook what host and port to listen to along with the username for login.

9. Input the following into the notebook:

    a. ```import getpass```

    b. ```password=getpass.getpass()```

10. Hit Shift + Enter

This will give you a dialog box to enter your password into.

11. Input the SQL password: ``password123`` and click **Enter**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Fusion%20SQL%206/SQL_4.png" style="height: 300px; width:350px;"/>

<br>

With all our credentials in place, we are now ready to connect to Fusion.

12. Input: ``%fusionsql connect``, then press shift + enter

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Fusion%20SQL%206/SQL_56.png" style="height: 350px; width:450px;"/>

<br>

Note the successful connection message below the line.

# Exploring citibikes Data with Fusion SQL

Now that we are successfully connected to our Fusion instances, we can use Fusion SQL to explore our data

13. Input: ``%fusionsql show tables``

14. Hit: Shift + Enter

This will show all the various tableNames in your Fusion VM

> Note that your table will look different than the image

> Note also that now we are given a response time for our query

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Fusion%20SQL%206/SQL_6.png" style="height: 350px; width:400px;"/>

<br>

15. Input: ```%fusionsql describe citibikes```, then press shift + enter

This command gives a description of the citibikes collection in the form of the associated fields.

> Note that we again are given a response time for our query. In fact, we will be given a query response time for each one we execute.

16. Input: ```%fusionsql select * from citibikes limit 20```, then press shift + enter

We can now see a detailed chart of not only the fields but their values as well

   * Select * indicates we want all field values to appear in our query.

   * From citibikes instructs that we want this data from the citibikes collection.

   * Limit 20 allows us to see the returned values of all fields while only seeing the first 20 documents

17. Input: ```%fusionsql select end_station_name_s, count(*) as cnt from citibikes group by end_station_name_s```, then press shift + enter

With this query we are asking for a total count (*) of all ending stations and we want each end station to have this count grouped together

Had we not indicated that we wanted them grouped together, our query would have returned each end station in the collection singley

18. Input: ```%fusionsql select start_time_dt, trip_duration_s, count(*) as cnt from citibikes group by start_time_dt, trip_duration_s limit 100```, then press shift + enter

    * With this query we are asking for a joining of how long a trip took with when that trip started

    * Here we place a limit of 100 due to the sheer volume of our query

________

If you would like to save your Fusion App to reference later, you can do it now:
1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**

_________

## Great job! If you would like to save your Fusion App to reference later, you can do it now:

1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**

