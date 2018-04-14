---
title: Web Speech API Experimentation
author: tusharm
type: post
date: 2016-09-21T06:31:30+00:00
url: /?p=213
image: /wp-content/uploads/2016/10/LI64Q1475437605.jpg
categories:
  - Voice based query interface for database
tags:
  - api
  - browser
  - google
  - speech
  - speech to text
  - stt
  - text
  - web

---
Converting the Natural Language to Database Query project over to Javascript requires the implementation of the Web Speech API in a single Javascript file. I will discuss the steps taken for the integration in this blog post. Kinda unorthodox but here&#8217;s a reference before the content, if you want to experiment on Web Speech API using the <a href="https://developers.google.com/web/updates/2013/01/Voice-Driven-Web-Apps-Introduction-to-the-Web-Speech-API?hl=en" target="_blank">official guide</a>.

First we check if the API is available with the browser using the following code

> if (!(&#8216;webkitSpeechRecognition&#8217; in window)) { upgrade(); }

This checks for the webkitSpeechRecognition availability and if unavailable, asks the user to upgrade the browser. Next, accessing the API using a Javascript object.

> var recognition = new webkitSpeechRecognition();

Clearly this creates a recognition named object for the API using which we can access its functionality. Here&#8217;s the definition of the object received in the above statement.

> <span class="console-object-preview">SpeechRecognition {}</span>
> 
>   * <span class="name">continuous</span><span class="object-properties-section-separator">:</span><span class="value object-value-boolean">false</span>
>   * <span class="name">grammars</span><span class="object-properties-section-separator">:</span><span class="value object-value-object">SpeechGrammarList</span>
>   * <span class="name">interimResults</span><span class="object-properties-section-separator">:</span><span class="value object-value-boolean">false</span>
>   * <span class="name">lang</span><span class="object-properties-section-separator">:</span><span class="value object-value-string">&#8220;&#8221;</span>
>   * <span class="name">maxAlternatives</span><span class="object-properties-section-separator">:</span><span class="value object-value-number">1</span>
>   * <span class="name">onaudioend</span><span class="object-properties-section-separator">:</span><span class="value object-value-null">null</span>
>   * <span class="name">onaudiostart</span><span class="object-properties-section-separator">:</span><span class="value object-value-null">null</span>
>   * <span class="name">onend</span><span class="object-properties-section-separator">:</span><span class="value object-value-null">null</span>
>   * <span class="name">onerror</span><span class="object-properties-section-separator">:</span><span class="value object-value-null">null</span>
>   * <span class="name">onnomatch</span><span class="object-properties-section-separator">:</span><span class="value object-value-null">null</span>
>   * <span class="name">onresult</span><span class="object-properties-section-separator">:</span><span class="value object-value-null">null</span>
>   * <span class="name">onsoundend</span><span class="object-properties-section-separator">:</span><span class="value object-value-null">null</span>
>   * <span class="name">onsoundstart</span><span class="object-properties-section-separator">:</span><span class="value object-value-null">null</span>
>   * <span class="name">onspeechend</span><span class="object-properties-section-separator">:</span><span class="value object-value-null">null</span>
>   * <span class="name">onspeechstart</span><span class="object-properties-section-separator">:</span><span class="value object-value-null">null</span>
>   * <span class="name">onstart</span><span class="object-properties-section-separator">:</span><span class="value object-value-null">null</span>

Most of the attributes and the functions are clear about their role in their own name. But here&#8217;s a [reference][1] just in case.

So now let&#8217;s get the transcript for the recognized speech from the API.

> recognition.onresult = function(event) {console.log(event.results\[0\]\[0\].transcript);};

Then start the recognition using the following code.

> recognition.start();

PS: You&#8217;ll have to authorize the use of microphone by the webpage.

<img class=" wp-image-218 aligncenter" src="https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/09/Screenshot-from-2016-09-21-12-00-02.png?resize=699%2C163" alt="screenshot-from-2016-09-21-12-00-02" srcset="https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/09/Screenshot-from-2016-09-21-12-00-02.png?resize=300%2C70 300w, https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/09/Screenshot-from-2016-09-21-12-00-02.png?resize=768%2C180 768w, https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/09/Screenshot-from-2016-09-21-12-00-02.png?resize=370%2C87 370w, https://i1.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/09/Screenshot-from-2016-09-21-12-00-02.png?w=843 843w" sizes="(max-width: 699px) 100vw, 699px" data-recalc-dims="1" />

 [1]: https://dvcs.w3.org/hg/speech-api/raw-file/tip/speechapi.html
