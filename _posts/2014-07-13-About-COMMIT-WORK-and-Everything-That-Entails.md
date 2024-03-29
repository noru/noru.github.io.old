---
layout: post
title: About COMMIT WORK and Everything That Entails
tagline: 
tags: ABAP COMMIT_WORK LUW SAP_LUW
categories: ABAP
---

I can't remember when and why I use the statement `COMMIT WORK` for the first time, however I do know that I was being an epigone when I used it. I, like a lot of my colleagues I believe, seldom perform DB actions other than read. Even when I do have insert/update without existing API, I would not come out of using this statement myself. To me, using `COMMIT WORK` is merely a mysterious custom just like drop something on the ground, I never bother to ask why it did not go straight up to the sky. Funny thing is, I'm not alone.   

---   

Until someday we were told to remove all `COMMIT WORK` statement in our code and no one provided a solid reason. The most acceptable reason is regarding performance. I don’t think it’s cogent. Since when a suppose-to-be commit may cause a performance issue? Even if it does, it won’t be a huge impact (not huge enough to involve people on level that high). So I started pressing F1 and doing my delayed homework.    

---   

To understand `COMMIT WORK` there is a couple of prerequisites:      

>  - 	__LUW__ (Logical Unit of Work, A.K.A Database Transaction), including:      
>> <a href="http://help.sap.com/saphelp_nw04s/helpdata/en/41/7af4bca79e11d1950f0000e82de14a/content.htm"> DB LUW</a>      
>> <a href="http://help.sap.com/saphelp_47x200/helpdata/en/41/7af4bfa79e11d1950f0000e82de14a/content.htm"> SAP LUW</a>
   
> -  And one of its most important propositions: __“All or Nothing”__.      
   
---
After went through some documents, I found that the `COMMIT WORK` statement is a part of SAP LUW, it closes the current SAP LUW and opens a new one.      

Here comes the first reason why we shall not use this statement:   

### - REASON 1:  In SAP system, database commits and rollbacks can be triggered implicitly.   
---   
   
That is, when implicit database commit happened, you don’t have to call explicit database commits such as `COMMIT WORK` or function module `DB_COMMIT( )`(unlike `COMMIT WORK`, this FM performs a sole task of commit without triggering other tasks, refer to documentation).    
   
 One of the situation that triggers an implicit commit is:     

<pre>HTTP/HTTPS/SMTP communication executed using the Internet Communication Framework    
</pre>
   
Which fits our Odata case I presume. I do try to skip all the `COMMIT WORK`s (mentioned in <a href="https://jam4.sapjam.com/blogs/show/HZa74OUDc0HMHcfHSaqWku">this blog</a>) and it also works fine.     

---   

Until now I still don't have a tangible answer for everything seems fine with or without `COMMIT WORK`. After that I did a little <a href="http://noru.github.io/assets/image/commit.jpg">experiment</a>, and still can't find what I want. Then a word called “All or Nothing” comes into my mind.     

Quote from <a href="http://en.wikipedia.org/wiki/Database_transaction">Wikipedia</a>.:   
   
<pre> Transactions provide an "all-or-nothing" proposition, stating that each work-unit performed in a database must either  complete in its entirety or have no effect whatsoever. Further, the system must isolate each transaction from other transactions, results must conform to existing constraints in the database, and transactions that complete successfully must get written to durable storage.</pre>


Then I started to realize that it may be the reason:   

### -   REASON 2:  Explicit Commits may be a violation of “All or Nothing”.   
---   

The service framework of OData has already included us in a SAP LUW and provided an explicit commit on a higher level. If we do it again, there will be no chance to roll back to the original status where the transaction begins.    

---   

I’d believe this is more persuasive than the ‘Performance’ or the first reason. However I still don’t have the whole picture of it and my conclusion may not precise.  May experts can give a thorough explanation about it. And the lesson I learnt is (also my suggetstion):   


> -   __DO NOT use ‘COMMIT WORK’ unless you’re introducing a SAP LUW in your project.__   


---   
> Appendix:    
> ![screenshot]({{ site.url }}/assets/image/commit.jpg)
