---
layout: post
title: Bitwise Operator in JavaScript
tagline: you think you're a smartpants, huh?
tags: JavaScript Tips Tricks Bitwise_Operator
categories: Javacript
---

I was sauntering on GitHub and ended up in [JSHint](https://github.com/rwaldron/idiomatic.js/), a static code analysis tool for JavaScript. When I was looking at the sample code in idomatic style I saw this:     
`!!~array.indexOf("a");`    
I was like, "WTF is this shit?". And its comment says its "__unnecessarily clever__".    
Slick trick? I dig that! Got to grasp it.    

`!!` turns something into boolean, that's no news. However it took me a while to remember `~`. It's bitwise operator in JavaScript, and C/C++, and Java. A bitwise NOT operator: trun every 1 to 0 of a number(binary-wise) and vice versa. Basically `~foo` means `-(foo + 1)`. ([Why is that?](https://en.wikipedia.org/wiki/Signed_number_representations#Signed_magnitude_representation))

Turns out the `!!~` is only another version of `something >= 0`.  Huh, I got the "unnecessarily" means.

A little bit dispointed but still, a few awesome tricks about bitwise operators.

-----   
> `~~`: __You want interger?__

`~~` is probably something like:   
                        <code>typeof foo === 'number' && !isNaN(foo) && foo !== Infinity
                        ? foo > 0 ? Math.floor(foo) : Math.ceil(foo) : 0;</code>

In sample form:
    `-(-(foo + 1) + 1)`
or briefly speaking: gives a int by any object, __in a lot faster way__, generally it can replace `Math.floor()`.
PS: Alternatively, ' | 0 '.

-----   
> __Parses hexadecimal value to get RGB color values.__
  

    var hex = 'ffaadd';   
    var rgb = parseInt(hex, 16);    
    
    var red   = (rgb >> 16) & 0xFF;   
    var green = (rgb >> 8) & 0xFF;     
    var blue  = rgb & 0xFF;   
    
this usage can be applied on a lot of cases I assume, such as IP address operations.
    
-----   
> __Toggle:__ `^`   

     

Used like `value ^= 1` will change on every call the value to 0, 1, 0, 1 ...
If we pass that value as a Statement into a Conditional operator (?:) like

`statement ? (if true) : (if false)`

-----   
> __Is Odd?__ `&1`   

 
   
1 = ...0000001, and every digits after the 1st digit got a "0" after the __&__ operation. So it is a fancy way to determine odd number.

-----   

I believe there are many other good example of using bitwise operators and I'll keep updating this thread. Their neat style and super effeciency are really attractable. Yeah, sometime a little brainfuck, but who couldn say that's not another advantage?


<pre>
<a class="statement">var </a>i <a class="operator">= </a> <a class="integer">100</a><a class="operator">;</a>
<a class="statement">var </a>i <a class="operator">= </a> <a class="integer">100</a><a class="operator">;</a>
</pre>




