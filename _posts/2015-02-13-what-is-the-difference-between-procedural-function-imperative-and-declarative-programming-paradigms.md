---
layout: post
title: "The Differences Between Procedural, Functional, Imperative, and
Declarative Programming Paradigms"
description: "There are tons of resources on the internet about imperative and declarative
programming paradigms. I am writing this article because I think there are two
key points that every article I have read so far misses..."
category: "Programming Paradigms"
tags: [programming paradigms, design patterns, computer science]
---
{% include JB/setup %}

<h1>Declarative vs Imperative</h1>
<p>There are tons of resources on the internet about imperative and declarative
programming paradigms. I am writing this article because I think there are a few
key points that are commonly missed that I want to cover.</p>

<p>Declarative and Imperative programming paradigms are nothing but buzzwords
for describing coding on different levels of abstraction. The concept is much
simpler than people make it out to be.
The common description of declarative programming that echoes throughout the internet is
that declarative programming is concerned with <blockquote>"what to do, not how to do
it."</blockquote> And likewise imperative programming is generally described as 
being concerned with <blockquote>"How to do it,
not what to do</blockquote>Declarative programming is to program on a higher
level of abstraction than imperative programming. Neither is better or worse, but both have
their places. An example of where declarative programming is necessary would be
in <a
href="http://www.smashingmagazine.com/2014/07/30/declarative-programming/">web
development when you are working with frameworks</a>. An where of where
Imperative programming is necessary would be in the engineering of
algorithms and other low level necessities.</p>

<p> The definitions for declarative and imperative are pretty clear cut and
ubiquitous throughout the internet. Where things often get muddled is when you
start throwing in the notions of functional and procedural programming.
The concept of functional and procedural programming paradigms are really just
extensions of the concept of declarative and imperative programming paradigms.
In fact, functional programming is a subset of declarative programming, and
procedural programming is a subset of imperative programming. This makes more
sense when you really consider what the <a
href="http://stackoverflow.com/questions/721090/what-is-the-difference-between-a-function-and-a-procedure">difference between a function and a
procedure is.</a></p>

<h2>The Difference Between a Function and a Procedure</h2>
<p>Both functions and procedures are <a
href="http://en.wikipedia.org/wiki/Subroutine">subroutines</a> that are used for re-executing a
predefined block of code. The difference between them is that functions return a value, and
procedures do not. More specifically, functions are designed to have minimal
side effects, and always produce the same output when given the same input.
Furthermore, functions are usually concerned with higher level ideas and
concepts. <a href="http://underscorejs.org/">A great example of this would be
the underscore library</a>. Procedures on the other hand do not have any return
value, their primary purpose is to accomplish a given task and cause a desired
side effect. A great example of procedures would be the well known for loop:
<code>for (var i = 0;i < arr.length;i++) {...}</code>. The for loop is a
subroutine that's main purpose is to cause side effects, and it
does not return a value in of itself.</p>


<h3>How to Remember the Difference Between Imperative and Declarative</h3>
<p>
I remember the difference between the two through the use of an
analogy. To be declarative is to declare something, and usually when I imagine
someone declaring
something I picture them as being in a position of power. Imagine the president during the state
of the union <b>declaring</b> his intentions for <b>what he wants have to
happen</b>. On the
other hand, a good analogy for imperative would be akin to that of a manager of
a McDonald's franchise. He is very imperative and as a result makes everything
really important. He therefore tells everyone <b>how to do everything</b> down to the most simplist of actions. </p>

<img src="http://i.imgur.com/iEc4ry9.gif" title="source: imgur.com" />

<h2>Wrap up (tldr)</h2>
<ul>
<b>
<li>Declarative programming refers to code that is concerned with higher levels of
abstraction.</li>

<li>Imperative programming refers to code that is concerned with lower levels of
abstraction.</li>

<li>Procedural programming is a subset of imperative programming which utilizes subroutines.</li>

<li>Functional programming is a subset of declarative programming which utilizes subroutines.</li>
</b>
</ul>


