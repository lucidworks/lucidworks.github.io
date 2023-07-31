---
layout: page
title: Javascript in Fusion
permalink: /afjava/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

## It may take a few minutes to fully load and display the Fusion environment. Please do not click *Start lab* again. 
<br>

>When the Fusion Login page displays, login:
>* USERNAME: ```admin```
>* PASSWORD: ```password123```

<br>

## Welcome to the JavaScript Lab! <br> Through this set of lab activities you will learn how to modify a document via REST Call, as well as authenticate a REST call. 

---
<br>

Let's get started by creating a new app in Fusion, and getting our datasource set up.

1. From the Fusion launch page, click **Create new app**.

2. In the **App Name** field, enter the name ```JS Labs```.

3. *(Optional)* Enter an **App Description** and select an **App tile color**.

4. Click **Create App**,

5. Once it has been created, click the **JS Labs** app to open it and enter the Fusion workspace.

6. In the left navigation pane, click **Indexing**, then select **Datasources** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_indexing.png" style="height: 300px; width:200px;">

<br>

7. Click: **Add+** and select **Web** from the list.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_jslabsdatasource.png"/>

<br>

8. Enter the following datasource values:
* In the **Datasource ID** field, enter ```Lucidworks_website```.
* Click the **Pipeline ID** field and select ```JS_Labs```.
* Click the **Parser** field and select ```JS_Labs```.

9. In the Start Link section, click **Add**, then enter ```https://lucidworks.com```.

10. Click to expand **Limit Documents** and enter the following values:
* In the **Max Crawl Depth** field, enter ```1```.
* In the **Max Items** field, enter ```10```.

><b>Note:</b> These values are intentionally small, to ensure that our indexing job will only take a small sample of the available data.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_jlabsdatasourcessetup.png"/>

<br>

11. Click **Save** to create the datasource.

<br>

Now we need to run a job in order to ingest the data into Fusion.

12. Click **Run**, then click **Start** in the job dialog to start the job.

>The job will take about 2 minutes to run. Note that the **Running** indicator displays while the job is in process, and will change to **Success** when the job is complete.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_datasourcejob.png"/>

<br>

13. Once the job is complete, click **Save**, then click the **X** to close the job dialog.

<br>

## Modifying a Document via REST Call

For this exercise, we will set up a pipeline stage that instantiates an HTTP client, accesses a URL, and uses data from that URL to modify the pipeline document.

14. In the left navigation pane, click **Indexing**, then select **Index Pipelines** from the list. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/navigation/nav_indexing.png" style="height: 300px; width:200px;">

<br>

15. In the Existing Pipelines pane, select **JS_Labs** to open the configuration window.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_jslabspipeline.png"/>

<br>
    
16. Click **Add a new pipeline stage** and begin typing ```java```, then select **JavaScript** from the list.

><b>Note:</b> For this lab we are creating a custom JavaScript stage, where we will be pasting our script directly in the stage setup. You will notice there is also a Managed JavaScript option, which uses a script from the blob store. <br><br> For more information on the differences, please see our Fusion documentation site. 

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_customjavascript.png"/>

<br>

17. In the **Label** field, enter ```REST Call```.

<br>

Now that we have created the shell for the stage, it's time to add in the script.

We will be putting together the script over multiple steps, to highlight the different actions being performed as part of the script. 

Let's begin by adding the function script, which contains a try-catch block that will help us identify any exceptions or errors with our code.

18. In the **Script Body** field, delete the default script and replace it with the following code snippet:

```
function(doc){
  var e = java.lang.Exception;
  try{  
  }catch(e){
    logger.error(e.getLocalizedMessage());
  }
  return  doc;
}
```

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_scriptex1.png" style="height: 350px; width:500px;"/>

<br>

Next, we will add the variable definitions, which includes an action to set up an HTTP client.

19. In the **Script Body** field, add the following code snippet <u>above</u> the **try clause** declaration:

