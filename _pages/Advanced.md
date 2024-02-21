---
title: Lab 2 - Advanced
author: Yaroslav & Dimitri
date: 2022-02-02
category: Jekyll
layout: post
---
```
Last modified: Tue, 20 Feb 2024
```

## Webex Contact Center API and Customer Journey Data Services (JDS)

Welcome to the Contact Center API and JDS Lab Guide – your gateway to exploring advanced features in Contact Center solutions. This intermediate-level tutorial focuses on integrating APIs and exploring JDS functionality.

As businesses prioritize exceptional customer experiences, this guide empowers you to enhance agent workflows. You'll gain hands-on experience integrating Contact Center APIs and discover how to use JDS effectively with JDS widget.

Let's dive in and unlock the potential of Contact Center API integration and JDS use cases!

## Table of Contents


| Topic | Lab Type | Difficulty Level | Estimated length |
| ---- | ---- | ---- | ---- |
| [**Part 1: APIs on Webex Contact Center (WxCC)**](#APIs-on-Webex-Contact-Center) | Practical Lab | MED | 45 min |
| Lab 1 – APIs Fundamental |  |  |  |
| Lab 2 – Developer Portal |  |  |  |
| Lab 3 – WxCC APIs - Postman |  |  |  |
| Lab 4 – Import WxCC APIs to Postman |  |  |  |
| [**JDS APIs & Use Case**](#jds-apis--use-cases) | Practical Lab | HARD | 45 min |


## **APIs on Webex Contact Center (WxCC)**

This is an **intermediate** level lab intended for engineers with prior **Webex Contact Center (WxCC)** experience.

The WxCC APIs enable you to access the WxCC platform programmatically to customize, fine tune and build the solution.

Upon completion of this lab, you will be able to:
- Get familiar with Developers portal and Postman
- Learn some WxCC APIs
- Configure and Implement WxCC via APIs
- Obtain WxCC information via APIs.

**Disclaimer:** This lab is not designed for a production system, thus not all recommended features are implemented or enabled optimally. For implementation and design-related questions, please contact your representative at Cisco, or a Cisco partner.

## Lab 1 – APIs Fundamental 
### Objectives 
The objective of the lab is to introduce you to concept of APIs and the way the Postman tool can be used to manage APIs.

**Note:**  If you are already familiar with APIs and Postman, you can skip this lab. We also recommend using Google Chrome for all labs requiring a web browser but for this lab sometimes we have used Firefox for some specific simplicity.

### Task 1: APIs Fundamentals

An API is a set of tools, definitions, and rules or protocols for building a software application.

APIs allow one component of software to easily communicate with another component of software. Cisco product designers determine the APIs that each Cisco product supports.

Many of the Webex Customer Experience APIs are RESTful. Each resource is represented by a base URL and supports various methods for API usage. Refer to API Reference (https://developer.webex-cx.com/documentation/introduction-to-apis) for details.

#### Methods

An API method defines what the API Client (who is allowed to ask for the data or request the service) should or must do to submit a request to access the service at the backend (API server)

These are the methods supported for Webex Contact Center APIs:

![API01](/assets/images/API/API01.jpg)


#### API Anatomy

Here is an example of an API GET request that helps define the API anatomy:
![API02](/assets/images/API/API02.jpg)

##### - http:// or https://
	- Protocol over which data is sent between client and server.
	- ‘s’ in https stands for secure.
##### - Server or Host
	- Resolves to the IP and port to which to connect.
##### - Resource
	 - The location of the data or object of interest
##### - Parameters
	- Details to scope, filter, or clarify a request. Often optional.


#### Authentication and Authorization
To use the Webex REST API, you'll need a Webex account backed by Cisco Webex Common Identity (CI).

When making requests to the Webex REST API, an Authentication HTTP header is used to identify the requesting user. This header must include an access token.

For authorization, there are different types that are supported for Webex APIs:
- None: Web API resource is public, anybody can place requests
- Basic (over SSL/TSL): Username and password passed to server in base64 encoded (not encrypted) string.
- Authorization : Basic ENCODEDSTRING
- Oauth 2.0: Standard framework to retrieve access token from Identity Provider
- Authorization: Bearer ENCODEDSTRING
 - Authorization can be short-lived and require refreshing of token.

#### Examples:

In this example you will use deck of cards public API to simulate a game of cards.

**Step 1.** Open a Firefox Web browser, execute this GET API and define the number of decks you want to use. The default is one. But change the parameter to 6 in order to play Blackjack.

[https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=6](https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=6)

You see the response in Json format:

![API03](/assets/images/API/API03.jpg)

**Step 2.** Change the parameter now to 1 and check the response.
[https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=1](https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=1)

You see the remaining cards in one deck.

![API04](/assets/images/API/API04.jpg)

**Step 3**. The count variable defines how many cards to draw from the deck. Be sure to replace _deck_id_ with the id obtain from the previous example. You can also replace it with “new” to create a new shuffle deck and draw cards from this new deck.

https://deckofcardsapi.com/api/deck/<<deck_id>>/draw/?count=2

Replace the deck_id with the id, you got from the previous response. For example: [https://deckofcardsapi.com/api/deck/58f7v8te5530/draw/?count=2](https://deckofcardsapi.com/api/deck/58f7v8te5530/draw/?count=2)

![API1](/assets/images/API/API1.jpg)

![API2](/assets/images/API/API2.jpg)

or replace it with “new”.
https://deckofcardsapi.com/api/deck/new/draw/?count=2

![API3](/assets/images/API/API3.jpg)
![API4](/assets/images/API/API4.jpg)

***Note:** In these examples, you did not have to be authenticated and authorized because it is a public API.*


#### Task 2: Postman Fundamentals

Postman is an API platform for building and using APIs. It includes a comprehensive set of tools that help accelerate the API lifecycle—from design, testing, documentation, and mocking to the sharing and discoverability of your APIs.

Postman can only run on the Chrome browser. To use Postman, you will first need to install Google Chrome.

In this lab we will use Web based version of the Postman API client tool to define API requests and test them.

***Note**: In this lab you will use Postman browser and sign in with a pre-registered account *

**Step 1.** Locate the Chrome icon at the bottom of the task bar and launch it.

![API5](/assets/images/API/API5.jpg)

**Step 2.** Navigate to postman.com and select sign in.
![API6](/assets/images/API/API6.jpg)

**Step 3.** Provide the username related to the username assigned by your proctor and the password. ***Note:** Please be careful to follow the steps if you use shared infrastructure.*

For example, the username is **<<To_add_user_from the sheet>>.** The password is the same for all users: **<<To_add_pwd_from the sheet>>.**

![API7](/assets/images/API/API7.jpg)

**Step 4.** Create your workspace. On the Workspaces tab, type the name of your workspace. In this exercise your workspace name is the same as the username. So, for Pod1, type ~~**Ciscolabuser001**~~.


![API8](/assets/images/API/API8.jpg)

**Step 5.** On the Workspace create window, add the name, check the Personal option and click Create Workspace.
![API9](/assets/images/API/API9.jpg)

![API10](/assets/images/API/API10.jpg)

**Step 6.** You see your workspace created and all options on the left side of the window. You will navigate to each of this option to understand Postman functionality.
![API11](/assets/images/API/API11.jpg)

Step 7. Select New and then HTTP Request to create a new API request.
![API11-12](/assets/images/API/API11-12.jpg)

**Step 8.** Notice in the screenshot below that the default method is GET; Click the drop-down arrow next to it to show all other REST API methods including the ones mentioned above for WxCC.
![API13](/assets/images/API/API13.jpg)

**Step 9.** Evaluate the previous deck of cards API via Postman. Copy the following URL and paste it into Postman and select the GET option to the left:

[https://deckofcardsapi.com/api/deck/new/draw/?count=2](https://deckofcardsapi.com/api/deck/new/draw/?count=2)
![API14](/assets/images/API/API14.jpg)

Note, that after adding the URL, the parameter count was automatically added.

**Step 10.** Click Send button. Review the results. You see 200 OK in the response, which indicates that this was a successful response, you see the body of the response and the format.
![API15](/assets/images/API/API15.jpg)

**Step 11.** Save this request in a Collection. Select Save As from the pull-down button.
![API16](/assets/images/API/API16.jpg)

**Step 12.** Click Create a Collection. Add the name DeckofCards and click Create. Then, click Save.
![API17](/assets/images/API/API17.jpg)

![API18](/assets/images/API/API18.jpg)

You see the collection now added to your workspace.

**Step 13.** Open a brand-new deck of cards. Copy the following URL, paste it into Postman, and select the POST option to the left. Add the parameter _jokers_enabled=true._
https://deckofcardsapi.com/api/deck/new/

![API19](/assets/images/API/API19.jpg)

**Step 14.** Save this request in the previous created Collection. Change the name of the request and click SAVE.
![API20](/assets/images/API/API20.jpg)


Postman offers lot of other options for APIs, some of which we'll explore in the subsequent sections of this lab.


# Lab 2 – Developer Portal

Developers can build, enhance, and customize their Customer Experience solution with the rich set of APIs, which includes Contact Center, AI, Journey, Orchestration and Experience Management. The Developers portal help you to get started with the APIs. The Developers portal provides detailed API reference docs as well as the Try Out functionality which help to familiarize you with WxCC APIs and learn quickly.


## Objectives

The objective of the lab is to understand the benefits of the Cisco Developers Portal to learn and understand WxCC APIs.

### Task 1: Introduction to developer portal

**Step 1. **Open a web browser and navigate to the developer portal: **developer.webex-cx.com.**
Sign in with the username assigned to you and the password is **~~Ciscolabuser123!**~~ 

![API21](/assets/images/API/API21.jpg)


**Step 2.** Select Documentation from the top-right corner.
![API22](/assets/images/API/API22.jpg)

You can see different sections on the left-hand sides, for example:

**Authentication**: This section explains the authentication method used by WxCC and the prerequisites.

**Common API errors:** In this section you have the list of errors that can be returned as a response to an API request.

**Introduction to APIs**: In this section you can find an overview to the WxCC open architecture APIs.

**API Reference**: You will see in this section all the APIs categories that WxCC offers. 

**Step 3.** Navigate to the API reference and select Address Book
![API23](/assets/images/API/API23.jpg)
**Step 4.** In this case, you want to first list the address books already created. So, select the GET request under “List Address Books Entries (v2 API)”

**Step 5.** You can see all the parameters required, like **orgid** and optional parameters, like **page** or**page size,** and so on.

**Step 6.** On the right-hand side, you see how the API is executed. You can see the method; GET; the URL used with the variable (orgid) and the code language that is being used (you can use cURL, csharp, java, python, etc.)
![API24](/assets/images/API/API24.jpg)

**Step 7.** Select the Try out section. As you notice, this requires an authorization token. The token used by default, is the one automatically assigned when you log in with the admin credentials to the Developers portal. It also pulls the orgid from the organization the user you logged in is part of. Click Run.

You see the 200 Response, which indicates the request was successful. You also see the address books created in this org. You can scroll down in the response window to see the list of all address books.

![API25](/assets/images/API/API25.jpg)

**Step 8. **Log in with the same user to WxCC Portal: [https://portal-v2.wxcc-anz1.cisco.com/portal/home](https://portal-v2.wxcc-anz1.cisco.com/portal/home) and navigate to Provisioning > Address Book

![API26](/assets/images/API/API26.jpg)

![API27](/assets/images/API/API27.jpg)


### Task 2 Develop a Webex Application

This task shows you the configuration steps to create a Webex application. This covers how to build the authentication part of the application for use with Postman.

**Step 1. **Logon to [https://developer.webex-cx.com](https://developer.webex-cx.com) with your username and password. On the top-right hand corner, hover over your userID and select My Webex Apps from the pop-out menu.

![API28](/assets/images/API/API28.jpg)

**Step 2. **Provide the name of your choice, description of your choice, the redirect URI and check the scopes (Config, write and read).

For the URI, we are using Postman as a sample application so, use this URI: [https://oauth.pstmn.io/v1/callback](https://oauth.pstmn.io/v1/callback) and select the top 3 scopes as shown in the screenshot below.

![API29](/assets/images/API/API29.jpg)

**Step 3. **Accept the terms and click **Add Integration**.

![API30](/assets/images/API/API30.jpg)

**Step 4. **You will get the response with the Client ID, Client Secret, and the URL that you could embed in your application to initiate the authentication.

![API31](/assets/images/API/API31.jpg)

**Step 5. **Copy the whole URL into a new browser window and you see that redirect you to a Webex authentication page.

![API32](/assets/images/API/API32.jpg)

**Step 6. **On the authentication window, click Accept.
![API33](/assets/images/API/API33.jpg)

**Step 7. **You see that your application is now authenticated.

![API34](/assets/images/API/API34.jpg)

More Information about creating a Webex application and using Postman in this document: [https://www.cisco.com/c/en/us/support/docs/contact-center/webex-contact-center/218418-](https://www.cisco.com/c/en/us/support/docs/contact-center/webex-contact-center/218418-configure-webex-contact-center-apis-with.html)

[configure-webex-contact-center-apis-with.html](https://www.cisco.com/c/en/us/support/docs/contact-center/webex-contact-center/218418-configure-webex-contact-center-apis-with.html)


# Lab 3 – WxCC APIs - Postman



===============================================================
## JDS APIs & Use Cases
This lab is designed to teach you the concepts and functionalities of Customer Journey Data Services (JDS), both in regard to the JDS Widget that can be added in Agent Desktop as well as the API capabilities of the solution, since JDS remains an API-first solution today. You will learn how to use the JDS widget, how to add new customers (identities) to your JDS database as well as how to use the JDS APIs to extract information and act upon it. 

# Exploring JDSs APIs & Widget
JDS Desktop Widget provides agents with an interface that shows the end customer’s complete journey with the agent’s business, aggregated metrics of their experience as well as the customer’s unique identifiers (aliases).
<img width="1433" alt="image" src="https://github.com/WebexCC-SA/partner-summit/assets/43476977/e710de0e-e311-4e35-9599-6ae72aede7af">

- **Identity / Person**: A unique customer, all the events that the same customer (e.g. call, chat, email, visit website) creates are marked under the same identity.
- **Alias**: Different ways we can identify the same customer/person (e.g. email, phone number, Customer ID). Customer must have at least one alias.
- **Profile Template**: A profile template defines the kind of aggregation technique we want to see for a customer (e.g. contacts within _last 24 hours_).
- **Progressive Profile**: The values that correspond to an identity’s profile template at that particular moment of time (e.g. contacts within last 24 hours = _10_).


## Task 1: Adding a new identity for the JDS project

> Note 1: For this task, you must have an admin account with the **"Full admin"** permissions.\
> Note 2: To save time, we will be skipping that exercise. Please read it and go to the next task.
{: .block-tip }

1.	Add a new identity for yourself to JDS project. Navigate to Control Hub with your administrator credentials.

2.	Navigate to Customer Journey Data under Monitoring.
<img width="1790" alt="image" src="https://github.com/WebexCC-SA/partner-summit/assets/43476977/b469dce7-8fde-4ca1-be48-9114bd6faa4f">


3.	A project (named  **Lab Tenant**) has already been created for the purposes of this lab. Click on it to check its configuration.

4.	Click on the Identities tab. Identities are all the end-customer profiles created to be tracked by this specific JDS project.
 <img width="1786" alt="image" src="https://github.com/WebexCC-SA/partner-summit/assets/43476977/203c2b35-7aeb-4278-85fb-cafbca307736">



5.	Click on **Add Identities** button. In the UI you can only add identities by uploading a CSV file. To check the expected format of the CSV, click on Download to download the sample template.
 
6.	Open the file. You see the expected format is the following:
```Id,First Name,Last Name,Email Addresses,Phone Numbers,Customer Ids```

7.	Enter a row with your details keeping in mind the following:
•	**Id** field should be left empty.
•	If you want to add multiple **email addresses, phone numbers or customer IDs**, you need to use the pipe “|” delimiter between them. For example, try to add your phone number both with and without a plus sign.
•	**Customer ID** is a unique ID given by the JDS administrator to each customer. Make sure to use a large number to avoid conflicts with existing customer IDs.

8.	Based on the above, your new line should look similar to this:
 <img width="989" alt="image" src="https://github.com/WebexCC-SA/partner-summit/assets/43476977/890d2d05-9eec-4d6f-9e0d-b2ea67f16c66">


9.	Save the file and go back in Control Hub, click on **Choose a file** and select the file you created. Click on **Next**. If all is good, you will see the Import Status as _Completed_. In case of errors, you will get the message Completed with Errors and the option to download the error file to understand what you need to fix.

10.	Click on **Close** button. You should now be able to see your created identity in the list.



## Task 2: Adding JDS to the Desktop layout 
The process to add the JDS Widget is also thoroughly explained on the [GitHub page](https://github.com/CiscoDevNet/cjaas-widgets/blob/main/CustomerJourney/README-VERSION-9.0.0.md), including a video walkthrough. 

1.	Download the default JSON Layout from the Control Hub -> Contact Center ->  Desktop Layouts ->  Global Layout 
<img width="1720" alt="Screenshot 2024-02-20 at 17 52 00" src="https://github.com/WebexCC-SA/partner-summit/assets/43476977/3431a739-07e4-4d38-82e6-d4be6ae7e51b">

2. Within the downloaded default desktop layout JSON file, search for the data property "visibility": "IVR_TRANSCRIPT" under the **agent** section. Find the following code block associated with that.
> Note: IVR_TRANSCRIPT may appear a few times, please find the last appearance of "visibility": "IVR_TRANSCRIPT"

<img width="967" alt="image" src="https://github.com/WebexCC-SA/partner-summit/assets/43476977/9016f607-c58e-4916-946d-a7aba49e3bd0">

3.	Copy the JDS Widget code block below:

```
{
            "comp": "md-tab",
            "attributes": {
              "slot": "tab"
            },
            "children": [
              {
                "comp": "slot",
                "attributes": {
                  "name": "WXM_JOURNEY_TAB"
                }
              }
            ],
            "visibility": "WXM_JOURNEY"
          },
          {
            "comp": "md-tab-panel",
            "attributes": {
              "slot": "panel",
              "class": "widget-pane"
            },
            "children": [
              {
                "comp": "customer-journey-widget",
                "script": "https://cjaas.cisco.com/widgets/customer-journey-9.0.0.js",
                "attributes": {
                  "base-url": "https://api-jds.prod-useast1.ciscowxdap.com",
                  "logs-on": "true",
                  "project-id": "65171e0682b7f52b9209b39d",
                  "template-id": "journey-default-template1",
                  "icon-data-path": "https://wxcc-widgets.s3.us-west-1.amazonaws.com/icons.json",
                  "limit": "50",
                  "time-frame": "All",
                  "live-stream": "true"
                },
                "properties": {
                  "interactionData": "$STORE.agentContact.taskSelected",
                  "bearerToken": "$STORE.auth.accessToken",
                  "organizationId": "e56f00d4-98d8-4b62-a165-d05a41243d98"
                },
                "wrapper": {
                  "title": "Customer Journey Widget",
                  "maximizeAreaName": "app-maximize-area"
                }
              }
            ]
          },
```
> For this lab, the Project ID is **65171e0682b7f52b9209b39d**. Project ID can be found in the Customer Journey Data tab in Control Hub.
<img width="753" alt="Screenshot 2024-02-20 at 17 53 11" src="https://github.com/WebexCC-SA/partner-summit/assets/43476977/60968b46-818e-4809-ab27-17dc275a4a33">

4. If in the **Default Desktop Layout** the WxM widget is already presented, make sure that the following section is removed
```
{
            "comp": "md-tab",
            "attributes": {
              "slot": "tab"
            },
            "children": [
              {
                "comp": "slot",
                "attributes": {
                  "name": "WXM_JOURNEY_TAB"
                }
              }
            ],
            "visibility": "WXM_JOURNEY"
          },
          {
            "comp": "md-tab-panel",
            "attributes": {
              "slot": "panel",
              "class": "widget-pane"
            },
            "children": [
              {
                "comp": "agentx-wc-cloudcherry-widget",
                "properties": {
                  "userModel": "$STORE.app.userModel",
                  "spaceId": "",
                  "metricsId": "",
                  "ani": "$STORE.agentContact.taskSelected.ani",
                  "isDarkMode": "$STORE.app.darkMode"
                },
                "wrapper": {
                  "title": "Customer Experience Journey",
                  "maximizeAreaName": "app-maximize-area"
                }
              }
            ],
            "visibility": "WXM_JOURNEY"
          },
```

4. Save the desktop Layout that now has your customer journey widget code. 

> The modified JSON file (4 steps above) can be downloaded [here](files/JDS_Layout.json)
{: .block-tip }

5. Go to Control Hub -> Contact Center ->  Desktop Layouts and Create a new Desktop Layout. 

6. In the name section set your **ID**_JDS_Layout (example: **140_JDS_Layout**). Click on **Replace file**, assign the Layout to your team, and click **Create**.


## Task 3: Downloading the JDS Postman collection
As JDS is an API-first solution, there is a very wide [range of APIs](https://developer.webex-cx.com/documentation/journey) available. To make the introduction to them easier, Cisco has created a [JDS API Collection](https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/customer-journey-samples/cjds-postman-example/JDS%20CiscoLive.postman_collection.json) that you can download and import in your API tool (e.g. Postman) and start playing around, in conjunction with various use cases. 

1.	Download the JDS Postman collection, by going to the [GitHub samples page] (https://github.com/WebexSamples/webex-contact-center-api-samples/blob/main/customer-journey-samples/cjds-postman-example/JDS%20CiscoLive.postman_collection.json)

2. Click on **Download raw file**
<img width="1785" alt="Screenshot 2024-02-21 at 19 34 27" src="https://github.com/WebexCC-SA/partner-summit/assets/43476977/5c197928-ec2c-4fa3-ac8a-bcc4159efdaf">

3. Open the Postman app on your laptop and click on **Import** button.
   
4. Select the downloaded JSON file in the appeared window
<img width="1610" alt="Screenshot 2024-02-21 at 19 36 42" src="https://github.com/WebexCC-SA/partner-summit/assets/43476977/08ccaf18-2ca5-4b75-a2a0-02e4b0999c99">


6. Once the JDS collection is imported, select the root folder of the imported collection in the left menu, then navigate to the **Variables**, and define the values 
> Note: reuse the same values as it was in the API lab (client ID, client Secret and org ID). The **workspaceId** is your project ID which is **65171e0682b7f52b9209b39d**

7. Once the values are defined, click **Save** button
<img width="1603" alt="Screenshot 2024-02-21 at 19 41 36" src="https://github.com/WebexCC-SA/partner-summit/assets/43476977/f1f03ddc-59df-4527-9898-0df61570673b">


8. Go to **Authorization** and click on **Get New Access Token** button. The Postman will redirect you to the Auth page where you need to define your Admin account which was used for the App creation in the dev portal. As a result, you should get the message **Authentication complete**. Click **Proceed** and on the next page click on **Use Token** button
![Auth](https://github.com/WebexCC-SA/partner-summit/assets/43476977/d032ef35-a6ee-4740-af1a-8588e2c089fd)



## Task 4: Exploring the JDS APIs & Creating new events
This video shows you how to use various API's to manage JDS profiles and templates.

<div style="padding-bottom:60.25%; position:relative; display:block; width: 100%">
	<iframe src="https://app.vidcast.io/share/embed/9c7f0d45-d860-4962-99d2-d5d818fde573" width="100%" height="100%" title="JDS Postman Collection" frameborder="0" loading="lazy" allowfullscreen style="position:absolute; top:0; left: 0"></iframe>
</div>






# Use Case - Journey Based Queue Priority
-- About Use Case
## Task 1: Getting number of requests for the X last days/hours
## Task 2: Adding JDS API Request to the Flow Designer
## Task 3: Making a test call and checking the restul




<p style="text-align:center"><strong>Congratulations, you have completed this lab! You can continue with the next one.</strong></p>
		
<p style="text-align:center;"><img src="/assets/gitbook/images/webex.png" width="100"></p>	

