---
layout: post
title: "Instantiating a SuperClass Constructor from a ChildClass"
description: "Calling the constructor of a given subclasses parent in the
context of the subclass is the same as performing 'super' in Python or Ruby"
category: "javascript"
tags: [javascript]
---
{% include JB/setup %}

<p><a
href="http://amzotti.github.io/javascript/2015/02/09/javascript-inheritance-patterns/">Yesterday
I wrote about how to perform pseudo-classical inheritance</a> and I wanted to
follow up on that post with a few key distinctions. This is the example I gave
of how to perform pseudo-classical inheritance: </p>

<pre>
function Fruit(sweetness, freshness, organic) {
  this.sweetness = sweetness;
  this.freshness = freshness;
  this.organic = organic;
}

function Apple(sweetness, freshness, organic) {
  Fruit.call(this, sweetness, freshness, organic);
  this.color = "red";
  this.name = "apple";
}

Apple.prototype = Object.create(Fruit.prototype);
Apple.prototype.constructor = Apple
</pre>

<p>In this example it appears as though there are two distinct lines of code of
where inheritance is occurring. Lines <code>Fruit.call(this, sweetness, freshness,
organic);</code> and <code>Apple.prototype =
Object.create(Fruit.prototype);</code>. Both of these lines of code are involved
in pseudo-classical inheritance, but do you know what each one does?</p>

<h3>Calling SuperClass Constructor</h3>
<p><code>Fruit.call(this, sweetness, freshness, organic);</code> is actually has
no role in establishing a delegation relationship at all. This line does not
really have anything to do with inheritance per se. What this line really
does is call the the super classes constructor in the context of a child.
Conceptually it does
the same thing that <code>super</code> does in Ruby or Python.</code>

<h3>Establishing the Delegation Relationship</h3>
<p><code>Apple.prototype = Object.create(Fruit.prototype);</code> is the line of
code solely responsible for establishing the prototypal chain. In my previous
article I was more focused on this relationship so I will not write about it
much here. I just wanted to take this time to focus on the distinction between
calling the super class constructor and establishing the delegation
relationship.</p>
