---
layout: post
title: "How HTML Tables Work"
description: "Simple and concise explanation of what all the different HTML tags
related to tables do and tips on how to structure a table correctly."
category: "web development"
tags: [web development, front end development, html]
---
{% include JB/setup %}

<h1>Components of an HTML Table</h1>
<p>While working with <a href="http://backbonejs.org/">Backbone.js</a> I had to use parent and children views to
create various tables. I realized I didn't fully understand how to structure
HTML tables so I decided to take a few minutes to do a deep dive on table
structure. I want to write this posts to really solidify what I learned and
share my knowledge with anyone else who is very curious.</p>

<ul>
  <li>The <code>tr</code> tag is a table row</li>
  <li>The <code>th</code> tag is a table header. This represents the
columns in the table</li>
  <li>The <code>td</code> tag is a unit of table data. <code>td</code> tags are
what make up the actual content of the table</li>
</ul>

<h2>Structuring an HTML Table</h2>
<p>When setting up an HTML table you should declare all the <code>th</code>
cells before listing any <code>td</code> or <code>tr</code> cells.
<code>th</code> cells should be listed completely independently of the other
tags because they represent the number of columns the HTML table will have and
are therefore related to structure and not content.</p>

<h3>Filling in Table Content</h3>
<p>As far as inputting content in the HTML table, you should create a table row
using the <code>tr</code> tag and then fill it with <code>td</code> tags. The <code>td</code>
tags represent the content, so within each <code>td</code> tag you should put
one element of table data.</p>

<p>The td cells should be nested within the tr
cells. This is because a td cell represents an entry, and a tr represents the
beginning of a new row. So the overall structure of a tree should look like
this</p>

<pre>
&lt;table&gt;
  &lt;th&gt;First&lt;/th&gt;
  &lt;th&gt;Last&lt;/th&gt;
  &lt;th&gt;Age&lt;/th&gt;

  &lt;tr&gt;
    &lt;td&gt;Jill&lt;/td&gt;
    &lt;td&gt;Smith&lt;/td&gt;
    &lt;td&gt;50&lt;/td&gt;
  &lt;/tr&gt;
  &lt;tr&gt;
    &lt;td&gt;Eve&lt;/td&gt;
    &lt;td&gt;Jackson&lt;/td&gt;
    &lt;td&gt;94&lt;/td&gt;
  &lt;/tr&gt;
  &lt;tr&gt;
    &lt;td&gt;John&lt;/td&gt;
    &lt;td&gt;Doe&lt;/td&gt;
    &lt;td&gt;80&lt;/td&gt;
  &lt;/tr&gt;
&lt;/table&gt;
</pre>

<p>This table will render as:</p> 
<img src="http://i.imgur.com/XTQvtTz.png"/>

<p>Obviously, this requires some basic styling. Tables need CSS styling or else
the content inside the table will overflow and become disorganized.
We can fix this by adding a nice 1px solid black border around the
<code>table</code>, <code>th</code>,
and <code>td</code> tags.

<pre>
&lt;style&gt;
  td, th, table {
    border: 1px solid black;
  }
&lt;/style&gt;
</pre>

<p>This causes the table to instead render with a simple border which causes the
data to be more organized and readable:</p>
 <img src="http://i.imgur.com/i9UYOza.png"/>
