---
layout: post
title: READ TABLE Statement in ABAP
tagline: usage and tips
tags: ABAP tips READ_TABLE
categories: ABAP
---

### `sy-tabix` is set!
(Boooo...) yeah, it is lame.

### No Structure? use `"table_line"`
It can be used as a general line type of an internal table. This is particularly useful for tables whose line type does not have a structure.

Example:

> DATA: wa   TYPE i,   
>      itab TYPE SORTED TABLE OF i WITH UNIQUE KEY TABLE_LINE.   
>...   
>LOOP AT itab INTO wa WHERE KEY table_line > 5.   
>  ...   
>ENDLOOP.   

There is something more. If the internal table is of object references. The associated class has an attribute NAME. You can access this attribute by specifying `TABLE_LINE->NAME` in a `READ TABLE`/`LOOP` statement.


### Alternative: Table Expressions!
A table expression reads a row from an internal table and returns it as a result.
Syntax `... itab[ itab_line ] ... `

No major difference compare to `READ TABLE`. However it is more concise and and can be used within functions like `line_exists` & `line_index`, and with operands. Plus, unlike `READ TABLE`, it does not set `sy-tabix`.