```
var BufferedReader = java.io.BufferedReader;
  var InputStreamReader = java.io.InputStreamReader;
  var HttpResponse = org.apache.http.HttpResponse;
  var HttpClient = org.apache.http.client.HttpClient;
  var HttpGet = org.apache.http.client.methods.HttpGet;
  var StringBuffer = java.lang.StringBuffer;
  var String = java.lang.String;
  var userAgent = org.apache.http.HttpHeaders.USER_AGENT;
  var HttpClientBuilder = org.apache.http.impl.client.HttpClientBuilder;
```

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_scriptex2.png" style="height: 430px; width:500px;"/>

<br>

Now we will add an action to execute a REST request.

20. In the **String Body** field, add the following code snippet <u>within</u> the **try clause** declaration:

```
 var client = HttpClientBuilder.create().build();
 var url = new String("http://www.google.com/search?q=httpClient");
 var request = new HttpGet(url);
 request.addHeader("User-Agent", userAgent);
```

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_scriptex3.png" style="height: 350px; width:500px;"/>

<br>

><b>Note:</b> The URL we are fetching is not very interesting, nor is it related to the Lucidworks.com site that the documents are coming from. We are using it in this exercise to illustrate how such a request can be made.

<br>

Next, let's add an action for the stage to execute the REST call and construct a response object to parse.

21. In the **Script Body** field, add the following code snippet to the <u>end</u> of the **try clause** declaration:

```
var response = client.execute(request);
 var rd = new BufferedReader(new InputStreamReader(response.getEntity().getContent()));
 var result = new StringBuffer();
 var line = "";
 while ((line = rd.readLine()) !== null) {
   result.append(line);
 } 
```

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_scriptex4.png" style="height: 430px; width:500px;"/>

<br>

For our last step, let's add add an action for the stage to parse the response using Jsoup, fetch the URL’s title, and attach that title to the document via the **sub_title** field.

22. In the **Script Body** field, add the following code snippet to the <u>end</U> of the **try clause** declaration:

```
var Jsoup = org.jsoup.Jsoup;
 var httpDoc = Jsoup.parse(result);
 var httpTitle = httpDoc.select("title").first();
 doc.addField("sub_title", httpTitle);
```
<br>

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_scriptex5.png" style="height: 430px; width:500px;"/>

<br>

23. Click **X** to close the Script Body editor, then click **Save** to save your changes to the REST Call pipeline stage.

<br>

Now that we have added the new pipeline stage, let's re-ingest our data and observe the difference.

24. Navigate to the Datasource tab and open the **Lucidworks_website** datasource.

25.  Click **Clear Datasource**, then click **Yes, clear** to confirm the action.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_cleardatasource.png"/>

<br>

26.  Click **Run**, then click **Start** to start the indexing job. 

27. Once the job is complete, click **X** to close the job dialog.

<br>

Now that our job is complete, let's go review our search results.

28. In the left navigation pane, click **Querying**, then select **Query Workbench** from the list.

In our results, we can see a total of 10 (or less) documents returned in the search. If you return to the Datasources tab and look at the Lucidworks_website datasource's **Job History**, you will see that its last successful run took ~10 seconds.  This is relatively slow, given that the search only produces a few documents.  The reason for this is that setting up and using an HTTP Client is not very fast.  

Since the client we set up and the URL we fetch are the same every time, we can instead make this stage stateful.  It will execute the client setup and REST call once, save the result, and use that saved result every time the stage runs.

<br>

For the next part of our exercise, we will do this by adding some additional code snippets to our script being executed.
<br>

29. Navigate back to the **Index Pipelines** tab and open the **REST Call** pipeline stage.

30. In the **Script Body** field, add the following code snippet <u>above</u> the **try clause** declaration:

```
var System = java.lang.System;
```

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_scriptex6.png" style="height: 350px; width:500px;"/>

<br>

Next, we are going to add an action that saves ```httpTitle``` as a Java system property, so that it persists between starts and stops of this stage.

31. In the **Script Body** field, add the following code snippet <u>before</u> the **doc.addField** line:

```
System.setProperty("page_sub_title", httpTitle);
```

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_scriptex7.png" style="height: 350px; width:500px;"/>

<br>

Now that we have made the httpTitle persistent, we need to add a conditional to the function so that the HTTP Client will only be created if the target system property is empty.  Otherwise, the function should fetch the system property and skip the client creation and REST call execution.

