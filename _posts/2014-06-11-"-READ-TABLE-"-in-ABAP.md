---
layout: post
title: "READ TABLE" Statement in ABAP
tagline: 
tags: ABAP tips READ_TABLE
categories: ABAP
---


Using TCode **SAAB**, one can create a new checkpoint group(with namespace maybe), activate 3 kinds of check point:

> Breakpoints    
> Logpoints    
> Assertions.  

and manage(check/delete) log records.  
On ABAP side, insert the checkpoint like this:

`BREAK-POINT ID Z_DREW_CPG.`  
`LOG-POINT ID Z_DREW_CPG SUBKEY 'drew' FIELDS 'f1' 'f2'.`  
`ASSERT ID Z_DREW_CPG SUBKEY 'drew' FIELDS 'f3' CONDITION 1 = 2.`  

After activation, these checkpoints will take effect and help you lock down the trouble maker easily.  
