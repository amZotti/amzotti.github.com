---
layout: post
title: "All Primitive Values are (Not) Singletons"
description: "All variables in JavaScript hold references to values in memory. In lower level languages primitive
values like numbers and booleans are stored in variables directly. In JavaScript primitives like numbers and booleans 
  are not values held in variables themselves."
category: "javascript"
tags: [javascript]
---
{% include JB/setup %}

<h1>All Variabes Hold References</h1>
<p>All variables in JavaScript hold references to values in memory. In lower level languages primitive
values like numbers and booleans are stored in variables directly. In JavaScript primitives like numbers and booleans 
  are not values held in variables themselves. Numbers
and booleans are stored
strictly in the heap and the variables which represent those primitive data
types have references to those variables in memory. This is why strings can be
considered primitive types in JavaScript even though they are <a
href="http://www-ee.eng.hawaii.edu/~tep/EE160/Book/chap7/subsection2.1.1.2.html">really arrays under the
hood</a>.</p>

<h2>The Map is not the Territory</h2>
<p>Sometimes the most accurate perception of something is not the most effective
perception of something. Human's have developed heuristics to allow for quick
decision making. If we did not use heuristics then we would have to go through a
lengthy decision making process for simple tasks like opening a door. In
programming human's also use heuristics. For example, programmers believe that primitive values are singletons. Although
this is not really true it is a useful way to think of it in the context of
programming.</p>

<h2>The Map: Only a Single 9 Exist</h2>
<p>All instances of primitive values in
JavaScript are singletons. Only a single instance of a given primitive value
exist in memory at any given time. It appears as though that if you were to instantiate a number,
then that number is created in memory. Any other variables that reinstantiate
that number, will actually be referencing the same number in memory that was
already created.</p>

<pre>
var a = 9;
var b = 9;
a === b
>>>true
</pre>

<p>On the surface, There can only be single number <code>9</code>
in JavaScript; although this is not true in actuality it is a good way to think
about it.</p>

<h2>The Territory: There are Multiple 9's</h2>
<p>The truth is that although the notion that only a single <code>9</code> can exist
in memory at a time it is a good mental model for programming, it is not
technically accurate. JavaScript is
optimized in such a way as such multiple <code>9</code> values can exist in
memory. JavaScript does black magic under the hood to give the illusion there
is only one <code>9</code> value in memory.</p>

