---
title: 'Voice based query interface for database: Speech-to-Text'
author: Anmol Rastogi
type: post
date: 2016-04-12T06:37:04+00:00
url: /?p=112
image: /wp-content/uploads/2016/04/rsz_wallhaven-3382571-1200x656.png
categories:
  - Voice based query interface for database

---
Speech recognition and synthesis technology provides a natural interaction method for many computing tasks. It allows users to communicate with computers naturally using spoken language, requiring very little training. Although this technology has existed for several decades, it has recently become widely usable because of the increasing capabilities of consumer .

Benefits of Speech Interaction (in general):

  *  Improved interaction for people with disabilities.
  * Hands-free interaction with virtual reality and augmented reality applications.
  * Intuitive interaction: speech is natural for most people and requires little to no special training.

There are various other benefits of speech-to-text systems like Writing documents and email through dictation, etc.

For our project we initially used VOCE Java API which is a free and Open Source library that uses the LGPL and BSD licenses. It is cross platform as it uses FreeTTS and Sphnix which are written in Java. Voce is easily portable to platforms with Java virtual machine implementations. Voce itself is mostly written in Java with bindings for C++.

The problem we faced with VOCE implementation was that the result obtained was not accurate. Due to the ambient noises present around us the library could not differentiate between user&#8217;s voice and the noise and thus returned arbitrary results. Also, since we have Indian Accent the system could not understand our inputs properly.

After putting a lot of efforts trying to configure the Voce system we could not get resolve it. Therefore, after a lot of research we decided to switch to Google Web Speech API.

Google Web Speech API:

The Web Speech API, introduced at the end of 2012, allows web developers to provide speech input and text-to-speech output features in a web browser. Typically, these features aren’t available when using standard speech recognition or screen reader software. The Web Speech API defines a complex interface, called SpeechRecognition<code class=" language-undefined">.</code>

Since we are providing the users with an online interface to access our system, this javascript based library fits in perfectly. The user will open a webpage and click a button to start recording the input. The output from the web speech api will then be sent to the backend java based server where our actual system resides. The output can then be displayed on the page automatically.

Web Speech API is better than VOCE as it is supported by a wide grammar. Moreover it supports multiple accents, Thus the system had no problem recognizing our Indian Accent.
