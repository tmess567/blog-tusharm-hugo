---
title: Firebase Offline 1.0
author: tusharm
type: post
date: 2016-02-05T14:45:32+00:00
url: /?p=54
categories:
  - Firebase
tags:
  - Firebase

---
Recently I [published a post][1] where I explained why I needed to create some synchronization scripts for a web application that uses Firebase as a Database.

As stated in the previous post, there are 3 parts to this endeavor.

I will be planning out the first one in this post.

&nbsp;

&nbsp;

### 1. When user enters or edits data while offline, save the data in a local json file.

So, Firebase allows the users 4 ways to enter data into the database. [(Refer to this page) ][2]

  * **set()** : Allows the user to write json object/array to a particular location / url regardless of what was there before
  * **update() **: Allows the user to change values of keys at the particular location / url
  * **push()** : Generates a chronological key for each entry and adds it to the defined location / url
  * **transaction()** : Used when concurrency issues are faced. Not required for our use case.

&nbsp;

  * The first part is pretty simple. Since the set() function changes the entire data, the json passed to it can be saved directly to the local file that we have stored. Once we have the network, we simply upload the entire file onto the path specified. One down 2 to go.
  * update() function takes a key value pair as a parameter. Fairly simple, we change the particular key &#8211; value pair in the local json file and save the changes list in a new local file. Once we have a network connection, we run multiple update queries one for each change. (This can be refined if we rewrite multiple changes to the same key &#8211; value pair instead of add new ones in the local change list)
  * The push() function needs some thinking. The ID generation is something we need to look deep into. [Here&#8217;s a link][3] to how the IDs are generated. As the link states,

> Push IDs are string identifiers that are generated client-side.

&nbsp;

So, it may be possible to fire up the push() function and get a fake push ID and then instead of pushing the new data, we could just set() it with the fake ID. Too much for today, let&#8217;s think about this in the next post.

 [1]: http://opensourcefever.netai.net/2016/02/04/firebase-offline/
 [2]: https://www.firebase.com/docs/web/guide/saving-data.html
 [3]: https://www.firebase.com/blog/2015-02-11-firebase-unique-identifiers.html
