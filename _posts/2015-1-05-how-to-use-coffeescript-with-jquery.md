---
layout: post
title: "How to use CoffeeScript with jQuery"
description: "Syntactic differences between CoffeeScript and JavaScript when using jQuery library"
category: "jQuery"
tags: [jQuery, CoffeeScript, web development]
---
{% include JB/setup %}

<h1>How to use CoffeeScript with jQuery</h1>
<p>Despite CoffeeScript's beauty I was discouraged to use it because I thought it wouldn't work well when used in conjunction with other libraries such as jQuery. I was skeptical, but I was wrong. CoffeeScript works great with other libraries, especially jQuery! Here I will provide the basic syntactic shifts needed to write jQuery using CoffeeScript.</p>

<h2>Purpose of Writing CoffeeScript</h2>
<p>Before learning CoffeeScript we need to ask ourselves: What IS the purpose of CoffeeScript? CoffeeScript tutorials invariably state the primary benefit of CoffeeScript is that it requires less typing. While this is certaintly true, I believe there is a more subtle benefit. CoffeeScript allows developers to quickly mentally shift between ideas. This is the result of CoffeeScript's readability. CoffeeScript's readability provides a higher degree of clarity in regards to what is happending in the code than vanilla JavaScript does. CoffeeScripts natural readability makes it so there are no breaks in the stream of thought of the developer. Normally in jQuery there is so much 'noise' that switching between methods takes a second to readjust mentally. CoffeeScript's high levels of readability make this mental shift only take a few milliseconds. It makes it far easier to transistion mentally between tasks. The boost in productivity is not only a boost in terms of time effectiveness from reduced typing, but it is also a qualitative improvement that is the result of deeper focus and thus more attention to details.</p>

<h2>Syntactic Shift: Use Stabby Lambdas (->) Instead of Annonymous Functions</h2>
<p>jQuery syntax for targeting elements is not different. The only major syntactic difference is that annonymous functions are declared using 'stabby lambdas' rather than the 'function (...) {...}' syntax.</p>

<h3>JavaScript</h3>
<pre>
$('.num').click<b>(function() {</b>
  displayValue += $(this).text();
  return setDisplayValue(displayValue);
<b>});</b>
</pre>

<h3>CoffeeScript</h3>
<pre>
$('.num').click<b> -></b>
  displayValue += $(@).text()
  setDisplayValue displayValue
</pre>

<p>CoffeeScript looks a lot cleaner- the code is very easy to mentally grasp quickly and effectively.</p>

<h2>Syntactic Shift: Use @ Instead of this</h2>
<p>Writing jQuery with CoffeeScript is not that much different. It is really just a series of syntactic shifts. One of those shifts is writing <code>@</code> instead of <code>this</code>.

<h3>JavaScript</h3>
<pre>
$('.operation').click(function() {
  num1 = parseInt(displayValue);
  operator = $(<b>this</b>).text();
  displayValue = "";
  return setDisplayValue(displayValue);
});
$('#equals').click(function() {
</pre>

<h3>CoffeeScript</h3>
<pre>
$('.operation').click ->
  num1 = parseInt displayValue
  operator = $(<b>@</b>).text()
  displayValue = ""
  setDisplayValue displayValue
</pre>

<h2>How do I use CoffeeScript with jQuery?</h2>
<p>Okay, so you are convinced CoffeeScript is awesome! But how do you start using it? There are really two ways to incorporate CoffeeScript with jQuery. The first way is to include CoffeeScript as a client side library and have it render CoffeeScript into JavaScript in the browser during runtime. This way is not recommended. The second way is to write CoffeeScript and then compile it into JavaScript, then use that JavaScript as you normally would. This is the recommended way. There are many CoffeeScript compilers out there. Choose one.</p>

<h4>Resources</h4>
<p>Want to learn more? I recommend <a href="http://autotelicum.github.io/Smooth-CoffeeScript/Smooth%20CoffeeScript%20Web%20Optimized.pdf">Smooth CoffeeScript</a> and <a href="coffeescript.codeschool.com">CodeSchool's CoffeeScript course</a>.

