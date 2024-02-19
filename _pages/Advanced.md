---
title: Lab 2 - Advanced
author: Yaroslav & Dimitri
date: 2022-02-02
category: Jekyll
layout: post
---
```
Last modified: Tue, 16 Feb 2024
```

## Webex Contact Center API and Widgets

Welcome to the Contact Center API and Agent Desktop Customization Lab Guide – your gateway to exploring advanced features in Contact Center solutions. This intermediate-level tutorial focuses on integrating APIs and customizing agent desktops using widgets.

As businesses prioritize exceptional customer experiences, this guide empowers you to enhance agent workflows. You'll gain hands-on experience integrating Contact Center APIs and discover how to customize agent desktops effectively with widgets. Whether you're a developer or customization enthusiast, this tutorial is designed to meet your intermediate-level needs, providing the skills to create a more intuitive and personalized workspace for contact center agents.

Let's dive in and unlock the potential of Contact Center API integration and agent desktop customization!

## Table of Contents


| Topic | Lab Type | Difficulty Level | Estimated length |
| ---- | ---- | ---- | ---- |
| [**Part 1: APIs on Webex Contact Center (WxCC)**](#APIs-on-Webex-Contact-Center) | Practical Lab | MED | 90 min |
| - Lab 1 –APIs Fundamental |  |  |  |
| - Lab 2 – Developer Portal |  |  |  |
| - Lab 3 – WxCC APIs - Postman |  |  |  |
| - Lab 4 – Import WxCC APIs to Postman |  |  |  |
| [**Part 2: Custom Widgets on Agent Desktop**](#Custom-Widgets-on-Agent-Desktop) | Practical Lab | HARD | ?? min |


## **APIs on Webex Contact Center (WxCC)**

This is an **intermediate** level lab intended for engineers with prior **Webex Contact Center (WxCC)** experience.

The WxCC APIs enable you to access the WxCC platform programmatically to customize, fine tune and build the solution.

Upon completion of this lab, you will be able to:
- Get familiar with Developers portal and Postman
- Learn some WxCC APIs
- Configure and Implement WxCC via APIs
- Obtain WxCC information via APIs.

**Disclaimer:** This lab is not designed for a production system, thus not all recommended features are implemented or enabled optimally. For implementation and design-related questions, please contact your representative at Cisco, or a Cisco partner.

## Lab 1 –APIs Fundamental 
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

**Step 4.** Create your workspace. On the Workspaces tab, type the name of your workspace. In this exercise your workspace name is the same as the username. So, for Pod1, type Ciscolabuser001.
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










===============================================================
## JDS APIs & Use Cases
This lab is designed to teach you the concepts and functionalities of Customer Journey Data Services (JDS), both in regard to the JDS Widget that can be added in Agent Desktop as well as the API capabilities of the solution, since JDS remains an API-first solution today. You will learn how to use the JDS widget, how to add new customers (identities) to your JDS database as well as how to use the JDS APIs to extract information and act upon it. 

# Exploring JDSs APIs & Widget
JDS Desktop Widget provides agents with an interface that shows the end customer’s complete journey with the agent’s business, aggregated metrics of their experience as well as the customer’s unique identifiers (aliases).
<img width="1015" alt="image" src="https://github.com/WebexCC-SA/partner-summit/assets/43476977/ef44388d-8984-430b-b2d1-971f8929926a">


## Task 1: Adding a new identity for the JDS project
## Task 2: Adding JDS to the Desktop layout 
-- Assign to the team and sign in as an agent
## Task 3: Downloading the JDS Postman collection
## Task 4: Exploring the JDS APIs
## Task 5: Creating a new event via API 
-- Check in the widget



# Use Case - Journey Based Queue Priority
-- About Use Case
## Task 1: Getting number of requests for the X last days/hours
## Task 2: Adding JDS API Request to the Flow Designer
## Task 3: Making a test call and checking the restul




<p style="text-align:center"><strong>Congratulations, you have completed this lab! You can continue with the next one.</strong></p>
		
<p style="text-align:center;"><img src="/assets/gitbook/images/webex.png" width="100"></p>	

