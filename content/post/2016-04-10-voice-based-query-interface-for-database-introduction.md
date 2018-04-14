---
title: 'Voice based query interface for database: Introduction'
author: tusharm
type: post
date: 2016-04-10T03:18:23+00:00
url: /?p=97
image: /wp-content/uploads/2016/04/rsz_wallhaven-3382571-1200x656.png
categories:
  - Voice based query interface for database

---
<span style="font-weight: 400;">As a part of our 2nd Minor Project, we decided to take up the topic: “<strong>Voice based query interface for database</strong>”. The aim of the project is to develop a system that takes a natural language statement as a voice (audio) input from the user and then convert it into a relevant query for a specific database.</span>

&nbsp;

## <span style="font-weight: 400;">What we are trying to solve</span>

&nbsp;

<span style="font-weight: 400;">In this project, we are trying to tackle the problem of learning and understanding a language before we are able to start working on projects concerning it. Often the primary way of solving a problem with a programming language is by finding a function in the API or documentation that is able to provide the desired output. However developers/users face the following issues in this procedure.</span>

&nbsp;

<li style="font-weight: 400;">
  <span style="font-weight: 400;">First, users must learn to cope with rigid and seemingly arbitrary syntax rules for formulating expressions. </span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Second, users must often learn several different scripting languages and be able to switch between them. </span>
</li>
<li style="font-weight: 400;">
  <span style="font-weight: 400;">Finally, users must learn the Application Programmer Interface (API) for the application they want to script, but API’s can be quite large and it can be difficult to isolate the portion of the API relevant to the current task.</span>
</li>

&nbsp;

### <span style="font-weight: 400;">Earlier Implementations</span>

<span style="font-weight: 400;">Fortunately, there are alternative approaches to this problem. </span>

> <span style="font-weight: 400;">Two notable approaches include programming by demonstration (PBD) and structured editors. </span>

<span style="font-weight: 400;">A PBD works by recording the user’s actions using a macro recorder. However, the programs generated can be arbitrary and is not the most efficient way of solving our issue. Structured editors can be a good approach for end users to write and edit scripts, since they force the script to retain a syntactically correct form. However, this approach retains the original problem that the user is expected to understand and learn a syntax (even though it is closer to natural language) and structure the command in a certain way which is comprehensible to the system.</span>

&nbsp;

### <span style="font-weight: 400;">Related Work</span>

<span style="font-weight: 400;">People have been interested in this field of natural language query generation since a long time. The 2003 paper “Towards a theory of natural language interfaces to databases” describes a system named PRECISE and some theoretical ways in which it could work. A more recent paper named “Program Synthesis using Natural Language” described a set of algorithms designed to solve natural language commands and queries for systems such as ATIS (Air Travel Information System) and Text Editing tools. </span>

> <span style="font-weight: 400;">A common hurdle such works face is the issue of context resolution. If a person asks a question, which relation does it correspond to.</span>

 <span style="font-weight: 400;">For example, if a person asks “Show me the Symptoms of Cancer”, obviously he/she is referring to a database with a name similar to “Disease” and a “Symptoms” attribute. However, if the person then asks “Who is the best doctor to consult for this.”, the system should be able to comprehend that the user wants a listing of (preferably nearby) doctors that specialize in cancer treatments.</span>

&nbsp;

<span style="font-weight: 400;">The systems mentioned above go around this problem by asking the user for further input. The PRECISE system asks the user to explain the query further if the confidence level of the generated queries is low. The Program Synthesis paper displays a ranked set of the queries to the user to choose the most appropriate one from.</span>
  
<span style="font-weight: 400;">Artificial assistants such as Google Now, Siri and Cortana also provide similar functionality except for the fact that they cannot be targeted to a local database and even so, the results they produced are based on the results of their respective search engines (Google and Bing) instead of focussing on directly accessing a structured set of data. </span>

> <span style="font-weight: 400;">A great feature in such systems though is context resolution.</span>
