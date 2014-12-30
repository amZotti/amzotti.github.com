---
layout: post
title: "How to map event listeners to dynamically generated content"
description: "Adding new elements to the DOM may not always have the expected
funtionality. Learn how to use the DOMNodeInserted event listener to map events
to dynamically generated elements."
category: "jQuery"
tags: [jQuery, front end development, design]
---
{% include JB/setup %}

<h1>Detecting Dynamically Added Elements With jQuery</h1>
<p>The other day I was creating a task manager UI for my <a
href="https://github.com/amZotti/oneWebsiteADay">30 websites 30 days
challenge</a>. The website allows a user to create and delete tasks. This requires a create
and delete button. There are two <code>click</code> listeners: one for creating a new task,
another one for completing a task. </p>

<pre>
var createElement = function() {
  var text = $(&#x22;#todo-create-input&#x22;).val();
  var newElement = &#x22;&#x3C;form class=&#x27;todo-item&#x27;&#x3E;&#x3C;p class=&#x27;todo-text&#x27;&#x3E;&#x22; + text +
    &#x22;&#x3C;/p&#x3E;&#x3C;button type=&#x27;submit&#x27; class=&#x27;delete-button&#x27;&#x3E;Completed&#x3C;/button&#x3E;&#x3C;/form&#x3E;&#x22;
    $(&#x22;main&#x22;).append(newElement);
};

var displayCongratulations = function(e) {
  e.preventDefault();
  $(&#x27;img&#x27;).fadeTo( &#x27;slow&#x27;, &#x27;1&#x27;);
  $(&#x27;header&#x27;).children().remove();
  $(&#x27;header&#x27;).append(&#x22;&#x3C;h1&#x3E;Good job! You did something!&#x3C;/h1&#x3E;&#x22;);
  this.remove();
};

$(document).ready(function(){
  $(&#x22;#todo-create-button&#x22;).on(&#x22;click&#x22;, createElement);
  $(&#x22;.delete-button&#x22;).on(&#x22;click&#x22;, displayCongratulations);
});
</pre>

<h2>The limitation of $(document).ready()</h2>
<p>The above code does not work because we are attempting to bind an event listener
to <code>.delete-button</code> before it has been created. The element which is being created is the same element we are trying to
bind our <code>click</code> listener to in our <code>ready()</code> method. When developing dynamic web
applications it is common that to add new elements to the DOM that need to be
mapped to events. How do we reconcile creating new elements which will require
event listeners, with the notion that all elements are binded to event only when
the DOM loads? Usually our content is binded to an event listener right after the
DOM loads, but if we are adding new elements after the binding method has run, then our new elements will
not map to events correctly.</p>

<h2>The solution: DOMNodeInserted event</h2>

  <p>We can bind an event to the <code>body</code> element of our HTML with the
<code>DOMNodeInserted</code> event. With <code>DOMNodeInserted</code>, when a new
element is inserted onto <code>html</code> element during
runtime the provided callback is executed. That callback can be used for binding <code>click</code>
listeners to events. The syntax for doing that would be as follows:
<code>$('body').on('DOMNodeInserted', callback)</code>.</p>

<p>The above code can be refactored to include <code>DOMNodeInserted</code> event:</p>
<pre><code>
var createElement = function() {
  var text = $(&#x22;#todo-create-input&#x22;).val();
  var newElement = &#x22;&#x3C;form class=&#x27;todo-item&#x27;&#x3E;&#x3C;p class=&#x27;todo-text&#x27;&#x3E;&#x22; + text +
    &#x22;&#x3C;/p&#x3E;&#x3C;button type=&#x27;submit&#x27; class=&#x27;delete-button&#x27;&#x3E;Completed&#x3C;/button&#x3E;&#x3C;/form&#x3E;&#x22;
    $(&#x22;main&#x22;).append(newElement);
};

var displayCongratulations = function(e) {
  e.preventDefault();
  $(&#x27;img&#x27;).fadeTo( &#x27;slow&#x27;, &#x27;1&#x27;);
  $(&#x27;header&#x27;).children().remove();
  $(&#x27;header&#x27;).append(&#x22;&#x3C;h1&#x3E;Good job! You did something!&#x3C;/h1&#x3E;&#x22;);
  this.remove();
};

var bindEventToNewElement = function(e) {
  var target = $(e.target).find(&#x27;button&#x27;);
  $(target).on(&#x22;click&#x22;, displayCongratulations);
}

$(document).ready(function(){
  $(&#x22;#todo-create-button&#x22;).on(&#x22;click&#x22;, createElement);
  $(&#x22;body&#x22;).on(&#x27;DOMNodeInserted&#x27;, bindEventToNewElement);
});
</code></pre>

<p>The newly created elements map to the correct events and
everything will work. Merry Christmas!</p>

<h3>Limitations of DOMNodeInserted event</h3>
<p>New solutions generally create new problems. Problems are never really
solved, because every different solution requires a different implementation,
which leads to different limitations. We will always have problems. We can't
solve problems permanantly, but we can have solutions which lead to higher
quality problems.</p>

<p><b>Consider this:</b> Right now only one kind of element is being added to the DOM:
the delete button. What if we want to add multiple elements to the DOM, each
with its own unique event listener? The above solution would not work because
the same callback is being executed regardless of what we add to the DOM, or
where on the DOM we add it. </p>

<p>In the above example, what if we attatched something new to the DOM which had nothing to do
with our delete functionality? It would attempt to rebind all delete buttons to
their associated events.</p>

<p>One solution would be to <b>bind DOMNodeInserted to the container of wherever we
are appending our dynamically generated content. Instead of listening on
our <code>body</code> tag we could listen only on the container of wherever we
are adding our new content.</b> For example, with
<code>$("body").on('DOMNodeInserted', bindEventToNewElement);</code> we are
initiating <code>bindEventToNewElement</code> callback whenever something is added to the
<code>body</code> element. We could make this more precise by instead binding
the <code>DOMNodeInserted</code>
event to the container that we are attatching the new element to. 
Doing so would look like:

<pre><code>
var createElement = function() {
  var text = $(&#x22;#todo-create-input&#x22;).val();
  var newElement = &#x22;&#x3C;form class=&#x27;todo-item&#x27;&#x3E;&#x3C;p class=&#x27;todo-text&#x27;&#x3E;&#x22; + text +
    &#x22;&#x3C;/p&#x3E;&#x3C;button type=&#x27;submit&#x27; class=&#x27;delete-button&#x27;&#x3E;Completed&#x3C;/button&#x3E;&#x3C;/form&#x3E;&#x22;
    $(&#x22;main&#x22;).append(newElement);
};

var displayCongratulations = function(e) {
  e.preventDefault();
  $(&#x27;img&#x27;).fadeTo( &#x27;slow&#x27;, &#x27;1&#x27;);
  $(&#x27;header&#x27;).children().remove();
  $(&#x27;header&#x27;).append(&#x22;&#x3C;h1&#x3E;Good job! You did something!&#x3C;/h1&#x3E;&#x22;);
  this.remove();
};

var bindEventToNewElement = function(e) {
  var target = $(e.target).find(&#x27;button&#x27;);
  $(target).on(&#x22;click&#x22;, displayCongratulations);
}

$(document).ready(function(){
  $(&#x22;#todo-create-button&#x22;).on(&#x22;click&#x22;, createElement);
  $(&#x22;.list-of-ToDos&#x22;).on(&#x27;DOMNodeInserted&#x27;, bindEventToNewElement);
});
</code></pre>

<p><b>Now the delete buttons will only map to events when an element is added to
<code>.list-of-toDos</code></b>, rather than mapping when any element is added to the
body.</p>

