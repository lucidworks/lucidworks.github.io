---
layout: page
title: Javascript in Fusion
permalink: /afjava/
---

<link rel="stylesheet" href="/lib/public/global-training.css">

## The environment should begin to load immediately. Please do not click *Start Lab* again. It may take a few minutes for the Fusion environment to fully display.

When the Fusion Login page displays, login:
    
* USERNAME: ```admin```
* PASSWORD: ```password123```

# In this lab  you will learn how to modify a document via REST Call, as well as authenticate a REST call. Let's get started!


> Note: You may need to adjust the size of the instructions panel to fully view results in the UI. Toggle the window sizes as needed.


# Modifying a Document via REST Call

1. In the Fusion Admin UI, click **Create New App**

2. For App Name, enter **JS Labs**

3. Click **Create App**

4. Click **JS Labs** to open your newly created app

5. Hover over INDEXING and click **Datasources**

6. Click: **Add+**

7. Begin typing “web” and select the **Web** result

8. For Datasource ID, enter: **Lucidworks_website**

    a. For PIPELINE ID, enter **JS_Labs**

    b. For PARSER, enter **JS_Labs**

>Note: The values for PIPELINE ID and PARSER may already be populated

9. Click **Add** next to **Start Link** and enter: ``https://lucidworks.com``

10. Scroll down and expand **Limit Documents**

    a. Max Crawl Depth: **1**

    b. Max Items: **10**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Javascript_1.png" style="height: 425px; width:475px;"/>

<br>

> **Note:** This ensures that our indexing job will only take a small sample of data.

11. Click: **Save**, **Run**, then **Start** and wait until the job shows success

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Screen%20Shot%202021-11-23%20at%2012.41.08%20PM.png" style="height: 282px; width:544px;"/>

<br>

In this task we will set up a JS stage that instantiates an HTTP client, accesses a URL, and uses data from that URL to modify the pipeline document

12. Navigate to **Index Pipelines**

13. Select pipeline: **JS_Labs**
    
14. Click **Add a new pipeline stage** and select **JavaScript** for the stage type

15. For Label, enter: **REST Call**

16. Find the Script Body, clear what is in it by default, and copy and paste the following to it:

```Javascript
function(doc){
  var e = java.lang.Exception;
  try{  
  }catch(e){
    logger.error(e.getLocalizedMessage());
  }
  return  doc;
}
```
<br>

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Screen%20Shot%202021-11-10%20at%204.15.02%20PM.png" style="height: 288px; width:500px;"/>

<br>

> **Note:** Embedding most of the functional code in a try-catch is a best practice for code safety

17. In the Script Body of the REST Call stage, add these class declarations <u>above</u> the **try clause**:

> Note: For reference, see screenshot below

```Javascript
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

The first thing this stage will do is set up an HTTP client and a REST request

<br>

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Screen%20Shot%202021-11-10%20at%204.20.02%20PM.png" style="height: 267px; width:500px;"/>

<br>

18. In the Script Body of the REST Call stage, <u>after</u> the variable definitions, add the following within the **try clause**:

```Javascript
 var client = HttpClientBuilder.create().build();
 var url = new String("http://www.google.com/search?q=httpClient");
 var request = new HttpGet(url);
 request.addHeader("User-Agent", userAgent);
```
<br>

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Screen%20Shot%202021-11-22%20at%2012.09.08%20PM.png" style="height: 517px; width:650px;"/>

<br>


The URL we are fetching is not very interesting nor is it related to the Lucidworks.com site that the documents are coming from.  It serves the purpose of illustrating how such a request can be made.


Next, the stage will execute the REST call and construct a response object to parse

19. In the Script Body add the following to the <u>end</u> of the **try clause**:

```Javascript
var response = client.execute(request);
 var rd = new BufferedReader(new InputStreamReader(response.getEntity().getContent()));
 var result = new StringBuffer();
 var line = "";
 while ((line = rd.readLine()) !== null) {
   result.append(line);
 } 
```

<br>

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Screen%20Shot%202021-11-09%20at%205.24.18%20PM.png" style="height: 262px; width:500px;"/>

<br>

Finally, the stage will parse the response using Jsoup, fetch the URL’s title, and attach that title to the Pipeline Document in the sub_title field

20. In the Script Body, add the following to the <u>end</U> of the **try clause**:

```Javascript
var Jsoup = org.jsoup.Jsoup;
 var httpDoc = Jsoup.parse(result);
 var httpTitle = httpDoc.select("title").first();
 doc.addField("sub_title", httpTitle);
 } 
