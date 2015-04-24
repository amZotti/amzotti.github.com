---
layout: post
title: "Exposing the Relationships Between Array Matrices and the Cartesian
Coordinate System"
description: "An array matrix could be seen as a modeling of the Cartesian coordinate system whereby only positive coordinates exist and an extra dimension is included for the value at each point.  In the Cartesian
coordinate system x represents a vertical line which encompasses all y values within a particular range. "
category: "computer science"
tags: [computer science]
---
{% include JB/setup %}


<h1>New Questions Create New Answers</h1>
<p>Today I was solving a complex problem that involved an array matrix. For this
particular problem it seemed useful to think of the matrix in the context of the
Cartesian Coordinate System. I noticed a few distinct differences between the
two systems. The most obvious difference
was that array matrices can only have coordinates that are positive integers as
where the Cartesian Coordinate System spans in every direction. I realized that this
has the potential to create problems representing indices in terms of <code>x</code> and <code>y</code>
instead <code>rows</code> and <code>columns</code>.</p>

<p>
Normally I think of matrices as having a <code>row</code> index and a
<code>column</code> index.

<pre>matrix[row][column]</pre>

The differences in structure between the two visual representations of data
could make it difficult to map <code>x</code> and <code>y</code> to
<code>rows</code> and <code>columns</code>.
I was fascinated as to how the <code>x</code> and <code>y</code> coordinates would
map to the <code>rows</code> and <code>columns</code> indices.
Furthermore, I wanted to know <i>What is the relationship between a 2d Cartesian
coordinate grid and a matrix of arrays?</i></p>

<i>Note: In this article I am referring to a matrix specifically in the
<a href="http://en.wikipedia.org/wiki/Matrix_representation">context of computer science</a>,
as <a href="http://en.wikipedia.org/wiki/Matrix_%28mathematics%29">opposed to a
mathematical matrix</a>.</i>

<h2>Modeling Array Matrices and the Cartesian Coordinate System</h2>

<p>An array matrix could be seen as a modeling of the Cartesian Coordinate System where only positive coordinates exist and
an extra dimension is included to represent the value at each point.  In the Cartesian
Coordinate System, <code>x</code> represents a vertical range which encompasses
all <code>y</code> values
within that given range. Visually, this is represented as follow:</p>

  <img src="http://i.stack.imgur.com/SeThx.png"/>

<p>Values exist at every point on the map where <code>x</code> intersects with <code>y</code>.
A single <code>x</code> coordinate could therefore be seen as a slice of all y
values which fall within that range.  In the context of an array matrix,
the first index represents an <code>x</code> value. For example, `x = 5` is the mathematical representation of `matrix[5]`.
The <code>x</code> value in the Cartesian Coordinate System maps to the first index (The <code>row</code>) of an array matrix.
Therefore when you index into an array matrix and only specify a single index, such as in our previous example of `matrix[5]`,
 you are essentially taking a slice of all the values along the vertical axis at 5. On the level of code, this is represented
by slicing a single array out of an array of arrays. A matrix is nothing more than an array of arrays. Each inner array is
therefore a vertical slice of the overall matrix.</p>

<p>The horizontal values are represented by the second index within an array matrix (the <code>row</code> index).


      <pre>matrix[5][2]</pre>

    <pre>5 === x === row</pre>

    <pre>2 === y === column</pre>

This is not immediately intuitive until you start really white boarding out the
relationships between the two systems. </p>

<h2>Where the Model Breaks Down</h2>

<p>So far we have talked about the similarities between Cartesian coordinate system and an array matrix. Lets spend some time talking about the differences and where the modeling between the two begins to deteriorate.
In the cartesian coordinate system, the values at any particular point are intertwined with the coordinates themselves.
In other words, the value at a point where x = 3 and y = 5 would be (3, 5).
There is a direct relationship between the values at any given point, and the location of that point.
When talking about array matrices, this is not the case.
The location of a particular value in an array matrix has absolutely no relationship with the value at that point.
The values at locations are divorced from the numeric representation of the locations themselves.
In a sense, this adds something like a third dimension to the model of an array matrix that cartesian coordinates do not have.
 The consequences of this divorce between point values and point locations causes a sharp split between the 2 models.
Array matrices can represent negative values even in the space of positive coordinates. This needs to be th

e case since we are representing our matrix with an array, which has the limitation of only indexable by positive values.
This is why an array matrix is bounded at negative coordinates. </p>



