---
layout: post
title:  "Why Clojure is a better Java"
date:   2017-12-19 
categories: clojure, java
---

#### Less need for Naming Things ####

[Naming things is hard](https://www.martinfowler.com/bliki/TwoHardThings.html).  In OO Design, a lot of time can be spent working out the right names for your classes and their associated contents.  With Clojure we don't need to define as many classes.  

Where possible, maps, lists and vectors are used for our data structures, only resorting to using "defrecord" and "deftype" on occasion (Chas Emerick made a [flowchart](https://cemerick.com/2011/07/05/flowchart-for-choosing-the-right-clojure-type-definition-form) to help decide when you would need to use defrecord, deftype or even reify).  So no more class proliferation, having to define java beans for your [DTOs](https://www.martinfowler.com/eaaCatalog/dataTransferObject.html), [Value Objects](https://www.martinfowler.com/eaaCatalog/valueObject.html), and/or your [anaemic domain model](https://www.martinfowler.com/bliki/AnemicDomainModel.html)/entities.  And no need for [Lombok](https://projectlombok.org/)!  

Along with the core data structures, the core clojure functions are typically all you need to manipulate those structures - the [clojure cheatsheet](https://clojure.org/api/cheatsheet) is your first port of call when implementing new functionality.  When using higher order functions such as map and reduce, we can often define short anonymous functions to apply, further reducing the need for naming. 

#### Less Need for GoF Design Patterns ####

Certain design problems come up time and again such that common design solutions exist for them.  These are the design patterns, of which the GoF Patterns are the most famous.  [Functional Programming Patterns in Scala and Clojure](https://pragprog.com/book/mbfpp/functional-programming-patterns-in-scala-and-clojure) and the [Clojure Design Patterns](http://mishadoff.com/blog/clojure-design-patterns) article give great examples of how first class functions can be used thus further simplifying your code.   

#### Immutability and Object Orientation ####

Having immutability makes reasoning about your code much simpler  - a method (now a function) will always give a certain output given an input.  There are no timing/concurrency issues depending on the state of an object at a particular time and now worries about whether other threads are unknowingly changing your object's state, e.g. compared with using something like ConcurrentHashMap.  If you want immutability in Java, you'll either going to have to pepper the "final" keyword everywhere or use other libraries e.g. Google Guava. 

Clojure uses the embrace and extend strategy by being hosted on the Java platform and allowing access to a multitude of already existing libraries.  To use/reuse a particular library, in most cases it's a case of referencing the jar you need from a maven repository, importing the classes you need into your namespace and just using the java classes via clojure's java interop features.  For clojure equivalents of java libraries, many can be found from [the clojure toolbox](https://www.clojure-toolbox.com/)

#### REPL-Driven Development ####

Clojure's REPL improves the feedback loop for testing your code.  In java, we type our code, compile it, and then run it to test if it works.  With Clojure's REPL we can program without the need for compilation.  We can "evaluate" our functions into the REPL, and re-evaluate them as we need to - a kind of hot code reloading you could do in java using a Java Debugger, but which is a lot more convenient, interactive and faster in clojure.  Any interactive testing we do in the REPl can be copied into a clojure test file in order to build a test suite.  Using an editor with good integration with the REPL (such as Emacs with CIDER), makes it easy to send s-expressions to the REPL for evaluation.  We can use the doc and source functions at the repl to learn more about the clojure functions we wish to use. 

#### Category Theory Not Essential ####

whilst functional programming is almost synonymous with having to learn about monads, monoids and functors, we can do a lot without having to learn about category theory initially.  The let macro is an implicit identity monad, where expressions are evaluated and bound to local "symbols" sequentially, that can then be used in an s-expression within the let form [(More info can be found here)](https://github.com/khinsen/monads-in-clojure/blob/master/PART1.md).  Other useful macros to help in structuring clojure code are the thread-first and the thread-last macros, which allow you to structure your functional calls as pipelines of transformations on data.

#### Functional programming basics ####

with clojure it's still important to learn some basics such as using recursion instead of iteration.  As well recursively calling functions, the loop/recur construct can help to both have an "accumulator" if required, and to do tail recursion, signalling "tail call optimisation" to the JVM[3](Living Clojure).  When working with lists, we should be comfortable with using map and reduce, as well as list comprehensions. 

#### Parentheses Gives Structure####

At first, the amount of brackets may seem overwhelming, but this is where an editor that works well with lisp is needed  (popular ones are Emacs, Vim, LightTable and Intellij with Cursive).  Emacs in particular has features for highlighting balanced parentheses in different colours, and to highlight any unbalanced parentheses.  The parentheses also provide a structure to your program where s-expressions can be manipulated using features such as paredit or smartparens in emacs.

#### Testing your Code ####

Without types in your code, your functions need be tested well, both at the repl, and in your tests.  Use unit tests and integration tests.  Where possible, use generative testing aka property based testing to generate your test cases. 

## References and Useful Links ##

- [Clojure](https://www.clojure.org) - the main clojure website.
- [Living Clojure](http://shop.oreilly.com/product/0636920034292.do) - This is a great book to get up to speed with Clojure.
- [4clojure.com](https://www.4clojure.com) - You're going to have to learn by doing.
- [exercism.io](https://www.exercism.io) - Again, learn by doing.
- [clojure.algo.monads](https://github.com/clojure/algo.monads) - Monads in clojure if you really want to.
- [Clojure Cheatsheet](https://clojure.org/api/cheatsheet) - The "go to" web page when you need to use a clojure function.
- [Effective Programs](https://www.youtube.com/watch?v=2V1FtfBDsLU) - where Rich Hickey claims types are coupling and you're going to need a lot of testing anyway.
- [Testing the Hard Stuff and Staying Sane](https://www.youtube.com/watch?v=zi0rHwfiX1Q) - introduction to the power of property based testing.