32. In the **Script Body** field, add the following code snippet <u>within</u> the **try clause** declaration:

```
var httpTitle = "";
  if(System.getProperty("page_sub_title") == null){
```

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_scriptex8.png" style="height: 350px; width:500px;"/>

<br>

33. In the **Script Body** field, add the following code snippet <u>above</u> the **doc.addField** line:

```
 } else {
   httpTitle = System.getProperty("page_sub_title");
 }
```

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_scriptex9.png" style="height: 350px; width:500px;"/>

<br>

34. Click **X** to close the Script Body editor, then click **Save** to save your changes to the REST Call pipeline stage.

<br>

Let's re-ingest our data and review our new results.

35. Navigate to the Datasources tab.

36.  Click **Clear Datasource**, then click **Yes, clear** to confirm the action.

37.  Click **Run**, then click **Start** to start the indexing job. 

38. Once the job is complete, click **X** to close the job dialog, then click **Job History** to open the job history dialog.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_jobhistory.png"/>

<br>

Notice with our pipeline stage changes, the job now only takes 3-5 seconds to run. While this is not significant when we call this small number of documents, it is considerable when calling volumes of data.

>If you feel your code is not working, you can copy the full codes for the **REST Call** pipeline stage below, then paste it into the script body field.

<br>

<details>

<summary>Click the arrow to view the full script body for the REST Call pipeline stage.</summary> 

```
function(doc){
  var e = java.lang.Exception;

  var BufferedReader = java.io.BufferedReader;
  var InputStreamReader = java.io.InputStreamReader;
  var HttpResponse = org.apache.http.HttpResponse;
  var HttpClient = org.apache.http.client.HttpClient;
  var HttpGet = org.apache.http.client.methods.HttpGet;
  var StringBuffer = java.lang.StringBuffer;
  var String = java.lang.String;
  var userAgent = org.apache.http.HttpHeaders.USER_AGENT;
  var HttpClientBuilder = org.apache.http.impl.client.HttpClientBuilder;

  var System = java.lang.System;

  try{  
    var httpTitle = "";

    if(System.getProperty("page_sub_title") == null){ 
      var client = HttpClientBuilder.create().build();

      var url = new String("http://www.google.com/search?q=httpClient");
      var request = new HttpGet(url);
      request.addHeader("User-Agent", userAgent);

      var response = client.execute(request);

      var rd = new BufferedReader(new InputStreamReader(response.getEntity().getContent()));
      var result = new StringBuffer();
      var line = "";

      while ((line = rd.readLine()) !== null) {
        result.append(line);
      }

      var Jsoup = org.jsoup.Jsoup;
      var httpDoc = Jsoup.parse(result);
      var httpTitle = httpDoc.select("title").first();

      System.setProperty("page_sub_title", httpTitle);

    } else {
      httpTitle = System.getProperty("page_sub_title");
    }

    doc.addField("sub_title", httpTitle);
    
  }catch(e){
    logger.error(e.getLocalizedMessage());
  }

  return  doc;
}
```

</details>

<br>

## Authenticating a REST Call

In the last activity, we set up a JavaScript stage that modified a document with information from a REST call.  But what do we do if the endpoint requires authentication?  

Let's explore authenticating a REST call. In this case, we will use Fusion as our target endpoint, using the admin password you’ve already created.

39. Navigate to **Index Pipelines** tab. 

40. In the Existing Pipelines pane, select **JS_Labs** to open the configuration window.
  
41. Click **Add a new pipeline stage** and begin typing ```java```, then select **JavaScript** from the list. 

42. In the **Label** field, enter **Authenticated Call**.

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_authcall.png"/>

<br>

43. In the **Script Body** field, delete the default script and replace it with the following code snippet:

```
function(doc){
var e = java.lang.Exception;
  try {
  } catch (e) {
    logger.error("Error getting httpclient " + e.getLocalizedMessage());
  }
  return  doc;
}
```

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_scriptex10.png" style="height: 350px; width: 500px;"/>

<br>
Next, let's add our class declarations.

44. In the **Script Body** field, add the following code snippet <u>below</u> the **function(doc)** line:

