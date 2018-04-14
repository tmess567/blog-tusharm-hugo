---
title: GSoC 2016 Work Submission
author: tusharm
type: post
date: 2016-08-21T13:23:16+00:00
url: /?p=197
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
## <a href="http://blog.tusharmishra.in/?p=197" target="_blank">GSoC 2016 Work Submission</a>

As a part of the final evaluation, GSoC 2016 accepted students are required to provide a permanent link with details about the work done along with the documentation for that work. This post is for that content.

Here are the details about my GSoC 2016 project once again:

> **Title:** <a href="https://issues.apache.org/jira/browse/SYNCOPE-809" target="_blank">Apache SYNCOPE-809</a>
> 
> **ORGANIZATION**
  
> <a href="http://www.apache.org/" target="_blank">Apache Software Foundation</a>
> 
> **MENTOR**
  
> <a href="http://home.apache.org/~ilgrosso/" target="_blank">Francesco Chicchiriccò</a>
> 
> **Description:**
> 
> The SYNCOPE-809 feature request points out the lack of a plugin for IDEs to allow users to create and edit mail templates and report stylesheets in the IDE itself instead of doing so using their dashboard. The feature request also provides a sample layout for the plugin where the mail and report templates are listed in a tree layout and made available for the user to view, edit and create new ones. The aim of this project will be to build a plugin that will solve the aforementioned problem and host it on the server so that end users can easily access and install the plugin on their own installation of eclipse and deployment of syncope.
> 
> &nbsp;

The project was added to the Apache Syncope repository in the form of Pull Requests. Since the entire project is mirrored to github, here is a link to the contributions I made to the project.

### <a href="https://github.com/apache/syncope/commits?author=tmess567" target="_blank">Link to Contributions</a>

Also, I maintained a blog throughout the project outlining the details of the code that was written. This would help future developers to better understand the code and easily modify it to meet future requirement. Here is a link to the list of posts relating to this project.

### <a href="http://blog.tusharmishra.in/?cat=2" target="_blank">Link to Blog Posts</a>

The project is complete as in all the milestones set in the GSoC 2016 proposal have been reached. An improvement still remains undone which is to automate the testing of the editors using swtbot.

I also made some contributions to the syncope code apart from my GSoC 2016 project which also listed in the contributions link above. They are:

  * Linked NumberWidgets on Dashboard (<a href="https://issues.apache.org/jira/browse/SYNCOPE-871" target="_blank">SYNCOPE-871</a>)
  * Added Exception for existing key (<a href="https://issues.apache.org/jira/browse/SYNCOPE-866" target="_blank">SYNCOPE-866</a>)
  * Corrected misspells and also added content to the Using the Admin Console section for the reference guide (<a href="https://issues.apache.org/jira/browse/SYNCOPE-700" target="_blank">SYNCOPE-700</a>)

I plan to continue working with the Apache Syncope community to fix some other issues or bugs, but mainly to help them complete the implementation of the Netbeans plugin.
