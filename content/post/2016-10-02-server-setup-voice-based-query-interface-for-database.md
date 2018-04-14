---
title: 'Server Setup: Voice based query interface for database'
author: tusharm
type: post
date: 2016-10-02T19:38:35+00:00
url: /?p=225
image: /wp-content/uploads/2016/10/LI64Q1475437605.jpg
categories:
  - Voice based query interface for database
tags:
  - based
  - database
  - express
  - interface
  - js
  - node
  - nodejs
  - npm
  - packet
  - parsey mcparseface
  - query
  - server
  - stt
  - syntaxnet
  - tensorflow
  - Voice
  - web speech api

---
For now, I have chosen packet for the trial server even though the cost is high. The specs are good (even for entry level containers) and I got some credits to work with initially.

<img class="alignnone size-medium wp-image-226 aligncenter" src="https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/10/Screenshot-from-2016-10-03-00-23-22.png?resize=300%2C186" alt="Packet Server Config" srcset="https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/10/Screenshot-from-2016-10-03-00-23-22.png?resize=300%2C186 300w, https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/10/Screenshot-from-2016-10-03-00-23-22.png?w=309 309w" sizes="(max-width: 300px) 100vw, 300px" data-recalc-dims="1" />

So I setup the ssh keys for login and got to work.

The github repository for parsey mcparseface and syntaxnet is available [here][1] and it also lists out the steps required to setup syntaxnet and get it working. They also provide a demo shell script file which accepts the input at stdin and passes it to a python script named parser_eval. The output which is an ascii tree of the pos tagged statement is posted to stdout.

<img class="alignnone size-medium wp-image-227 aligncenter" src="https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/10/Screenshot-from-2016-10-03-00-27-59.png?resize=300%2C117" alt="ASCII Tree of POS tagged statement" srcset="https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/10/Screenshot-from-2016-10-03-00-27-59.png?resize=300%2C117 300w, https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/10/Screenshot-from-2016-10-03-00-27-59.png?resize=370%2C144 370w, https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/10/Screenshot-from-2016-10-03-00-27-59.png?w=439 439w" sizes="(max-width: 300px) 100vw, 300px" data-recalc-dims="1" />

Moving on, lets create a bare bones node js express server. [Express Generator][2] setup the basic routing and layout things I wanted. However, the views are apparently written in Jade and not the age old HTML. This could be good if I write the layout myself, but I might have to cut some corners if I pick up a template from somewhere.

<img class="alignnone size-full wp-image-228 aligncenter" src="https://i0.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/10/Screenshot-from-2016-10-03-00-31-25.png?resize=295%2C254" alt="Welcome to Express" data-recalc-dims="1" />

  * Now, lets connect the above two things. Express generator creates a route named users which executes the users.js in the routes directory when called. I made use of this to accept the user input and pass it to a js script
  * Next I imported some libraries required to execute scripts onto the host environment.

> var util = require(&#8216;util&#8217;);
> 
> var exec = require(&#8216;child_process&#8217;).exec;

  * Then I wrote an exec command to send the user&#8217;s input to the demo.sh file and then send the stdout content back to the user.

> exec(&#8216;cd /root/models/syntaxnet && echo &#8220;&#8216;+req.query.query+'&#8221; | syntaxnet/demo.sh&#8217;,
> 
> function(error, stdout, stderr){
  
> console.log(&#8216;stdout: &#8216; + stdout);
  
> console.log(&#8216;stderr: &#8216; + stderr);
  
> if (error !== null) {
  
> console.log(&#8216;exec error: &#8216; + error);
  
> }
  
> res.send(stdout);
  
> });

  * Checking the execution of the script, I got the following result.

> Input: What are the symptoms of cancer ? Parse: What WP ROOT +&#8211; are VBP cop +&#8211; symptoms NNS nsubj | +&#8211; the DT det | +&#8211; of IN prep | +&#8211; cancer NN pobj +&#8211; ? . punct

As expected, except the output is in a single line. But that doesn&#8217;t really matter since we have to parse this on the server side before we output the queries to the user.

 [1]: https://github.com/tensorflow/models/tree/master/syntaxnet#configuring-the-python-scripts
 [2]: https://expressjs.com/en/starter/generator.html
