---
title: Structure of Voice based query interface for database
author: tusharm
type: post
date: 2016-09-30T07:56:47+00:00
url: /?p=221
image: /wp-content/uploads/2016/04/rsz_wallhaven-3382571-1200x656.png
categories:
  - Voice based query interface for database
tags:
  - based
  - database
  - interface
  - parsey mcparseface
  - query
  - stt
  - syntaxnet
  - tensorflow
  - Voice
  - web speech api

---
Before I start building up the server for the application, I wanted to pen down the structure for the app. The structure is represented below.

**Abbreviations:**

  * WSA: Web Speech API (Speech to Text)
  * NLP: Natural Language Processing Tool (Syntaxnet or Google Cloud NLP API)
  * DIS: Database Indexed Search
  * DDI: Database Dynamic Indexing
  * DES: Database Exhaustive Search
  * NES: NoSQL Database Elastic Search
  * SFT: SQL Database Full Text Search

<img class=" wp-image-222 aligncenter" src="https://i0.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/09/Struct.png?resize=500%2C718" alt="struct" srcset="https://i0.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/09/Struct.png?resize=209%2C300 209w, https://i0.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/09/Struct.png?resize=370%2C530 370w, https://i0.wp.com/blog.tusharmishra.in/wp-content/uploads/2016/09/Struct.png?w=651 651w" sizes="(max-width: 500px) 100vw, 500px" data-recalc-dims="1" />

&nbsp;

### Server Decisions

  * Server will be built on node js (express js) as of now. Node JS is capable of forking processes to run shell commands on the server and evoke output. A barebones express js server will allow the app to be small, quick and efficient.
  * The server needs to be a VPS with some minimum requirements to support syntaxnet if that is chosen. If we use the Google Cloud NLP API all the way, we will still need a google cloud instance.
