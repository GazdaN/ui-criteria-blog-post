# ui-criteria-blog-post

# UI improvement process of Leisure Time Swiper

Client Side Web Engineering (CSWE) Workshop 25.05.2021

In this blog post we take a closer look at the UX and UI changes we implemented at Leisure Time Swiper during the CSWE workshop on 26.05.

- [UI improvement process of Leisure Time Swiper](#ui-improvement-process-of-leisure-time-swiper)
  - [About the App](#about-the-app)
  - [Tech stack](#tech-stack)
  - [Design](#design)
  - [App flow](#app-flow)
  - [Analysis of our design in regard to 10 Usability Heuristics for User Interface Design](#analysis-of-our-design-in-regard-to-10-usability-heuristics-for-user-interface-design)
    - [#1: Visibility of system status](#1-visibility-of-system-status)
    - [#2: Match between system and the real world](#2-match-between-system-and-the-real-world)
    - [#3: User control and freedom](#3-user-control-and-freedom)
    - [#4: Consistency and standards](#4-consistency-and-standards)
    - [#5: Error prevention](#5-error-prevention)
    - [#6: Recognition rather than recall](#6-recognition-rather-than-recall)
    - [#7: Flexibility and efficiency of use](#7-flexibility-and-efficiency-of-use)
    - [#8: Aesthetic and minimalist design](#8-aesthetic-and-minimalist-design)
    - [#9: Help users recognize, diagnose, and recover from errors](#9-help-users-recognize-diagnose-and-recover-from-errors)
    - [#10: Help and documentation](#10-help-and-documentation)
  - [Creating issues (based on identified problems)](#creating-issues-based-on-identified-problems)
    - [#84 Web build does not work on mobile devices](#84-web-build-does-not-work-on-mobile-devices)
      - [Problem](#problem)
      - [Screenshots](#screenshots)
    - [#72 Web app shell](#72-web-app-shell)
      - [Problem](#problem-1)
      - [Solution](#solution)
      - [Screenshots](#screenshots-1)
    - [#71 Stay logged in Problem](#71-stay-logged-in-problem)
      - [Problem](#problem-2)
      - [Solution](#solution-1)
    - [#69 Logout](#69-logout)
      - [Problem](#problem-3)
      - [Solution](#solution-2)
      - [Screenshots](#screenshots-2)
    - [#74 #75 Undo rating](#74-75-undo-rating)
      - [Problem](#problem-4)
      - [Solution](#solution-3)
  - [Prioritizing issues](#prioritizing-issues)
  - [What was implemented during the workshop](#what-was-implemented-during-the-workshop)
    - [Web build does not work on mobile devices #84](#web-build-does-not-work-on-mobile-devices-84)
    - [Stay logged in #71](#stay-logged-in-71)
    - [Logout #69](#logout-69)
    - [Style changes](#style-changes)
  - [Identified as unnecessary](#identified-as-unnecessary)
    - [Web app shell #72](#web-app-shell-72)
  - [What is yet to be implemented](#what-is-yet-to-be-implemented)
  - [Summary](#summary)

## About the App

Leisure Time Swiper is a mobile application which provides customised leisure-time activities for users based on their personal preferences and situated context. This app will showcase a variety of activities in the user's area in an easy to understand interface with swipe-able cards. By swiping the system collects information about user preferences and shows similar activities or ones similar users like. The additional problem of finding things to do together (in groups) is to be solved by having the possibility of shared swiping sessions, where everyone in the group is able to swipe the same activities.
Our team develops the Leisure Time app as part of the master's project on the MultiMediaTechnology master's degree. We were motivated by the opportunity to help  users find new activities within their vicinity. An additional application we identified could be to support the tourism industry, especially the lesser known attractions.  Moreover, we were eager to learn new technologies and deepen our knowledge in those already known.

## Tech stack

For the frontend side we chose the Flutter framework with Dart, which is able to compile amongst others for web, android and iOS using only one code base.
For the back end service we decided to use the nest.js framework for node.js. All non-static API requests are routed to this service. Here the authentication, the authorisation, the business logic, and the resource management are handled.
For the not yet begun admin panel we chose to use react with typescript and for the also not yet begun recommender service flask for python.
The main goal of the back end and all associated services is to provide efficient and coherent endpoints for the front ends like the app and the administrator panel to use.

## Design

Our application has a rather minimalist design. Everything is kept in the colour scheme of black, white and grey. We are rather satisfied with the current state of the design and are not planning any major changes to the main design area. We think that the main flow of the application is intuitive and simple, which was confirmed during the user testing phase. Most testers immediately knew where they were and what they needed to do.  However, we identified some minor points that definitely need improvement.

## App flow

Currently the application flow is as follows (described to understand the next point: analysis in regard to good ui criteria)

1. Log into (if not already) or register a new account (registering using other providers will be possible in the future)
2. Select and save hobbies, if not already done previously
3. Swipe through possible activities:
    1. Moving the finger up will lead to the details of the activity (also indicated by an arrow up, as shown in card) - currently a click / tap is required
       1. To return to the activity list one will be able to swipe down - currently a click on the arrow is necessary
       2. Swipe through the different images for this activity
       3. Click on a social media / the web site icon to display social media channel or web site of the activity if available
    2. Moving the finger right (swiping right) indicates a like
    3. Moving the finger left (swiping left) indicates a dislike
    4. Clicking on the account icon opens the profile screen containing matched activities
    5. Clicking on the options icon (three dots) opens an overflow menu containing settings and logout

## Analysis of our design in regard to [10 Usability Heuristics for User Interface Design](https://www.nngroup.com/articles/ten-usability-heuristics/)

### #1: Visibility of system status

We generally provide feedback to the user about what is happening. We for example show registration failure messages and a success message with further instructions. But we could improve the usability by also elaborating the failure reason already provided by the API.
It was hardly predictable for the user to be logged out when the page is reloaded or the application is reopened which is why we implemented an automatic stay logged in functionality during the workshop. No indication was displayed that the user was not logged in anymore as the pages were still accessible without content which is why we implemented guards in the front end as well. The refresh was also the only way to log out which lead us to implement the logout functionality.

### #2: Match between system and the real world

We do not use any special terms, icons or images that in any way would not resemble the real world. We stick to terminology that is familiar to the user and have not identified any issues in this regard.

### #3: User control and freedom

At the bottom of the registration screen there is a back to login button, in case the user already has an account (clear way to reverse the decision of logging in instead of creating an account).
Since the most central action in the whole app is swiping / rating we are planning to add an undo button for this action.

### #4: Consistency and standards

All words used in the application follow our conventions. We keep things consistent and currently do not see any issues in this area.

In the main stream, we used the familiar swipe convention as an indicator of likes and dislikes. Liking is indicated by swiping right or clicking on a button with a tick, which is also highlighted in green when clicked - which might be always slightly green in the future based on user feedback. Dislike is indicated by swiping left or clicking on the button with an X, which is also highlighted in red when clicked.
We identified an ambiguity of our log in with other providers buttons as they might be mistaken as links to our social media presence instead of a login or registration method. The standard convention is to display other providers as a list including explanatory text, as shown in figure below on example of Strava.

Standard (Strava)           |  Our app
:-------------------------:|:-------------------------:
![Strava](./images/login_providers.jpg) | ![Login before](./images/login_before.png)

When selecting a hobby, we simply highlight it, making the state visible and the information simple (shown on a figure below). The save button is in the top right corner and is always visible when scrolling down the activity.
As described above, we do not use any special or original techniques. All interactions are simple and do not distinguish our application from other standard conventions.

![Hobbies selection](./images/hobbies_selection.png)

### #5: Error prevention

In our registration form, we are highlighting fields that are not correctly filled out once the user clicks submit, so that the user cannot perform a registration (network request) if something is not entered correctly as of the front end's knowledge. This might be adapted to also validate the input once the user starts typing or leaves the field again.

### #6: Recognition rather than recall

We believe that the flow of the application is so simple that user does not have to remember any information from one part of the interface to another. Everything they need to use the interface is visible all the time. We show the labels to forms even when filled out and show the instructions until completed.

### #7: Flexibility and efficiency of use

We do not provide any shortcuts or options to customize the way the application works. We believe this is not necessary for the current flow. We customise the content not the interface that is presented to the user. Currently the user selects their interests at the beginning and then we show activities related to the selected interests. In the future we plan to implement a recommendation system that will take care of the fully personalised content.
The swiping could however be considered an accelerator as someone who has never used a swipe-able interface before might rather click the buttons and the card rather that swipe in the right direction.

### #8: Aesthetic and minimalist design

Our app has a fairly minimalist design. Displayed content is held at the necessary minimum and should not overwhelm which was confirmed during user testings. However, we identified some minor points that definitely need improvement, such as the size of elements (buttons, checkboxes), font sizes, colours, and element locations.

### #9: Help users recognize, diagnose, and recover from errors

Error messages are currently only displayed during registration or login. The error during registration that is displayed may not be ideal. The reason for failure is not shown, which would certainly help the user. Besides, the content of the error messages is clear and definitely not technical - no error codes are shown.
Furthermore, we are planning on showing the reason why an action failed. In the future we might even show the errors provided by the back end directly with the inputs.

![Registration failed](./images/registration_failed.png)

![Registration successful](./images/registration_successful_message.png)

### #10: Help and documentation

We currently do not provide any form of documentation or user support. However, we have previously thought about an in-app interactive tutorial which might assist the user. But as the interface is rather minimalistic and self-explanatory it has not been the biggest priority until now.

## Creating issues (based on identified problems)

Taking into account the analysis carried out, we created the following issues, which were added to our backlog.

### #84 Web build does not work on mobile devices

#### Problem

When opening the web build of the app on a mobile device it looks wrong and is not interactable.

#### Screenshots

| Before          |  Target       |
:-------------------------:|:-------------------------:
| ![Before #84](./images/issues/84-before.png) | ![Target #84](./images/issues/84-target.png) |

### #72 Web app shell

#### Problem

Provide a shell in which the app should load on the web. This shell shall restrict the size/aspect ratio so that it looks right.

#### Solution

Add a constraint on root level and center it to give it space to shrink. Additionally, a background is needed and the swiper has to be adapted to work with the constrained space.

#### Screenshots

**Before**:
![#72 Before](images/issues/72-before.png)

**Target**:
![#72 Target](images/issues/72-target.png)

### #71 Stay logged in Problem

#### Problem

Once the user reloads the page / reopens the app, they are logged out and need to log in again.

#### Solution

Save the auth token encrypted on native devices and in the localStorage on the web. Furthermore, it needs to be checked on app initialisation.

### #69 Logout

#### Problem

The user cannot log out unless refreshing the page which shall not be possible in the future (see [#71](#71-stay-logged-in-problem)). Furthermore, the valid tokens remain active on the server.

#### Solution

Add a logout button, call the logout endpoint on the backend, and remove all local data.

#### Screenshots

**Before**:
![#69 Before](images/issues/69-before.png)

**Target**:
![#69 Target](images/issues/69-target.png)

### #74 #75 Undo rating

#### Problem

When the user rates an item they cannot go back. Which might leave the users with pressure of making the right choice.

#### Solution

Save the ID of the last rating locally and once the user clicks on undo the delete rating endpoint on the back end is called. For this the back end has to have a delete rating endpoint and the front end needs to have an undo button including design for it.

## Prioritizing issues

**Prioritised Issues**:

1. Web build does not work on mobile devices #84
2. Stay logged in #71
3. Logout #69
4. Undo rating #74 + #75
5. Web app shell #72

In order to correctly prioritise the detected problems, we created a prioritization matrix (we choose "complexity/effort vs impact/value", shown on a picture below). Since the workshop lasted only one day, we had to focus on "quick wins" - low effort and high impact for the user.

![Prioritization matrix](./images/matrix_prioritization.jpg)

## What was implemented during the workshop

### Web build does not work on mobile devices [#84](https://github.com/leisure-time-corp/leisure-time/issues/84)

The web build on mobile was broken due to framework internals. The default render engine behaves differently on all devices and does not seem to work on some as a consequence. To solve this issue we locked the render engine to one that works across all devices.

### Stay logged in [#71](https://github.com/leisure-time-corp/leisure-time/issues/71)

To solve this issue we created a key value store abstraction that handles the encrypted storage on native devices and localStorage on the web. Then we added a global token which is populated on start up when possible or during the login process if not. Furthermore, we added the possibility of guarding routes on the front end so that the user can only access the ones they should be able to.

### Logout [#69](https://github.com/leisure-time-corp/leisure-time/issues/69)

This was solved by adding a function that remove the token from the storage abstraction once the user clicks logout or when the back end indicates that the authentication token is no longer valid.

### Style changes

Instead using default Flutter button. Font size of the button text was made bigger and insets (padding) were added around.

```dart
padding: EdgeInsets.all(10.0),
child: Text('Sign Up', style: TextStyle(fontSize: 25))));
```

<center> Login page </center>

Before        |  After
:-------------------------:|:-------------------------:
![Before login page](./images/login_before.png) | ![After login page](./images/login_after.png)

<center> Registration page </center> 

| Before        |  After |
| :-------------------------:|:-------------------------: |
| ![Before reg page](./images/registration_form_before.png) | ![After reg page](./images/registration_form_after.png) |

## Identified as unnecessary

### Web app shell #72

Since the app is primarily intended for use on mobile devices and not in a web browser and there does not seem to be a "clean" way to reduce the size of the app without breaking core functionality, we considered this issue to be not worth the effort for now.
  
## What is yet to be implemented

<!-- TODO: is it really real life? -->
As we described earlier, we want to change the way we log in to stick to the "real-world" convention (as shown in the Strava example). We also plan on showing more precise error messages and have overall better error handling.

## Summary

Before the workshop we analysed our UI/UX in depth and identified the strengths and weaknesses of our application. From these weaknesses, we created issues that we considered to be the most critical. During the one-day workshop, we focused on "quick-wins", i.e. solutions that can bring the most value to our users while not requiring a lot of work. We were able to implement most of these and also identified a few additional flaws. The work on our UI/UX is certainly not over and we will continue to work to provide the most delightful and enjoyable experience we can.
