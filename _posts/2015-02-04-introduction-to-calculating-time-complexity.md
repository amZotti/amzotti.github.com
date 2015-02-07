---
layout: post
title: "Introduction to Calculating Time Complexity"
description: "Time complexity is a measurement of how a given algorithm's efficiency
scales relative to a given dataset as the dataset increases towards infinity. Time complexity
is not concerned with the actual clock time required to run an algorithm."
category: "computer science"
tags: [computer science]
---
{% include JB/setup %}

<h1>Time Complexity and Efficiency Classifications</h1>
<p>Time complexity is a measurement of how a given algorithm's efficiency
scales relative to a given dataset as the dataset increases towards infinity. Time complexity
is not concerned with the actual clock time required to run an algorithm. Time
complexity is concerned solely with how the relative time to execute changes
when the size of the dataset changes. Big O notation essentially asks the
question of <blockquote>"What is the worst thing
that could happen?"</blockquote>Complexity is usually measured in Big
O notation, although there <i>are</i>  <a
href="https://www.youtube.com/watch?v=I7p2C4oJygo">other less frequently notations that can
be used to measure complexity instead:</a></p>
<ul>
<li><b>Big Omega</b> <i>Best case</i></li>
<li><b>Big Theta</b> <i>Tight bound between BigO and Big Omega</i></li>
<li><b>BigO</b> <i>Worst case</i></li>
</ul>

<h1>How to Calculate Time Complexity</h1>
To calculate time complexity, all we need to do is count the number of
comparisons and assignments that are taking place in our program and add them
together. However, we are not counting simply the lines of code, we are counting
the number of times those lines of code are executed. So if we have a program
that iterates through a list of values and adds one to each one, the time
complexity would be O(n). That is, the number of operations is roughly
proportional to the size of the data set. If we have a loop that iterates
through the entire data set, and on every iteration it performed 5 expressions,
then we would still have O(n) because we drop constants and round our
calculation to the nearest order of magnitude.</p>

<pre>
function double(array) {
  return array.map(function(element) {
    return element * 2;
  });
}
var test1 = [1,2,3,4,5];
double(test1);
</pre>

<p>This iterates over our entire data set once. Therefore the result would be
O(n)</p>

<ul>
  <li><b>A statement, conditional, or expression</b> 1</li>
  <li><b>Recursively splitting a dataset in half on every iteration</b>
O(log(n))</li>
  <li><b>Iterating over a dataset</b> O(n)</li>
  <li><b>Iterating over a nested dataset</b> O(n<sup>2</sup>)</li>
</ul>

<img src="http://www.college-code.com/blog/wp-content/uploads/2008/05/big_o_table.png"/>
