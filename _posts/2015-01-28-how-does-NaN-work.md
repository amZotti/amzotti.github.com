---
layout: post
title: "How does NaN work?"
description: "Why not a number actually IS a number!"
category: "javascript"
tags: [javascript]
---
{% include JB/setup %}

<h1>isNaN VS Math.isNaN</h1>
I have been writing underscore.coffee and in doing so I decided to recreate
<code>isNaN</code>.
<pre>
  _.isNaN = (value) ->
Number.isNaN(value)
  </pre>

  <p>There is a method on the <b>global object</b> called <code>isNaN</code>.
There is also a method
  on the <b>Number object</b> called <code>isNaN</code>. Do you know the difference?
The global <code>isNaN</code>
  returns true if passed the value undefined, which is clearly incorrect.
  <code>Number.isNaN</code> returns false for undefined values and returns true
only for NaN values.</p>

<h2>NaN is a Number</h2>
  <p>I originally thought 'not a number' meant a mathematical expression
evaluated to a value that was a type other than <code>Number</code>. I later
realized that 'not a number' really means
  'not a <b>real</b> number'. <code>NaN</code> is actually meant to represent
mathematical expressions which result in
  values that cannot be expressed in the number set JavaScript provides. For
  example, imaginary numbers cannot be represented in JavaScript. If an
  expression is performed that creates an imaginary number then JavaScript
  will raise <code>NaN</code>. Imaginary numbers are numbers though, they are just numbers that cannot be
represented in JavaScript. Therefore, 'not a number' should more accurately be called 'not a real
  number'. JavaScript can only represent real numbers and everything else
is considered <code>NaN</code>. This is why the data type of <code>NaN</code> is
<code>number</code>.</p>

  <pre>
  typeof NaN
  >>>"number"
  </pre>

<p>So there you have it, not a number is a number!</p>

