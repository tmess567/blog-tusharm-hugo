---
title: 'Apache SYNCOPE Eclipse Plugin: Update #1'
author: tusharm
type: post
date: 2016-06-06T14:11:54+00:00
url: /?p=154
image: /wp-content/uploads/2016/03/wallhaven-2842171-1200x675.jpg
categories:
  - Apache SYNCOPE (GSOC Project)
tags:
  - apache
  - api
  - eclipse
  - google summer of code
  - gsoc
  - plugin
  - project
  - rest
  - syncope

---
## Progress Report

The <a href="https://github.com/tmess567/SYNCOPE-809" target="_blank">SYNCOPE-809</a> project is going as expected. There are new things that I now understand crystal clear (like maven) and there are things that I don’t yet understand very well (most of the source code of syncope). But here’s another update on the part of it that I have been assigned to build.

### What has been done since?

The Tree Viewer was built, but I still had to interface with the syncope deployment to fetch and send data to a user defined url. Here are the changes / additions I made to fulfill this requirement.

  * The TreeObjects for MailTemplate and ReportTemplate TreeParent are now fetched using the SyncopeClient library.
  * A login dialog appears on clicking the Login button which allows the user to specify the url for the syncope deployment and the username password combination to get access.
  * A loading dialog to inform the user that the keys are being fetched from the server while the UI is blocked to allow the updates to the TreeViewer.
  * The details entered in the login dialog are stored in the preferences of the eclipse instance. The username and password are stored for the particular workspace, whereas the deployment url is saved for the entire eclipse instance.
  * The entire project has been restructured to be able to build using maven. This was done with the help of Tycho to ensure that the project will be able to build under the project structure of syncope itself.

### What is still to be done?

  * An editor is to be added to allow the content of the templates to be edited and changed by the user.
  * Interface the editor with the SyncopeClient library to allow changes to be reflected in the deployment.
  * Move the entire project under the syncope project structure to allow it to be built with the source code of the base project.

Besides this, I created and solved an <a href="https://issues.apache.org/jira/browse/SYNCOPE-866" target="_blank">issue</a> with the MailTemplate and ReportTemplate logic which caused no exceptions to be raised on adding duplicate keys to the deployment.
