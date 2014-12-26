---
layout: post
title: "What is Middleware?"
description: ""
category: "software architecture"
tags: [middleware, software architecture]
---
{% include JB/setup %}

<h1>What is Middleware?</h1>
<p>Middleware is software that operates between the bounds of two interfaces.
It is a layer of abstraction between two other layers. The term
'middleware' is context dependent. It refers to different things depending on
the level of abstraction you are speaking of. For example, in standard MVC we could consider a controller a
peice of middleware because it it a layer of abstraction which lies between the
routes and model.</p>

<h2>Middleware simplified</h2>
<p>The term middlware may sound intiminating when you hear it for the
first time. A lot of terms in programming
sound complex but are actually incredibly simple. <a
href="http://en.wikipedia.org/wiki/Middleware">Wikipedia</a> sums up middleware in a very simple and accurate way by describing it
as "software glue".</p>

<h2>Real world example:</h2>
<p>We want to parse incoming traffic as json before it hits the routes. In
other words, we want to put <b>software</b> in the <b>middle</b> between our client and our
routes.</p>

<p>We can do that by using <a
href="https://github.com/expressjs/body-parser">body-parser</a>
for <a href="https://github.com/expressjs">express.js</a> with the following lines of code:
of code:</p>
<pre>
var express = require('express');
var app = express();
app.use(express.json());
</pre>

<p>And BAM! That's pretty much it.</p>

<p>If this is your first time learning about middleware then I encourage you to go
find ways to use it rather than to read more about it. Reading about something
is great to get an awareness but there needs to be a point where that knowledge
becomes translated into experience.</p>

<p>And of course no blog post would be complete without an explanatory
image:</p>
<p><img src="http://clacklisp.org/tutorial/clack-middleware-2.png"></p>
