---
title: 'DLTC: End of Project'
author: tusharm
type: post
date: 2016-04-08T12:15:53+00:00
url: /?p=86
image: /wp-content/uploads/2016/04/wallhaven-224671-1200x675.png
categories:
  - Uncategorized

---
> <span style="font-weight: 400;">RECAP: </span>
> 
> &nbsp;
> 
> <span style="font-weight: 400;">I tried working on Firebase libraries that would allow a user to save a local snapshot of the data stored online and then access and amend it. However, javascript does not allow you to access or modify locally stored files (unless the user provides the location of the file as an HTML5 input).</span>

&nbsp;

<span style="font-weight: 400;">Since I had to complete the project within the deadline, I decided to build a JavaFX based application which would be able to access and modify online as well as offline data. The offline data in the application is stored in an sqlite database the location of which is predefined to be the home folder of whatever operating system the user is working on. Linux has a dedicated home folder for each user in the /home/<username> directory. In windows, the db file is saved in C:</span><span style="font-weight: 400;">Users<username>.</span>

&nbsp;

<span style="font-weight: 400;">The database is created if not available on the first running instance of the application. Once the application detects a network connection, the data from the firebase online resource is fetched and saved in the database. This is useful in this case since the data is not so large as to hog the traffic while being downloaded or uploaded. Once the user is satisfied with the insertions and updates made to the database, the application allows the user to upload the entire data to firebase directly. This is made possible by embedding javascript codes inside the application’s FXML controllers with the help of the ScriptEngine class.</span>

&nbsp;

<span style="font-weight: 400;">The source code has been uploaded to drive for now. I will upload it to github when I get the time for it. The project has been closed due to difference in my working hours and theirs. The source code will be transferred to another developer. Any updates that I receive, will be uploaded to this blog. </span>

> <span style="font-weight: 400;">Meanwhile I will try to browse around for a way to complete the goal of an offline web capable JSON database.</span>