```

<br>

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Screen%20Shot%202021-11-09%20at%205.28.50%20PM.png" style="height: 246px; width:500px;"/>

<br>

21. **Close** the Script Body editor and **save** the updated REST Call stage

22. Return to the Datasource window and **clear the Datasource**, then **re-run**, **start** and **save** the Lucidworks_website datasource

23. Navigate to the **Query Workbench**. There should be a total of 10 docs or less

If you look at the Job History for the Lucidworks_website datasource, you will see that its last successful run took ~10 seconds.  Given that it only produces ~30 documents, that is absurdly slow.  The reason for this is that setting up and using an HTTP Client is not very fast.  

Since the client we set up and the URL we fetch are the same every time, we can instead make this stage stateful.  It will execute the client setup and REST call once, save the result, and use that saved result every time the stage runs.
<br>

24. Return to the **Index Pipelines** window

25. In the Script Body of the REST Call stage, add the following class declaration <u>just above</u> the **try clause**:

```var System = java.lang.System;```

The Script Body should look like this (see line 12):

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Javascript_2.png" style="height: 275px; width:525px;"/>

<br>

26. Add the following line just <u>above</u> the **doc.addField line**:

```
System.setProperty("page_sub_title", httpTitle);
```


This saves httpTitle as a Java system property, so that it is persists between starts and stops of this stage

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Javascript_3.png" style="height: 175px; width:375px;"/><br>

Now that we have made the httpTitle persistent, we need to add a conditional to the function so that the HTTP Client will only be created if the target system property is empty.  Otherwise, the function should fetch the system property and skip client creation and REST call execution

27. Add the following <u>just beneath</u> the **try clause** declaration:

```
var httpTitle = "";
  if(System.getProperty("page_sub_title") == null){
```
<br>


So it looks like this:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Javascript_4.png" style="height: 110px; width:375px;"/>

<br>

28. Now, add the following <u>just</u> above the **doc.addField** line:

```
 } else {
   httpTitle = System.getProperty("page_sub_title");
 }
```
<br>

So it looks like this:


<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Javascript_5.png" style="height: 110px; width:375px;"/>

<br>

29. Close the Script Body editor

30. **Save** the updated REST Call stage

31. **Clear** and **re-run** the Lucidworks_website datasource

32. Once the datasource finished, check the **Job History**

Now the job should only take 3-5 seconds.

# Authenticating a REST Call

In the last task, we set up a JS stage that modified a document with information from a REST call.  But what do we do if the endpoint requires authentication?  That’s what this lab will explore.

In this case, we will use Fusion as our target endpoint, using the admin password you’ve already created.

33. Navigate to **Index Pipelines**

34. Select the **JS_Labs** pipeline

35. Add a new JavaScript stage

36. For Label, enter: **Authenticated Call**

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Javascript_6.png" style="height: 275px; width:355px;"/>

<br>

37. Add the following to the **Script Body**:

```Java
function(doc){
var e = java.lang.Exception;
  try {
  } catch (e) {
    logger.error("Error getting httpclient " + e.getLocalizedMessage());
  }
  return  doc;
}
```

<br>


38. In the Script Body, add the following class declarations <u>to the top</u> of **function(doc)**:

```Javascript
var UsernamePasswordCredentials = org.apache.http.auth.UsernamePasswordCredentials;
  var AuthScope = org.apache.http.auth.AuthScope;
  var BasicCredentialsProvider = org.apache.http.impl.client.BasicCredentialsProvider;
  var HttpClientBuilder = org.apache.http.impl.client.HttpClientBuilder;
  var HttpPost = org.apache.http.client.methods.HttpPost;
  var StringEntity = org.apache.http.entity.StringEntity;
```

39.  Add credentials to the block of class declarations <u>at the top</u> of **function(doc)**:

```Javascript
 var pwd = "password123";
 var user = "admin";
 var fusionUrl = "http://localhost:8764";
 var client = null;
```
<br>


 So it looks like this:

<img src="https://storage.googleapis.com/fusion-datasets/5.4_Markdown_images/02%20AF/Javascript_4/Javascript_8.png" style="height: 310px; width:575px;"/><br>

Now that the building blocks are in place, we can instantiate the client 

40. Add the following code to the **try clause** <u>within</u> **fuction(doc)**:

```Javascript
var authJson = "{\"username\":\"" + user + "\", \"password\":\"" + pwd + "\"}";
    var authUrl = fusionUrl + "/api/session?realmName=native";
    var provider = new BasicCredentialsProvider();
    var credentials = new UsernamePasswordCredentials(user, pwd);
    provider.setCredentials(AuthScope.ANY, credentials);
    var client = HttpClientBuilder.create()
       .setDefaultCredentialsProvider(provider)
       .build();
```
<br>

Finally, we can use the client-plus-credentials to build a REST call and establish an authenticated session

41. Add the following code to the <u>end</u> of the **try clause** <u>within</u> **function(doc)**:

```Javascript
var session = new HttpPost(authUrl);
    var params = new StringEntity(authJson);
    session.addHeader("content-type", "application/json");
    session.setEntity(params);   
    var response = client.execute(session);
```
<br>

If you feel your codes aren't working, you can copy the full codes for the REST Call and the Authenticated Call pipelines below and paste them into the script bodies

<details>

<summary>Click to expand the REST Call full script body </summary> 

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
<details>

<summary>Click to expand the Authenticated Call full script body</summary> 

```function(doc){
  var e = java.lang.Exception;
  var UsernamePasswordCredentials = org.apache.http.auth.UsernamePasswordCredentials;
  var AuthScope = org.apache.http.auth.AuthScope;
  var BasicCredentialsProvider = org.apache.http.impl.client.BasicCredentialsProvider;
  var HttpClientBuilder = org.apache.http.impl.client.HttpClientBuilder;
  var HttpPost = org.apache.http.client.methods.HttpPost;
  var StringEntity = org.apache.http.entity.StringEntity;
  
  var pwd = "password123";
  var user = "admin";
  var fusionUrl = "http://localhost:6764";
  var client = null;
 
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
<br>
Make sure to save your open windows before ending your lab.

_________

## Congratulations! You have successfully modified and authenticated a document via REST Call. If you would like to save your Fusion App to reference later, you can do it now:

1. Return to the Fusion Launcher
2. Hover over your app and click on the cog that appears in the lower right corner
3. Within the box that opens, click **Export app to zip**
