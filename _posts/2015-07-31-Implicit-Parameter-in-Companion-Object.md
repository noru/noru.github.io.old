---
layout: post
title: Implicit Parameter in Companion Object
tags: scala implicit
categories: scala
---

When I read the Implicit section in Scala in Depth I was really impressed by what this mechanism can do. After I read a part says companion object is a part of the implicity scope, I tried to write code as such

    object SomeObj {
        implicit val para = 1
    }

    class SomeObj {
        def foo(implicit i : Int) = i.toString
    }

    I was expecting something like:

    val obj = new SomeObj
    obj.foo   // Oppps!

Instead of returning a string of 1, an error was thrown says implicit parameter cannot be found. To make this work, I have to `import SomeOjb._` explicitly.

### Why???

After investigation, I found that I had misinterpreted the book here.

SLS says:

>The actual arguments that are eligible to be passed to an implicit parameter of type T fall into two categories. First, eligible are all identiﬁers x that can be accessed at the point of the method call without a preﬁx and that denote an implicit deﬁnition (§7.1) or an implicit parameter. An eligible identiﬁermay thus be a local name, or a member of an enclosing template, or it may be have been made accessible without a preﬁx through an import clause (§4.7). If there are no eligible identiﬁers under this rule, then, second, eligible are also all implicit members of some object that belongs to the implicit scope of the implicit parameter’s type, T.

That means the compiler will try to resolve the parameter from the companion object of the parameter type T. Not the way I was thinking of. In my case, that will be the companion object of Int(if there's one)

The correct example should be:

    object SomeObj {
        implicit val defaultSomeObj = new SomeObj("companion")
    }
    class SomeObj(s: String) {
        if (s == null) println("original") else println(s)
    }

    object whatever {
        def test(implicit o: SomeObj) = println("whatever calls its method")
    }

Run it:

    scala> whatever.test
    companion
    whatever calls its method

    scala> whatever.test(new SomeObj("new"))
    new
    whatever calls its method

That make all the sense in the world~
