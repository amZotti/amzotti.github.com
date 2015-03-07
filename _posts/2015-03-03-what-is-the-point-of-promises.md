---
layout: post
title: "What is the point of JavaScript Promises?"
description: "Promises provide us a way to mimic the predictable control flow
of classical synchronous programming, while getting the benefits of actually
performing asynchronous operations under the hood. At it's core a promise is 
ssentially an object which represents a value that is not known yet."
category: "javascript"
tags: [javscript, computer science, programming paradigms, design patterns,
web development, software architecture]
---
{% include JB/setup %}

<h1>The Reason for Promises</h1>

<p>General purpose programming follows a predictable control flow. When
	asynchronous code is introduced into our code base, the predictable nature
	of our code bases control flow is interrupted. This interruption
	makes our codebase more difficult to read and thus more difficult to
	maintain. If the project requires us to nest asynchrnous operations then
	it is easy to fall into the depths of <a href="http://callbackhell
	com/">callback hell</a>, at which point the potential for both syntactic
	and semantic programming errors increases dramatically. </p>

<img src="http://i.imgur.com/gn3N5gB.png"/>

<p><i>At last, there is hope:</i> Promises provide us a way to mimic the predictable control flow of classical synchronous programming, while getting
the benefits of actually performing asynchronous operations under the hood.
At it's core a promise is essentially an object which represents a value that is not known yet.</p>

<p><a href="http://www.javacodegeeks.com/2013/12/node-js-non-blocking-io-model.html">All i/o in Javascript is asynchronous by default</a>.
Promises are a means of handling asynchronous i/o in a pseudo-synchronous 
format. Using promises gives the illusion of seamless and smooth control 
flow while getting the benefits of having non-blocking i/o. </p>

<h2>Benefits and Mechanics of Promises</h2>

<p>Promises are chainable which results in a predictable control flow. 
	Promises are chainable because under the hood every method on the Promise 
	prototype returns a promise object. The ability of promises to chain
	significantly increases code readability and therefore also significantly increases code maintainability. This translates to less time debugging and higher efficiency.</p>

<p>The promise accomplishes asynchronicity by maintaining an internal state 
	which represents whether the promise has been fulfilled or not. The 
	creation of a promise represents the initiation of an asynchronous i/o 
	operation. During the initial stage of creating a promise prior to 
	completing the i/o operation, the promises internal state is set to 
	'pending'. The internal state of the promise will be 'pending' until the 
	i/o operation completes and it receives the value from the completion of 
	the i/o operation.</p>

<img src="https://lh5.googleusercontent.com/-OMVIop6FKM0/Ul3gNkeJjKI/AAAAAAAAEyg/_4oPYkqVs4Q/w485-h314/promises.png"/>

<p> When the io operation is complete, the promises internal state can change 
	to either being 'fulfilled' or 'rejected'- depending on the results that 
	the io operation returned. Once the promises internal state is no longer 
	pending, any handlers will be activated that were passed to the promise 
	object will be activated. </p>



<p>If the promises state switched from pending to fulfilled, then a success 
	handler will be activated. If the promises state switched from pending to 
	rejected, then the promises failure handler will be activated. The most 
	simple and commonly used mechanism for setting success and failure handles 
	is the <code>then</code> method. </p>

<img src="http://www.b2bweb.fr/wp-content/uploads/687474703a2f2f7279616e73756b616c652e636f6d2f76697a2f50726f6d6973652e706e67-600x260.png"/>


<h3>Conclusion</h3>

<p>There are a lot of articles on the internet about how the internals of
promises work. But most use cases of promises do not require you to understand
their internals.This guide was meant to be a primer for most common uses cases
of promises as seen in popular libraries and APIs. I wanted to cover just the
very 
	basics in terms of methods because I feel like most articles on promises 
	are more about architecture rather than purpose. For more detailed 
	information as to how Promises are archetectured checkout <a href="
	http://dailyjs.com/2014/02/20/promises-in-detail/">Promises In Detail</a>.
</p>
