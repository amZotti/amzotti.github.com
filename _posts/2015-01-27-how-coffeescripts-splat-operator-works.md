---
layout: post
title: "Purpose for CoffeeScript's Splat Operator"
description: "CoffeeScript's splat operator solves the problem of arguments
shadowing and limited array method access."
category: "coffeescript"
tags: [coffeescript, javascript]
---
{% include JB/setup %}


<h1> Splat operator VS arguments psuedo-array </h1>

<p>Imagine this: You have a nested function and you want to access the arguments
from an outter function from inside an inner function. The only way to achieve
this using JavaScript's <code>arguments</code> psuedo-array would be to store
the contents of <code>arguments</code> in a variable. Otherwise it would be
inaccessible from an inner function, since when functions are nested, 
<code>arguments</code> refers to the formal parameters of the current function.</p>

<p>CoffeeScript's splat operator (<code>...</code>) allows custom naming of the variable we want
to hold arguments. This means no more shadowing when using
<code>arguments</code> psuedo-array with nested functions.
Check out the splat operator in action: </p>


<b>Example:</b>
<pre>
_.compose = (functions...) ->
  (args...) ->
    _.each functions, (fn) ->
      args = [fn.apply(fn, args)]
    args[0]
</pre>


<p>Using splat operator's makes it easy to access arguments from 
different functions while maintaining readability.</p>

<h2>Splat operator provides access to all array methods</h2>

<p>Using the splat operator transforms the <code>arguments</code>
psuedo-array into a real array. This is what the splat operator is
doing under the hood in our above example:</p>

<pre>functions = 1 <= arguments.length ? __slice.call(arguments, 0) : [];</pre>

<p>The arguments pseudo-array has slice applied to it which copies over the format
parameters into a real array. Using a real array instead of a pseudo-array
provides the ability to use methods which would be inaccessible other.</p>
