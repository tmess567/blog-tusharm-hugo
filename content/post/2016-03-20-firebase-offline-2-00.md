---
title: Firebase Offline 2.00
author: tusharm
type: post
date: 2016-03-20T05:26:46+00:00
url: /?p=58
categories:
  - Firebase
tags:
  - Firebase

---
In a recent post I explained how wee could theoretically save user&#8217;s data onto a local file which could then be synced to the Firebase database online. As i ventured further into the idea, I realized that JS doesn&#8217;t really allow you to read a file on the local system of the user.

I was a little frustrated after reading about 5 posts on StackOverflow stating how it would be &#8220;Invasion of Privacy&#8221; if we could do that but I realized that what they were posting was absolutely valid.

So, how do we build an offline app that could sync with an online JSON database. Since our problem is with reading offline files, let&#8217;s figure that out first. An obvious solution would be to build a native application that can connect with an online database. Problem is I don&#8217;t have enough time to learn how to and then build a native application.

But let&#8217;s say I had enough time, what would I need.

  1. A PHP file that spits out the JSON as an output every time it is called and also can accept a JSON file which it will be capable of replacing with the older version available in the server.
  2. A link that runs a JS script to generate the push keys.

> The last post stated a way to generate a fake Firebase push ID and then use it to create a ney key value pair, add it to the local file and set the JSON online. However upon looking deeper into the Google results, I found the JS script that allows us to generate the keys in a genuine way even locally.
