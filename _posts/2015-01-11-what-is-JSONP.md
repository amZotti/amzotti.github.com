---
layout: post
title: "What is JSONP?"
description: "JSONP allows developers to get around the restrictions incurred by
the same-origin policy."
category: "javascript"
tags: [javascript, front end development, coffeescript]
---
{% include JB/setup %}

<h3>What is JSONP?</h3>
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
