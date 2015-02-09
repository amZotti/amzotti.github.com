---
layout: post
title: "jQuery Data Structures"
description: "Foundational principles which will allow you to learn faster than
you ever thought possible. Tips to break through sticking points."
category: "jquery"
tags: [javascript]
---
{% include JB/setup %}


<h1>jQuery's Relationship to the Browser</h1>
<p>jQuery is a JavaScript library that provides an easy interface for manipulating
and traversing DOM Nodes. jQuery uses the browser API under the hood to perform
all DOM manipulations. jQuery abstracts all the different browser API's into a
single library.</p>

<p>Using jQuery instead of native DOM API results in less typing, cleaner code,
and easy handling of all
inconsistencies between different browser implementations. Different browsers
implement their API for interacting with the DOM differently, jQuery handles
all these inconsistencies under the hood and makes it so you can use the same
syntax to manipulate DOM Nodes regardless of what kind of browser you are
using. Additionally, jQuery also simplifies many web processes. For example,
AJAX request are part of of jQuery which allow for RESTful request to be
created. Prior to AJAX the primary means of client to server real-time
communication was by using <code>XMLHttpRequest</code>.</p>

<img
src="http://www.codeproject.com/KB/scripting/jqueryLab/anatomy_of_jquery.png"/>


<h2>What is a jQuery-array?</h2>
<p>Both <code>$</code> and <code>jQuery</code> can be used to make jQuery-arrays.
<code>$</code> is nothing but an alias for <code>jQuery</code>, they are both
the same object in memory.</p>

<pre>
jQuery === $
>>>true
</pre>

<p><code>$</code> is a function which returns an empty pseudo-array.</p>
<pre>
$()
>>>[]
</pre>

<p>The pseudo-array which the <code>$</code> function returns is a special type of
pseudo-array which has methods that act specifically on DOM Node objects, we can
refer to this special pseudo-array as a jQuery-array. The jQuery-array data
structure is meant to hold and act on DOM Node objects. jQuery-array's have
special methods that can act specifically on DOM Node objects. </p>

<h2>jQuery Methods are not Recursively Called on Children Nodes</h2>
<p>If a DOM node which is a container for other DOM nodes is inside a jQuerry-array, then calling a method on that container DOM node will not make the method be recursively called on all the DOM Node containers children. 
This is a key distinction to make because it appears as though method calls on a
DOM Node do affect children. For example, if you type
<code>$("body").fadeOut()</code> on a web page then everything on the page will
fadeout. It would appear as if fadeOut were called recursively on every Node
object in the body container. This is not true though, fadeOut is only called on
body. The fact that everything within body is also faded out occurs as a side effect. </p>

<img src="http://james.padolsey.com/stuff/jQueryBookThing/img/layers.png"/>
<p>jQuery-arrays are created by calling the jQuery object and passing in any valid CSS selector as a string.
<pre>
$jQueryArray = $('some-css-selector');
</pre>
The <code>$</code> function also accepts html strings, and HTML5 DOM tree accessors as arguments.</p>

<h3>jQuery Arrays Reimplement Existing Methods</h3>
<p>Some methods that exist in core JavaScript also exist on jQuery-arrays.For example, 
<a href="http://api.jquery.com/jquery.each/">jQuery-arrays have an <code>each</code> function</a>. because the array data structure it provides is not
a real array, therefore it could produce unexpected behavior if used with underscore/or
other libraries with higher order functions like <code>each</code>. Use the
jQuery version of higher order functions because they are specially designed to
work with jQuery-arrays.</p>

<h3>Naming Conventions for jQuery-arrays</h3>
<p>It is also worth emphasizing that DOM Node objects are never converted to jQuery
objects, they are only capable of being held in a jQuery-array. It is a best
practice to prefix variable identifiers which hold a jQuery-array with a
<code>$</code>.</p>
<pre>
var $myBody = $("body");
$myBody.show();
</pre>

<h3>jQuery-array's VS HTMLCollection's</h3>
<p>The DOM is the in-memory representation of the rendered HTML. There is a one to one mapping
between HTML elements and DOM Nodes. The DOM is updated in real time by a 2 way data
binding between itself and the HTML. The DOM has references to all HTML elements
on screen. Just as there exist a jQuery-array container there is also a DOM
array-like container which is called HTMLCollection. The HTMLCollection
pseudo-container has very limited functionality compared to jQuery-arrays.</p>
