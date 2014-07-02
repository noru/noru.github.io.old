---
layout: post
title: Bitwise Operator in JS
tagline: you think you're a smartpants, huh?
tags: Javascript Tips Tricks Bitwise_Operator
categories: Javacript
---

I was sauntering on GitHub and ended up in [JSHint](https://github.com/rwaldron/idiomatic.js/), a static code analysis tool for JavaScript. When I was looking at the sample code in idomatic style I saw this:     
`!!~array.indexOf("a");`    
I was like, "WTF is this shit?". And its comment says its "__unnecessarily clever__".    
Slick trick? I dig that! Got to grasp it.    

`!!` turns something into boolean, that's no news. However it took me a while to remember `~`. It's bitwise operator in JavaScript, and C++, and Java. A bitwise NOT operator: trun every 1 to 0 of a number(binary-wise) and vice versa. Basically `~foo` means `-(foo + 1)`. ([Why is that?](https://en.wikipedia.org/wiki/Signed_number_representations#Signed_magnitude_representation))

Turns out the `!!~` is only another version of `something >=0`.  Huh, I got the "unnecessarily" means.

A little bit dispointed but still, a few awesome tricks about bitwise operators.

### Parses hexadecimal value to get RGB color values.

    var hex = 'ffaadd';   
    var rgb = parseInt(hex, 16);    
    
    var red   = (rgb >> 16) & 0xFF;   
    var green = (rgb >> 8) & 0xFF;     
    var blue  = rgb & 0xFF;   
    
### 2. Cluster Repository: Spread it out      
> Your space seems contin
   
### 3. Duplicated Data: Hash it, hash it, hash it!      
> They tricked you, in a good way though. Many users stored the very same data in there repository but it's only one (or numberable, I don't k
