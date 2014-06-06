---
layout: post
title: Checkpoint Group in ABAP Programming
tagline: powerful friend of robust & efficient programming in ABAP
---

When I just joint SAP and became a ABAPer, I longed for a Logging/Issue Tracking mechanism. Saddly I only got it after I read 
<a href="http://scn.sap.com/community/abap/testing-and-troubleshooting/blog/2011/11/09/checkpoint-group-the-powerful-friend-of-every-abaper-but-beware">this article</a>.

Using TCode **SAAB**, one can create a new checkpoint group(with namespace maybe), activate 3 kinds of check point:
> Breakpoints
> Logpoints
> Assertions.

and check log records.

On ABAP side, insert the checkpoint:
'BREAK-POINT ID Z_DREW_CPG.'
'LOG-POINT ID Z_DREW_CPG SUBKEY 'drew' FIELDS 'f1' 'f2'.'
'ASSERT ID Z_DREW_CPG SUBKEY 'drew' FIELDS 'f3' CONDITION 1 = 2.'

### Header 3

> This is a blockquote.
> 
> This is the second paragraph in the blockquote.
>
> ## This is an H2 in a blockquote
