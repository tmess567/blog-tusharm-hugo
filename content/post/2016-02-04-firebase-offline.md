---
title: Firebase Offline
author: tusharm
type: post
date: 2016-02-04T09:16:38+00:00
url: /?p=49
image: /wp-content/uploads/2016/02/firebase-1200x630.png
categories:
  - Firebase
tags:
  - Firebase

---
I recently took up a project where I needed to store some structured data and provide the user with a UI to insert view and edit the data in a streamlined way.

&nbsp;

At first I tried to use a **MySQL database**, but it was too much work. Also I didn&#8217;t know the limits of the data they could enter so defining data types was a chore as well.

&nbsp;

So I switched to **Firebase**, a company that provides a real time json database and application hosting space. Everything was going well when the client said that they required the application to work offline as well. Firebase works offline for Android and IOS applications but this functionality is not available for Web Applications.

&nbsp;

The application I need to create isn&#8217;t real-time so I thought what if I created some scripts to write the data to a local json. Seems like a completely simple solution for now but it really isn&#8217;t.

&nbsp;

The json needs to be shared amongst various users and so not only would I have to host a custom json file with it&#8217;s getter and setter php scripts online, but I would also have to maintain the synchronization of the data the user enters.

&nbsp;

So what if I used the firebase hosting and create the synchronization scripts myself. All I would need to do in this case is

1. When user enters or edits data while offline, save the data in a local json file.

2. Keep a local copy of the data for whenever the user needs to view or edit it.

3. Whenever the user connects to the internet, upload the objects stored in the local json file.
