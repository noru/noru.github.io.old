---
layout: post
title: About COMMIT WORK and Everything That Entails
tagline: 
tags: ABAP COMMIT_WORK LUW SAP_LUW
categories: ABAP
---

I can't remember when and why I use the statement `COMMIT WORK` for the first time, however I do know that I was being an epigone when I used it. I, like a lot of my colleagues I believe, seldom perform DB actions other than read. Even when I do have insert/update without existing API, I would not come out of using this statement myself. To me, using `COMMIT WORK` is merely a mysterious custom just like drop something on the ground, I never bother to ask why it did not go straight up. Funny thing is, I'm not alone.   

---   

Until someday we were told to remove all `COMMIT WORK` statement in our code and no one provided a solid reason. The most acceptable reason is regarding performance. I don’t think it’s cogent. Since when a suppose-to-be commit may cause a performance issue? Even if it does, it won’t be a huge impact(not huge enough to involve people on level that high). So I started pressing F1 and doing my delay homework.    

---   

To understand `COMMIT WORK` there is a couple of prerequisites:      

#### 	LUW(Logical Unit of Work, aka Database Transaction), including
   
> DB LUW      
> SAP LUW      

#### 	And one of its most important propositions: “All or Nothing”.      
   
---
After went through some documents, I found that the `COMMIT WORK` statement is a part of SAP LUW, it closes the current SAP LUW and opens a new one.      

Here comes the first reason we shall not use this statement:   

#### In SAP system, database commits and rollbacks can be triggered implicitly.   
   
That is, when implicit database commit happened, you don’t have to call explicit database commits such as `COMMIT WORK` or function module `DB_COMMIT( )`(unlike `COMMIT WORK`, this FM performs a sole task of commit without triggering other tasks, refer to documentation).    
   
 One of the situation that triggers an implicit commit is:     
 
#### HTTP/HTTPS/SMTP communication executed using the Internet Communication Framework    
   
Which fits our Odata case I presume. I do try to skip all the `COMMIT WORK`s(mentioned in <a href="https://jam4.sapjam.com/blogs/show/HZa74OUDc0HMHcfHSaqWku">this blog</a>) and it also works fine.     

---   

Until now I still have a tangible answer for everything seems fine with or without `COMMIT WORK`. After that I did a litter experiment, and still found what I want. Then a word called “All or Nothing” comes into my mind.     

Quote for <a href="http://en.wikipedia.org/wiki/Database_transaction">Wikipedia</a>.:
> Transactions provide an "all-or-nothing" proposition, stating that each work-unit performed in a database must either  complete in its entirety or have no effect whatsoever. Further, the system must isolate each transaction from other transactions, results must conform to existing constraints in the database, and transactions that complete successfully must get written to durable storage.


Then I started to realize that it may be the reason:   

#### Explicit Commits may be a violation of “All or Nothing”.   


The service framework of OData has already included us in a SAP LUW and provided an explicit commit on a higher level. If we do it again, there will be no chance to roll back to the original status where the transaction begins.    

---   

I’d believe this is more persuasive than the ‘Performance’ or the first reason. However I still don’t have the whole picture of it and my conclusion may not precise.  May experts can give a thorough explanation about it. And the lesson I learnt is(also my suggetstion):   

### Do not use ‘COMMIT WORK’ unless you’re creating a SAP LUW in your project.



