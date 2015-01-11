---
layout: post
title: "What is JSONP?"
description: "JSONP allows developers to get around the restrictions incurred by
the same-origin policy."
category: "javascript"
tags: [javascript, front end development, coffeescript]
---
{% include JB/setup %}

<h1>JSONP Clarified</h1>
<p>JSONP stands for "JSON with padding". JSONP is a means of passing Javascript
expressions cross-origin. It is an alternative way to fetch data that can
bypass the <a href="http://en.wikipedia.org/wiki/Same-origin_policy">same-origin
policy</a> in a way normal AJAX calls cannot. JSONP allows us quick cross-domain
usage of APIs, but has the disadvantage of being unable to perform error
checking in older browsers. It also disallows us from making POST
request. Only cross domain calls which result with the evaluation of received
data using Javascript in the browser require JSONP. Interfaces which implements
<a href="http://en.wikipedia.org/wiki/Cross-origin_resource_sharing">CORS</a> do not require JSONP. For example, Twitter API and Google Maps API do not require JSONP. Another disadvantage of JSONP is it leaves your application vulnerable to XSS attacks by the foreign origin you are requesting from. If the remote end of the JSONP source isn't trusted, your application is open to an XSS attack.</p>

<h2>How to use JSONP</h2>
<p>I recently had to use an API in order to retrieve weather data. In doing so I
learned all about the restrictions incurred by the same-origin policy and how to
get around it using JSONP. JSONP allows developers to get around the same-origin
policy. JSONP takes advantage of the fact that the <code>&lt;script&gt;</code> tag does not need to abide by the same-origin
policy. We can create a <code>&lt;script&gt;</code> tag and set it's <code>src</code>
attribute to our API endpoint. Additionally, we can even specify options right there in the <code>src</code>
url, such as the return format and the callback to be triggered right there in
the <code>src</code> attribute.</p>

<b>app.coffee</b>
<pre>
script = document.createElement("script")
script.src = "http://api.worldweatheronline.com/free/v1/weather.ashx?q=#{query}&format=json&callback=processWeather&key=j8xvysb7t9jp2dvw7pwcbgs3"
document.body.appendChild(script)
</pre>

<p>Notice the <code>callback=processWeather</code> code in the <code>src</code>
attribute. This callback option makes it so when the data is retrived from the
API then that callback is called with the return data. All we need to do is
declare the callback function in <b>app.coffee</b>.</p>


<b>app.coffee</b>
<pre>
window.processWeather = (weather) ->
  if weather.data.error
    #do stuff
  else
    #do some other stuff
</pre>

<h3>Nuances of Scoping in CoffeeScript</h3>
<p>Notice that I declared processWeather on the <code>window</code> object. I had to do this
because CoffeeScript wraps all code inside an anonymous function when it
compiles into JavaScript. Since the
<code>src</code> attribute that is activating <code>processWeather</code> is calling from outside the
<b>app.coffee</b> scope, <code>processWeather</code> needs to be declared on the
<b>window</b> object so that it is accessible to the callback.</p>

<h3>Using JSONP with AJAX</h3>
<p>One way to perform a JSONP request it by using a
<code>&lt;script&gt;</code> tag with an embedded callback in it and appending it to the DOM.
There exist other ways to perform a JSONP
request. One of those other ways is to use ajax. JSONP can be used in
conjunction with ajax. All you need to
do is create a normal ajax get request and change a few properties of the object
you pass in. On the object you pass into the ajax
method the <code>dataType</code> property should be set to <code>"jsonp"</code> and the <code>jsonpCallback</code>
property should be set to whatever callback you want to use on the response
data.</p>

<h3>Example</h3>
<b>app.coffee</b>
<pre>
request = (requestType) ->
  {
    url: endpointURL requestType
    jsonpCallback: "displayMovies"
    dataType: "jsonp"
  }

$(document).ready ->
  $('#opening').click ->
    $.ajax request "opening"

  $('#now').click ->
    $.ajax request "in_theaters"

  $('#coming').click ->
    $.ajax request "upcoming"
</pre>
<p>And bam! JSONP will work with ajax!</p>
