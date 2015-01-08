---
layout: post
title: "Primer to Backbone.js"
description: "What is Backbone.js and what is its purpose?"
category: "Javascript"
tags: [Javascript, web development, front end development]
---
{% include JB/setup %}


<h1>Primer to Backbone.js</h1>
<p>Backbone is a front end MVC framework that provides the ability to
structure data. When I first heard of Backbone being a client side MVC framework I thought,
<blockquote>"I know how MVC works on the server side, but what does MVC mean in
the context of the client?"</blockquote>MVC is a design pattern; MVC applied
to a back-end server is only one implementation of that design pattern. MVC
on the client side is a different implementation of the same pattern. The model interacts with the
server, performs data manipulation, and communicates with our view. The view
renders our model data, listens for events, and makes
changes to the DOM. The view ensures that model data is being represented
accurately in the DOM.</p> 

<p>The notion of controller has different meanings in different front end frameworks. The
model and view are both straight forward and consistent among all frontend MVC
frameworks, but the controllers role differs between frameworks. In the context
of Backbone, the controller could be likened to our routes and navigation. The users ability to navigate around the page and how that navigation effects our data.</p>

<h2>What is the purpose of Backbone.js?</h2>
<p>Anyone who has ever made a non-trivial web application knows how inefficient
it can be to try to manage data through nothing but DOM interactions. Using
vanilla Javascript and jQuery can make it difficult to manage large amounts of
data. Backbone solves this problem by providing models, which provides a place to store information, and views, which allow us to easily make changes to the DOM that correspond to any changes in our models. Backbone provides client-side app structure by giving us models to represent data and view to hook up models to the DOM. </p>

<h3>Backbone.js Models: Managing Data</h3>
<i>Create a model class</i>
<pre>var TodoItem = Backbone.Model.extend({});</pre>

<i>Create a model instance</i>
<pre>var todoItem = new TodoItem({body: "Pick up dry cleaning stuff", id: 1});</pre>

<i>Get an attribute</i>
<pre>todoItem.get('body');</pre>

<i>Set an attribute</i>
<pre>todoItem.set({body: "Do NOT pickup dry cleaning"});</pre>

<i>Sync to server</i>
<pre>todoItem.save();</pre>

<h3>Backbone Views: Displaying Data</h3>
<i>Create a view class</i>
<pre>var TodoView = Backbone.View.extend({});</pre>

<i>Create a view instance</i>
<pre>var todoView = new TodoView({ model: todoItem });</pre>

<p>Notice we are passing in the model object we declared previously. Model
objects and view objects have a one to one relationship. That is, every model
object has a single view object which handles the rendering of it. Additionally
every view object has a top level element that is by default a
<code>&lt;div&gt;</code>. Every view
represents an html element. We can create a render method to display the html
representation of our data:</p>

<pre>
var TodoView = Backbone.View.extend({
  render: function() {
    var html = '&lt;h3&gt;' + this.model.get('description') + '&lt;/h3&gt;';
    $(this.el).html(html);
  }
});
</pre>

<p>This declares the render method on our class declaration of ToDoView.
<code>this.el</code> refers to the top level <b>el</b>ement of the view object,
which will be a <code>&lt;div&gt;</code> since we did not set it manually. The render method is creating the following HTML structure: </p>
<pre>
&lt;div&gt;
  &lt;h3&gt;descriptive text here&lt;/h3&gt;
&lt;/div&gt;
</pre>



