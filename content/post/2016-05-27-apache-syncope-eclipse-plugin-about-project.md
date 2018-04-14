---
title: 'Apache SYNCOPE Eclipse Plugin: About Project'
author: tusharm
type: post
date: 2016-05-27T08:56:41+00:00
url: /?p=121
image: /wp-content/uploads/2016/03/wallhaven-2842171-1200x675.jpg
categories:
  - Apache SYNCOPE (GSOC Project)
  - Uncategorized
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
##### Google Summer of Code (GSOC)

# <a href="https://syncope.apache.org/" target="_blank">Apache Syncope</a>

#### An Open Source Identity Management System

* * *

#### 

Ready for a new start? The community bonding period has ended and we have reached the most awaited Coding Period. Been waiting for this day since long and it is every bit as exciting as I imagined. Don&#8217;t yet know what I&#8217;m talking about? Well let me tell you! My proposal got accepted earlier and I am now a Google Summer of Code Student. Exciting right? Well let&#8217;s get back to business and talk about what&#8217;s been done and what&#8217;s to be done.

I&#8217;ve written about syncope before, not a lot about my proposal though. I picked up an issue from the Apache Syncope [issues list][1] and made up a proposal for the same. The idea was to create an Eclipse Plugin for editing and viewing email and report templates of the users. They had already provided a vision (sample image) of what they wanted the plugin to consist of. I&#8217;ve added the image below. The structure you see is called a Tree Viewer which is populated using TreeParent and TreeObject classes.

[<img class="aligncenter size-full wp-image-123" src="https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/05/apacheVisionPlugin.png?resize=178%2C138" alt="Apache's Vision for Plugin" data-recalc-dims="1" />][2]

Initial steps were simple yet took some looking around to figure out. I tried out my first eclipse plugins with the hello world popup and some other trivial stuff. Eventually stumbled upon the create a Plug-in with a view which essentially did most of the work itself. The boilerplate code included an Activator, plugin.xml file configured to instantiate the Activator on run and a View class which defined what the view would do.

 [1]: https://issues.apache.org/jira/browse/SYNCOPE-809?jql=project%20%3D%20SYNCOPE
 [2]: https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/05/apacheVisionPlugin.png
