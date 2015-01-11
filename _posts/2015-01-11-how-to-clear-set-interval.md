---
layout: post
title: "How to clear set interval"
description: "setInterval can be cleared by using the clearInterval method and
passing in the interval ID"
category: "MicroPost"
tags: [javascript, web development]
---
{% include JB/setup %}


<h1>Clearing setInterval()</h1>
<p>When you initiate the <a
href="https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers.setInterval">setInterval
method</a>, an interval ID is returned. If you retain
that interval ID in a variable, you can later pass it into the <a
href="https://developer.mozilla.org/en-US/docs/Web/API/WindowTimers.clearInterval">clearInterval
method</a> to stop the interval:</p>

<h3>Example:</h3>
<pre>
  var intervalID = setInterval(startClock, 1000);
  resetTimer()

  $("#stop").click(function() {
    clearInterval(intervalID);
  });
</pre>

