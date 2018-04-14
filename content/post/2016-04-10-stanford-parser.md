---
title: 'Voice based query interface for database: Stanford Parser'
author: Pulkit Gupta
type: post
date: 2016-04-10T15:27:05+00:00
url: /?p=93
image: /wp-content/uploads/2016/04/rsz_wallhaven-3382571-1200x656.png
categories:
  - Voice based query interface for database

---
> A natural language parser is a program that works out the grammatical **structure of sentences**, for instance, which groups of words go together (as &#8220;phrases&#8221;) and which words are the **subject** or **object** of a verb.

Dan Klein wrote the original version of this parser and Christopher Manning helped him by his support code and linguistic grammar development.

> A Part-Of-Speech Tagger (POS Tagger) is a piece of software that reads text in some language and assigns parts of speech to each word (and other token), such as noun, verb, adjective, etc., although generally computational applications use more fine-grained POS tags like &#8216;noun-plural&#8217;.

Example:-

### Query

<div class="parserOutput">
  <em>Show me the Symptoms of Cancer</em>
</div>

### Tagging

<div class="parserOutputMonospace">
  <div>
    Show/VB    me/PRP    the/DT    Symptoms/NNPS    of/IN    Cancer/NNP
  </div>
</div>

<div>
</div>

> ### Alphabetical list of part-of-speech tags used :
> 
> <table border="0" cellspacing="2" cellpadding="2">
>   <tr align="none" bgcolor="#DFDFFF">
>     <td align="none">
>       <div align="left">
>         Number
>       </div>
>     </td>
>     
>     <td>
>       <div align="left">
>         Tag
>       </div>
>     </td>
>     
>     <td>
>       <div align="left">
>         Description
>       </div>
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       1.
>     </td>
>     
>     <td>
>       CC
>     </td>
>     
>     <td>
>       Coordinating conjunction
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       2.
>     </td>
>     
>     <td>
>       CD
>     </td>
>     
>     <td>
>       Cardinal number
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       3.
>     </td>
>     
>     <td>
>       DT
>     </td>
>     
>     <td>
>       Determiner
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       4.
>     </td>
>     
>     <td>
>       EX
>     </td>
>     
>     <td>
>       Existential <i>there</i>
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       5.
>     </td>
>     
>     <td>
>       FW
>     </td>
>     
>     <td>
>       Foreign word
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       6.
>     </td>
>     
>     <td>
>       IN
>     </td>
>     
>     <td>
>       Preposition or subordinating conjunction
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       7.
>     </td>
>     
>     <td>
>       JJ
>     </td>
>     
>     <td>
>       Adjective
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       8.
>     </td>
>     
>     <td>
>       JJR
>     </td>
>     
>     <td>
>       Adjective, comparative
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       9.
>     </td>
>     
>     <td>
>       JJS
>     </td>
>     
>     <td>
>       Adjective, superlative
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       10.
>     </td>
>     
>     <td>
>       LS
>     </td>
>     
>     <td>
>       List item marker
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       11.
>     </td>
>     
>     <td>
>       MD
>     </td>
>     
>     <td>
>       Modal
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       12.
>     </td>
>     
>     <td>
>       NN
>     </td>
>     
>     <td>
>       Noun, singular or mass
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       13.
>     </td>
>     
>     <td>
>       NNS
>     </td>
>     
>     <td>
>       Noun, plural
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       14.
>     </td>
>     
>     <td>
>       NNP
>     </td>
>     
>     <td>
>       Proper noun, singular
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       15.
>     </td>
>     
>     <td>
>       NNPS
>     </td>
>     
>     <td>
>       Proper noun, plural
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       16.
>     </td>
>     
>     <td>
>       PDT
>     </td>
>     
>     <td>
>       Predeterminer
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       17.
>     </td>
>     
>     <td>
>       POS
>     </td>
>     
>     <td>
>       Possessive ending
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       18.
>     </td>
>     
>     <td>
>       PRP
>     </td>
>     
>     <td>
>       Personal pronoun
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       19.
>     </td>
>     
>     <td>
>       PRP$
>     </td>
>     
>     <td>
>       Possessive pronoun
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       20.
>     </td>
>     
>     <td>
>       RB
>     </td>
>     
>     <td>
>       Adverb
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       21.
>     </td>
>     
>     <td>
>       RBR
>     </td>
>     
>     <td>
>       Adverb, comparative
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       22.
>     </td>
>     
>     <td>
>       RBS
>     </td>
>     
>     <td>
>       Adverb, superlative
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       23.
>     </td>
>     
>     <td>
>       RP
>     </td>
>     
>     <td>
>       Particle
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       24.
>     </td>
>     
>     <td>
>       SYM
>     </td>
>     
>     <td>
>       Symbol
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       25.
>     </td>
>     
>     <td>
>       TO
>     </td>
>     
>     <td>
>       <i>to</i>
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       26.
>     </td>
>     
>     <td>
>       UH
>     </td>
>     
>     <td>
>       Interjection
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       27.
>     </td>
>     
>     <td>
>       VB
>     </td>
>     
>     <td>
>       Verb, base form
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       28.
>     </td>
>     
>     <td>
>       VBD
>     </td>
>     
>     <td>
>       Verb, past tense
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       29.
>     </td>
>     
>     <td>
>       VBG
>     </td>
>     
>     <td>
>       Verb, gerund or present participle
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       30.
>     </td>
>     
>     <td>
>       VBN
>     </td>
>     
>     <td>
>       Verb, past participle
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       31.
>     </td>
>     
>     <td>
>       VBP
>     </td>
>     
>     <td>
>       Verb, non-3rd person singular present
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       32.
>     </td>
>     
>     <td>
>       VBZ
>     </td>
>     
>     <td>
>       Verb, 3rd person singular present
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       33.
>     </td>
>     
>     <td>
>       WDT
>     </td>
>     
>     <td>
>       Wh-determiner
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       34.
>     </td>
>     
>     <td>
>       WP
>     </td>
>     
>     <td>
>       Wh-pronoun
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       35.
>     </td>
>     
>     <td>
>       WP$
>     </td>
>     
>     <td>
>       Possessive wh-pronoun
>     </td>
>   </tr>
>   
>   <tr bgcolor="#FFFFCA">
>     <td align="none">
>       36.
>     </td>
>     
>     <td>
>       WRB
>     </td>
>     
>     <td>
>       Wh-adverb
>     </td>
>   </tr>
> </table>

We are categorizing/parsing these queries according to different grammatical phrases which in turn is helping us to easily recognize keywords that we are using to search from database. These keywords are then compared to the lexicons of the database which include the relation names, attributes and values available in the database.  The wh-word (query word) defines an operation in an SQL query such as Select and a noun of any form defines a keyword to be searched in the database. The rest of the tokens are used to describe a relation between them defining what the user is actually looking for.
