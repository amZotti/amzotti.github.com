---
layout: post
title: "Javascript Inheritance Patterns: Functional and Psuedo-Classical"
description: "Polymorphism could be defined as an object's ability to manifest in different
forms. The abstract notion of polymorphism manifest as the concrete application
of subclassing. A class works great when you want to create a fleet on similar
objects. Polymorphism allows us to subclass in order to augment different"
category: "javascript"
tags: [javascript]
---
{% include JB/setup %}

<h1>Introduction to Polymorphism</h1>
<p>Polymorphism could be defined as an object's ability to manifest in different
forms. The abstract notion of polymorphism manifest as the concrete application
of subclassing. A class works great when you want to create a fleet on similar
objects. Polymorphism allows us to subclass in order to augment different
behavior onto different objects.</p>

<h3>Functional Inheritance</h3>
  <p>Functional inheritance can be used with functional instantiation (aka: Factory
Pattern) or shared functional instantiation. Functional inheritance is when you
instantiate an object inside a function, and then augment that object with
special properties before returning it.</p>

<pre>
function Shape(width, height) {
  var shape = {};
  shape.width = width;
  shape.height = height;
  return shape;
}

function Square(width, height) {
  var shape = Shape(width, height);
  shape.size = this.width * this.height;
  return shape;
}

square = Square(100, 100);
>>>Object {width: 100, height: 100, size: 10000}
</pre>

<p>We called the <code>Shape</code> factory and received a <code>Shape</code> object in return. We then
augmented it with a <code>size</code> property and returned the augmented
object.</p>

<h3>Pseudo-classical Inheritance</h3>
<p>Pseudo-classical inheritance is used with pseudo-classical instantiation
(aka: Constructor Pattern). There are two different things that need to be
inherited when using the pseudo-classical style. Firstly, you need to inherent
properties from within the constructor. Secondly, you need to inherent
properties from <code>ConstructorName.prototype</code>. Additionally, you also need
to manually set the subclass's <code>constructor</code> property. The subclass
inherents it's prototype from the superclasses prototype, this works fine but it
has the unfortunate side effect of destroying the reference the subclasses
prototype constructor property has to itself. We need to set the subclasses
constructor property manually as a
result.</p>

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
</pre>

<p>Notice when we use pseudo-classical inheritance that the line <code>
Fruit.call(this, sweetness, freshness, organic);</code> is what is doing the
heavy lifting here. All we need to do is call the superclass <code>Fruit</code>
from within subclass <code>Apple</code> for inheritance to occur. The reason we
do not need to set any variables explicitly is because our <code>call</code> to
<code>Fruit</code> is occurring in the context of <code>Apple</code>. Therefore
when <code>this</code> is used in superclass <code>Fruit</code> it is actually
referring to the object that is being instantiated in <code>Apple</code> since
<code>this</code> refers to the object being created when using the Constructor
pattern. </p>

<img src="http://i.stack.imgur.com/ZNn56.png"/>

<p>As stated previously, on top of calling <code>Fruit.call(this, sweetness, freshness,
organic);</code> we also need to set inheritance in their Prototype chains
correctly and set the subclasses constructor property manually on it's
prototype.</p>

<pre>
Fruit.call(this, sweetness, freshness, organic);
Apple.prototype.constructor = Apple
</pre>

<p>If we do not manually set <code>Apple.prototype.constructor = Apple</code>
then the <code>constructor</code> property will be lost due to inheritance
overriding it. We would then get weird behavior
when using functionality like <code>instanceof</code>.</p>
