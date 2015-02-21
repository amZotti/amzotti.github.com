---
layout: post
title: "How do Event Systems Work?"
description: "Event systems enables us to create dynamic code while minimizing decoupling
between entities. When I use the word event systems I am referring to any
network of publishers and subscribers. The most ubiquitous example of this would be a simple onclick listener as seen
in jQuery"
category: "design patterns"
tags: [design patterns, web development, software architecture]
---
{% include JB/setup %}


<h1>What are Event Systems?</h1>
<p>Event systems enables us to create dynamic code while minimizing decoupling
between entities. When I use the word <i>event systems</i> I am referring to any
network of publishers and subscribers.
The most ubiquitous example of this would be a simple onclick listener as seen
in jQuery:</p>

<pre>$('#el').on('click', callback);</pre>

<p>How would you implement the above functionality? How can we 'listen' to an
object? How can we activate <code>callback</code> only once that object is clicked? The
naive approach would be to simply create a
<code>setInterval</code> to continuously check the state of the object and compare it
to it's previous state. The most obvious problem with this way of implementing
an event listener
is that this process would be very expensive computationally. Modern event
systems provide us with a much more effecient way.</p>

<h2>Modern Event Systems Overview</h2>
<p>Instead of having another object continuously check for a state change on a
target object and then executing some behavior when a state change has occured, we can
maintain a datastore of behaviors on the target object itself and have those
behaviors execute when specific events are triggered on it. In other words, We
can associate a datastore of functions on a target object to a specific event. When the event is triggered on
that target object, then the target object itself invokes all the functions in its
datastore. In this way, putting a click listener on a target object, really just adds
a new behavior to the objects datastore.</p>

<h2>Registering an interesting</h2>
<p>The process of sending a callback to a target object to be executed when a certain
state changes are triggered on that target object is called <b>registering an
interest</b>. In our
previous example:</p> 

<pre>$('#el').on('click', callback);</pre>

<p>It could be said that jQuery is registering an interest on the <code>#el</code>
element. On the surface it appears the <code>on</code> listener is
actively listening to the <code>#el</code> element. However, the <code>on</code> listener is not really
<i>listening</i> to the <code>#el</code> element per se. In reality jQuery
is really just sending the provided callback to <code>#el</code> when the
<code>on</code> method is
executed during runtime. When the click state is finally triggered on
<code>#el</code>, it fires all the functions in its datastore. This gives the
illusion that the <code>on</code> method is actively 'listening' to
<code>#el</code> but in reality all<code>on</code> does is register an
interest with <code>#el</code> and as a result <code>#el</code> is <a
href="http://addyosmani.com/resources/essentialjsdesignpatterns/book/#decoratorpatternjavascript">decorated</a>
with new behavior which will be executed only when certain conditions are met in
terms of its state.</p>

<h2>3 Key Attributes of Event Systems</h2>
<ul>
  <li>Event listeners</li>
  <li>Data stores</li>
  <li>Triggers</li>
</ul>

<h4>Additional Resources</h4>
<p>If you want to go deeper on concepts relating to design patterns then I
highly recommend the <a
href="http://addyosmani.com/resources/essentialjsdesignpatterns/book/">JavaScript
Design Patterns book</a>.
