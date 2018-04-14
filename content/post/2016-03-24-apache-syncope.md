---
title: Apache SYNCOPE
author: tusharm
type: post
date: 2016-03-24T11:47:04+00:00
url: /?p=65
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

# **Introduction**

<span style="font-weight: 400;">Apache syncope is an identity management system which essentially means that it allows enterprises to maintain information and credentials for their employees in an organized and efficient way. It is a real world solution for a pressing problem.</span>

<span style="font-weight: 400;">Apache Syncope is an Open Source system for managing digital identities in enterprise environments, implemented in Java EE technology and released under Apache 2.0 license.</span><span style="font-weight: 400;"><br /> </span><span style="font-weight: 400;"><br /> </span><span style="font-weight: 400;">Identity management (or IdM) means to manage data on systems and applications, using the combination of business processes and IT.</span>

<span style="font-weight: 400;">Suppose an employee at an organization has competed a project and is asssigned a new one. The organization&#8217;s resource manager needs to </span>

  1.  <span style="font-weight: 400;">Revoke access to the completed projects resources. </span>
  2.  <span style="font-weight: 400;">Provide access to the resources of the new project.</span>

<span style="font-weight: 400;">This process can be simplified by deploying syncope on a local server and managing the resources through it.</span>

### How I came to know about it.

<span style="font-weight: 400;">I was looking at prospective organizations and proposed projects for GSOC when I came across this project and it instantly caught my eye. Open source projects are generally initiated to “scratch a developer&#8217;s itch” and this project send to be just that. It is a common problem a among various organizations and needs to be solved ASAP to prevent any further wastage of time on such trivial problems.</span>

### How it works

<span style="font-weight: 400;">The administrator is expected to install and run a server if syncope on the local intranet. His roles include managing the server, adding users and provisioning resources to the users. He can do this both the web based dashboard and a CLI tool. The end users can self register on the syncope server and self service.</span>

<span style="font-weight: 400;">Steps involved in installing syncope on a system are defined <a href="http://syncope.apache.org/docs/getting-started.html">here</a>. I would suggest using the maven way of installation as it allows you better access to log and configuration files which ensures better control over the deployment. </span><span style="font-weight: 400;">Once installed, the admin can login to the syncope console and create or edit users and resources.</span>
