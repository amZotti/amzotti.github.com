---
layout: post
title: "How to Represent Decision Trees in Code"
description: "Permutation problems can be solved by using a decision tree. The depth of the 
decision tree represents the number of possible outcomes. The breadth of the
 decision tree represents the ordering in which decisions are made."
category: "computer science"
tags: [computer science, design patterns]
---
{% include JB/setup %}


<h1>Exploring Decision Trees</h1>
<p><a
href="http://www.mathsisfun.com/combinatorics/combinations-permutations.html">Permutation
problems</a> can be solved by using <a
href="http://en.wikipedia.org/wiki/Decision_tree">decision trees</a>. The depth of the 
decision tree represents the number of possible outcomes. The breadth of the
 decision tree represents the ordering by which decisions are made. In
programming, we can represent decision trees by using the <a
href="http://www.fas.harvard.edu/~cscie119/lectures/recursion.pdf">recursive
backtracking algorithm</a>.</p>

<h2>Recursive Backtracking Algorithm</h2>

<pre>
function recurse(depth) {
  //some basecase here
  for (var i = 0;i < breadth.length;i++) {
    applyValue(breadth[i]);
    recurse(breadth[i], depth++);
    removeValue(breadth[i]);
  }
}
</pre>

<p>This code represents generalization of the recursive backtracking
algorithm. This algorithm can be used to model decision trees. The depth of the
tree can be represented by the depth of the recursive stack. The breadth of the
tree can be represented by the number of iterations performed by the <code>for</code> loop
within each recursive stackframe. The actual decision making process can be
represented by the code within the <code>for</code> loop.</p>

<h2>Solving Permutation Problems using the Recursive Backtracking Algorithm</h2>
<p>Lets explore using the recursive backtracking algorithm to solve a permutation
problem. This is an algorithm I created for
finding all possible <a href="http://en.wikipedia.org/wiki/Anagram">anagrams</a>
of any given word:</p>

<pre>
function anagrams(originalString) {
  var resultStorage = {};
  
  (function recurse(buildUpString, originalString) {
    if (originalString === '') {
      resultStorage[buildUpString] = 1;
      return;
    }
    for (var i = 0;i < originalString.length;i++) {
      recurse(buildUpString + originalString[i], originalString.substring(0, i) + originalString.substring(i + 1));
    }
  })('', originalString);
  
  return Object.keys(resultStorage);
};

var anagrams = anagrams('abc');
console.log(anagrams); // [ 'abc', 'acb', 'bac', 'bca', 'cab', 'cba' ]
</pre>

<p>This solution follows the structure of the recursive backtracking algorithm
shown previously. As you can see it has a <code>for</code> loop
within a recursive function. Within the <code>for</code> loop there is code which controls how the final result is generated. 
The code within the <code>for</code> loop appears as though it
does not resemble the 3 lines of code from within the <code>for</code> loop of
the recursive backtracking algorithm, but in actuality this one
line of code is performing the behavior of all three of the lines of code from
within the recursive backtracking algorithm's <code>for</code> loop. The one line of code within the
<code>for</code> loop of the <code>anagrams</code> algorithms perform the
behavior of each one implicitly.</p>


<p>The <code>anagrams</code> solution contains 3 variables which are essential to its
structure as a decision tree. Algorithm's which represent decision tree often
have some form of these variables.</p>

<ol>
  <li><h3>resultStorage</h3></li>
    <p><code>resultStorage</code> is the variable which accumulates all the
values of the <code>buildUpString</code> variable that have passed the success
base case. if we are using a pure recursive
solution then this variable will not exist. In such a case, each branch of the
decision tree would just return it's own results to the previous branch.
All results would accumulate together as each stackframe returned.</p>
  <li><h3>buildUpString</h3></li>
    <p>The <code>buildUpVariable</code> initially starts off empty and accumulates more
values as the depth of the decision tree increases. When the final level of
decision tree is hit, which can be represented in code as hitting a base case, we add the
value of the <code>buildUpString</code> to <code>resultStorage</code>, then
traverse back up the decision tree by returning from stack frames.</p>
  <li><h3>originalString</h3></li>
<p>The <code>originalString</code> variable represents the initial value passed into the decision
tree which is the basis for what all possible permutations can be.</p>
</ol>

<h3>Bringing it all together</h3>
<p>On every recursive call, the
<code>buildUpString</code> gets bigger, and the <code>originalString</code> gets
smaller. When <code>originalString</code> has length 0, we add the
value of <code>buildUpString</code> to <code>resultStorage</code>. </p>

<p>Returning from recursive stack frames removes values from the
<code>buildUpString</code> 
in the order they were added to it. In essence, returning takes the values away from
the <code>buildUpString</code> and puts them back into
<code>originalString</code>. This process represents our traversal
back up the decision tree.</p>

<img src="http://xkcdsw.com/content/img/1105.gif"/>
