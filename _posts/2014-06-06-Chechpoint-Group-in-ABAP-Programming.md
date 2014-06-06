---
layout: post
title: Checkpoint Group in ABAP Programming
tagline: powerful friend of robust & efficient programming in ABAP
tags: ABAP debugging
categories: ABAP
---

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
