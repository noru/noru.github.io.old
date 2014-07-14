---
layout: post
title: About COMMIT WORK and Everything That Entails
tagline: 
tags: ABAP COMMIT_WORK LUW SAP_LUW
categories: ABAP
---

I can't remember when and why I use the statement `COMMIT WORK` for the first time, however I do know that I was being an epigone when I used it. I, like a lot of my colleagues I believe, seldem perform DB actions other than read. Even when I do have insert/update without existing API, I would not come out of using this statment myself. To me, using `COMMIT WORK` is merely a mysterious custom just like drop something on the ground, I never bother to ask why it did not go straight up. Funny thing is, I'm not alone.

Until someday we were told to remove all `COMMIT WORK` statement in our code, the bell was rung. 

When I just joint SAP and became a ABAPer, I longed for a Logging/Issue Tracking mechanism. Saddly I only got it after I read 
<a href="http://scn.sap.com/community/abap/testing-and-troubleshooting/blog/2011/11/09/checkpoint-group-the-powerful-friend-of-every-abaper-but-beware">this article</a>.

Using TCode **SAAB**, one can create a new checkpoint group(with namespace maybe), activate 3 kinds of check point:

> Breakpoints    
> Logpoints    
> Assertions.  

and manage(check/delete) log records.  
![screenshot]({{ site.url }}/assets/image/SAAB.jpg)

On ABAP side, insert the checkpoint like this:

`BREAK-POINT ID Z_DREW_CPG.`  
`LOG-POINT ID Z_DREW_CPG SUBKEY 'drew' FIELDS 'f1' 'f2'.`  
`ASSERT ID Z_DREW_CPG SUBKEY 'drew' FIELDS 'f3' CONDITION 1 = 2.`  

After activation, these checkpoints will take effect and help you lock down the trouble maker easily.  

---
PS： the Log problem mentioned in that artical is no longer an issue for newest __SAAB__ got the activation period feature, that is, automatically turn off after that. And there is another TCode to manage log __SRTM__.
