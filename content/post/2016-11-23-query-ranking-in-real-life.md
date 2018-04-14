---
title: Query Ranking in Real Life (Part 1)
author: tusharm
type: post
date: 2016-11-23T18:28:14+00:00
url: /?p=233
image: /wp-content/uploads/2016/10/LI64Q1475437605.jpg
categories:
  - Uncategorized
  - Voice based query interface for database
tags:
  - api
  - based
  - database
  - express
  - interface
  - js
  - mcparseface
  - node
  - nodejs
  - npm
  - packet
  - parsey
  - query
  - server
  - speech
  - stt
  - syntaxnet
  - tensorflow
  - Voice
  - web

---
After a long delay I finally mustered up the courage to build the query ranking module. Some scary stuff. Here are the problems I&#8217;ve been facing whenever I start building this.

  * The ranking requires the table&#8217;s Foreign Key structure. Once the query generation is done, the recursive calls along with Javascript&#8217;s callbacks is a nightmare.
  * Callbacks are being received even after sending the output. Some relations between the tables are discovered even after ranking. This is troubling.
  * I tried to deal with promises but combined with the already scary ranking algorithm and multi-module structure this will just take more time than I have.

So I am switching to a new approach of this as suggested by a colleague.

  1. Get the foreign key structure before the server starts and prepare a searchable graph.
  2. Once the queries are generated, score them on the searchable graph in a sequential for loop.
  3. Minimize the use of callbacks as far as possible.

This [github repo][1] is the exact thing I need to make the graph searchable. Go Open Source and go NPM. Just add the package and you&#8217;ve got a working system.

 [1]: https://github.com/albertorestifo/node-dijkstra
