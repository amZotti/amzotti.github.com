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
challenge</a>. The app allows a user to create and delete tasks. This requires a create
and delete button. There are two on click listeners: one for creating a new task,
another one for completing a task. </p>

<pre>
var createElement = function() {
  var text = $("#todo-create-input").val();
  var newElement = "<form class='todo-item'><p class='todo-text'>" + text +
    "</p><button type='submit' class='delete-button'>Completed</button></form>"
    $("main").append(newElement);
};

var displayCongratulations = function(e) {
  e.preventDefault();
  $('img').fadeTo( 'slow', '1');
  $('header').children().remove();
  $('header').append("<h1>Good job! You did something!</h1>");
  this.remove();
};

$(document).ready(function(){
  $("#todo-create-button").on("click", createElement);
  $(".delete-button").on("click", displayCongratulations);
});
</pre>

<h2>The limitation of $(document).ready()</h2>
<p>The above code does not work because we are attempting to bind an event listener
to ".delete-button" before it is created. The element which is being created is the same element we are trying to
bind our <code>click</code> listener to in our <code>ready()</code> method. When developing dynamic web
applications it is common that to add new elements to the DOM that need to be
mapped to events. How do we reconcile creating new elements which will require
event listeners, with the notion that all elements are binded to event only when
the DOM loads? Usually our content is binded to a event listener right after the
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
<pre>
var createElement = function() {
  var text = $("#todo-create-input").val();
  var newElement = "<form class='todo-item'><p class='todo-text'>" + text +
    "</p><button type='submit' class='delete-button'>Completed</button></form>"
    $("main").append(newElement);
};

var displayCongratulations = function(e) {
  e.preventDefault();
  $('img').fadeTo( 'slow', '1');
  $('header').children().remove();
  $('header').append("<h1>Good job! You did something!</h1>");
  this.remove();
};

var bindEventToNewElement = function(e) {
  var target = $(e.target).find('button');
  $(target).on("click", displayCongratulations);
}

$(document).ready(function(){
  $("#todo-create-button").on("click", createElement);
  $("body").on('DOMNodeInserted', bindEventToNewElement);
});
</pre>

<p>The newly created elements map to the correct events and
everything will work. Merry Christmas!</p>

<h3>Limitations of DOMNodeInserted event</h3>
<p>New solutions generally create new problems. Problems are never really
solved, because every different solution requires a different implementation,
which leads to different limitations. We will always have problems. We can't
solve problems permanantly, but we can have solutions which lead to higher
quality problems.</p>

<p>Consider this: The app is expanded to have multiple kinds elements which are added
instead of just a single kind. The above solution would not work because we are executing the callback
to listen to bind only a single kind of element whenever anything is added to the body. In the above
example, what if we attatched something new to the DOM which had nothing to do
with our delete functionality? It would attempt to rebind all events! If we had
different kinds of elements we were dynamically generating then we would need to
listen to where we are adding the element to. For example, with
<code>$("body").on('DOMNodeInserted', bindEventToNewElement);</code> we are
initiating bindEventToNewElement callback whenever something is added to the
body element. We could make this more precise by instead bind DOMNodeInserted
event to the container that we are attatching the new element to, this way the
callback is not activated at the wrong times. Doing so would look like:

<pre>
var createElement = function() {
  var text = $("#todo-create-input").val();
  var newElement = "<form class='todo-item'><p class='todo-text'>" + text +
    "</p><button type='submit' class='delete-button'>Completed</button></form>"
    $("main").append(newElement);
};

var displayCongratulations = function(e) {
  e.preventDefault();
  $('img').fadeTo( 'slow', '1');
  $('header').children().remove();
  $('header').append("<h1>Good job! You did something!</h1>");
  this.remove();
};

var bindEventToNewElement = function(e) {
  var target = $(e.target).find('button');
  $(target).on("click", displayCongratulations);
}

$(document).ready(function(){
  $("#todo-create-button").on("click", createElement);
  $(".list-of-ToDos").on('DOMNodeInserted', bindEventToNewElement);
});
</pre>

<p><b>Now the delete buttons will only map to events when an element is added to
.list-of-toDos</b>, rather than mapping when any element is added to the
body.</p>