```
  var UsernamePasswordCredentials = org.apache.http.auth.UsernamePasswordCredentials;
  var AuthScope = org.apache.http.auth.AuthScope;
  var BasicCredentialsProvider = org.apache.http.impl.client.BasicCredentialsProvider;
  var HttpClientBuilder = org.apache.http.impl.client.HttpClientBuilder;
  var HttpPost = org.apache.http.client.methods.HttpPost;
  var StringEntity = org.apache.http.entity.StringEntity;
```

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_scriptex11.png" style="height: 350px; width:500px;"/>

<br>

Next, we'll add the credentials that will be used to authenticate the call.

45. In the **Script Body** field, add the following code snippet <u>directly below</u> the **function(doc)** line:

```
var pwd = "password123";
var user = "admin";
var fusionUrl = "http://localhost:8764";
var client = null;
```

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_scriptex12.png" style="height: 350px; width:500px;"/>

<br>

Now that the script building blocks are in place, we can instantiate the client.

46. In the **Script Body** field, add the following code snippet to the **try clause** declaration:

```
var authJson = "{\"username\":\"" + user + "\", \"password\":\"" + pwd + "\"}";
    var authUrl = fusionUrl + "/api/session?realmName=native";
    var provider = new BasicCredentialsProvider();
    var credentials = new UsernamePasswordCredentials(user, pwd);
    provider.setCredentials(AuthScope.ANY, credentials);
    var client = HttpClientBuilder.create()
       .setDefaultCredentialsProvider(provider)
       .build();
```

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_scriptex13.png" style="height: 430px; width:500px;"/>

<br>

Finally, let's add the action to use the client-plus-credentials to build a REST call and establish an authenticated session.

47. In the **Script Body** field, add the following code snippet to the <u>end</u> of the **try clause** declaration:

```
var session = new HttpPost(authUrl);
    var params = new StringEntity(authJson);
    session.addHeader("content-type", "application/json");
    session.setEntity(params);   
    var response = client.execute(session);
```

<img src="https://storage.googleapis.com/fusion-datasets/LabScreenshots_5.7/afjava/afjava_scriptex14.png" style="height: 430px; width:500px;"/>

<br>

While you are welcome to clear the datasource and re-run the job and view the results of the new call, you will not see anything different from our last set of results. We are sharing this as an example of <i>how</i> to write this type of script.

<br>

>If you feel your code is not working, you can copy the full codes for the Authenticated Call pipeline stage below, then paste it into the script body field.

<br>

<details>

<summary>Click the arrow to view the full script body for the Authenticated Call pipeline stage.</summary> 

```
function(doc){
  var pwd = "password123";
  var user = "admin";
  var fusionUrl = "http://localhost:6764";
  var client = null;
  
  var UsernamePasswordCredentials = org.apache.http.auth.UsernamePasswordCredentials;
  var AuthScope = org.apache.http.auth.AuthScope;
  var BasicCredentialsProvider = org.apache.http.impl.client.BasicCredentialsProvider;
  var HttpClientBuilder = org.apache.http.impl.client.HttpClientBuilder;
  var HttpPost = org.apache.http.client.methods.HttpPost;
  var StringEntity = org.apache.http.entity.StringEntity;

  var e = java.lang.Exception;
 
  try {
    var authJson = "{\"username\":\"" + user + "\", \"password\":\"" + pwd + "\"}";
    var authUrl = fusionUrl + "/api/session?realmName=native";
    var provider = new BasicCredentialsProvider();
    var credentials = new UsernamePasswordCredentials(user, pwd);
    provider.setCredentials(AuthScope.ANY, credentials);
 
    var client = HttpClientBuilder.create()
      .setDefaultCredentialsProvider(provider)
      .build();
    
    var session = new HttpPost(authUrl);
    var params = new StringEntity(authJson);
    session.addHeader("content-type", "application/json");
    session.setEntity(params);
 
    var response = client.execute(session);
    
    //Add any REST calls you would like to make to Fusion here
 
  } catch (e) {
    logger.error("Error getting httpclient " + e.getLocalizedMessage());
  }
  return doc;
}
```

</details>

---
<br>

## Great job! You have successfully completed the JavaScript in Fusion Lab, where you have learned how to use JavaScript to modify and authenticate documents via a REST Call. 

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