---
layout: post
status: publish
published: true
title: First steps with Haskell
author: Kyle
author_login: 0not
author_email: unclekyky@gmail.com
wordpress_id: 82
wordpress_url: http://0not.net/?p=82
date: '2015-02-25 19:40:48 -0700'
date_gmt: '2015-02-25 19:40:48 -0700'
categories:
- Programming
tags:
- Haskell
- Programming
comments: true
---

The other day I was bored and itching for something to do. I decided that it was about time to learn a new programming language. After awhile, I figured that I should try tackling functional programming again. Back in 2008 I tried to learn <a href="https://www.haskell.org/" target="_blank">Haskell</a>, but at the time I just didn't have it in me. I wasn't sure I wanted to try Haskell again, so I took a look at <a href="http://www.scala-lang.org/" target="_blank">Scala</a>, <a href="http://clojure.org/" target="_blank">Clojure</a>, and <a href="http://en.wikipedia.org/wiki/Scheme_%28programming_language%29" target="_blank">Scheme</a>. Scala and Clojure were both interesting, but I wanted to learn functional programming, so I went with Haskell. Haskell is often touted as a "purely functional programming language," so it seemed perfect.

## What I've Done So Far

I started out with <a href="https://tryhaskell.org/" target="_blank">Try Haskell</a>. It is a nice introduction to some very basic language features, but you're not going to get very far with their REPL. I don't believe there is any state between lines, so you cannot declare functions (and use them later). But that is OK, it's super easy to install the <a href="https://www.haskell.org/platform/" target="_blank">Haskell Platform</a> on your computer.

The main resource I followed for a few days was <a href="http://learnyouahaskell.com/chapters" target="_blank">Learn You a Haskell for Great Good</a>. It's a pretty decent book, but I couldn't help feeling that it wasn't really teaching me the "why" of functional programming, just the "how."

I needed some practice, so with what I had learned so far, I set out to solve some problems on <a href="https://projecteuler.net/archives" target="_blank">Project Euler</a>. For example, here is my solution to Problem 1:
    
```haskell
-- Sum of all natural positive numbers less than 1000 that are 
-- divisible by 3 or 5
-- Ans: 233168
e1 :: Int
e1 = sum [x | x <- [1..999], x `mod` 3 == 0 || x `mod` 5 == 0]
```


That was easy! I defined a function "e1" that returns an Int. Using <a href="https://wiki.haskell.org/List_comprehension" target="_blank">list comprehension</a>, I take a list from 1 to 999 and only return numbers divisible by 3 or 5.

I started reading <a href="http://www.amazon.com/Real-World-Haskell-Bryan-OSullivan/dp/0596514980/ref=sr_1_1?ie=UTF8&qid=1424890727&sr=8-1&keywords=real+world+haskell" target="_blank">Real World Haskell</a> (which is also available through Safari Books Online). I found it to be a much better resource. I already knew quite a bit, so I was able to fly through several chapters. Even so, those chapters did teach me more. The exercises in this book are also excellent.

I've also tried to use a few packages from <a href="https://hackage.haskell.org/packages/" target="_blank">Hackage</a>. I wanted to plot something, so I first tried using <a href="https://hackage.haskell.org/package/gnuplot" target="_blank">gnuplot</a>. I'm a fan of gnuplot, but the Haskell bindings are a bit on the unusable side (for a newbie, at least). I settled on <a href="https://hackage.haskell.org/package/easyplot" target="_blank">EasyPlot</a> (which still uses gnuplot under the hood). I was able to plot the results from my <a href="https://gist.github.com/0not/09dce776d3b4d6158b6d" target="_blank">radioactive decay function</a> in less than two minutes! After spending hours trying to work with the gnuplot packages, I was very impressed!

[![Radioactive decay solutions (Euler's method vs. analytical).](/images/haskell/Screen-Shot-2015-02-25-at-12.42.10-PM-300x216.png)](/images/haskell/Screen-Shot-2015-02-25-at-12.42.10-PM.png)

Some packages on Hackage have absolutely no documentation. I would stay away from them. Some of them have mediocre documentation. Very few have what I would consider acceptable documentation, especially for beginners. The problem is, as far as I can tell, that most Haskell programmers believe the language to be self documenting. I mean, you can always <a href="https://wiki.haskell.org/Determining_the_type_of_an_expression" target="_blank">inspect the type of a function</a>, right? While I admit that is useful to know, it doesn't help a beginner get the grasp of the language. <strong>If anyone who maintains a package on Hackage is reading this, please make sure you have at least one example on how to use your module(s)</strong>.

The most recent resource I found is Stephen Diehl's, <a href="http://www.stephendiehl.com/what/" target="_blank">What I Wish I Knew When Learning Haskell</a>. His section on <a href="http://www.stephendiehl.com/what/#monads" target="_blank">monads</a> helped me to understand them more than anything else.

## What I'll Do Next

Learning Haskell has been extremely rewarding so far. I love the language, I love it's type system, and I'm starting to love the community's abundant package system. I have a few projects in mind to help me continue to learn. I would like to write a ray tracer, since <a href="http://en.wikipedia.org/wiki/Ray_tracing_%28graphics%29" target="_blank">ray tracing</a> is a recursive algorithm. Before I get to that, I will probably make a little REST API for a simple headless CMS I'm planning.

I'm not sure I will ever find a real use for Haskell, but if I do then I'll be ready. Seriously, though, someone give me an excuse to use Haskell.
