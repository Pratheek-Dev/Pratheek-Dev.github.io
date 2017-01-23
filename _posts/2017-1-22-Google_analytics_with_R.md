---
layout: post
title: Using Google Analytics with R and Jekyll
---

### Introduction

Google’s developer console has several APIs that can be customized and used for a plethora of development tasks. Some popular APIs include, the Google Maps, Google Cloud, Google Apps and the Google Analytics API. The Google Analytics API provides structured data analytics and reporting tools for clients. For example, with the analytics API, it is possible to access a website’s total bounce rates, popularity, global traffic, and traffic peaks.

In order to collect the data from the API and work with it programmatically, we can use the R package, `rga` - R Google Analytics.

Let’s being by setting up the basic requirements in Google Developer Console to access the Google Analytics API:

#### Step 1: Set up a Google Analytics Account

Ensure you have a google account (i.e. Gmail account) as it will be required before proceeding any further. I logged into my google account and proceeded to the [Google Analytics website] (https://analytics.google.com/analytics/web/?authuser=0#management/Settings/a90661696w134530349p138597581/%3Fm.page%3DTrackingCode%26_r.ghFlowId%3D6324039/) and created the analytics profile that I want to request data from.


#### Step 2: Set up Analytics with Jekyll

I am using Jekyll to create my blog posts and I would like to perform analytics on my blogs. In order to do so, I will be modifying some of the code in the Jekyll default template so that the google-analytics can communicate with my blog traffic data.

In the forked Jekyll template repository, I opened the `_includes` folder and created `analytics.html` with the following code inside (from the google analytics tracking id):

```
<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

  ga('create', 'UA-90661696-1', 'auto');
  ga('send', 'pageview');

</script>
```
![Adding analytics.html](../images/analytics.png)


Then, in the `_layouts` folder, I opened the `default.html` file and added `{% include analytics.html %}` tag so that all the blog posts can be tracked by Google Analytics.

![Adding tag in <body>](../images/body.png)



Step 2: Access the Developer Console

Go to the Google Developer Console (https://console.developers.google.com/apis/library) and search for the `Analytics API` under the menu `Other popular APIs`. On the top right hand corner, click on the `Create New Project` if it’s your first time working with any google APIs.

Step 3: Setting up a new project for Analytics API

 Configure your project with a descriptive name and agree to the `terms and conditions check box. A project ID will be displayed below your project name.  Finally, click `create` to commence the analytics project.

Step 4: Creating Credentials

In this part, we will be setting up the authentication keys, so that we will be able to access the Google Analytics API from R.  On the left hand panel, click on the `Credentials` menu and under the `Credentials` tab, click on `Create Credential`, which will drop down with three menu options, and we will select the `OAuth Client Id`. On the next screen we will have to select `others` for usage type. If prompted to name a product name, click on that link select a product name for the profile (in my case, I used `Google Analytics with R` as the product name).

Now back to the `Application Type` menu, where we selected `other`, and will we select an appropriate name. I decided to keep my naming consistent and named my `Client ID` as `Google Analytics with R`.

We should now have a `client-id secret` and a `client-id url`. Both of which will be required when authenticating using R.

Step 5: Setting up a Google Analytics View

I will be using the default Google Analytics Viewer (https://ga-dev-tools.appspot.com/query-explorer/), but you’re welcome to select any other application you would like to work with. The basic idea behind a viewer is to select a website to perform analytics on.
