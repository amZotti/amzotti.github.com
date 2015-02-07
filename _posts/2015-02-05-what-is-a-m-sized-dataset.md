---
layout: post
title: "What is an m Sized Dataset?"
description: "A filled dataset is represented by the letter n. An unfilled
dataset is represented by a letter m"
category: "micropost"
tags: [computer science]
---
{% include JB/setup %}

<h1>MicroPost: Primer to Dataset Representation</h1>

<h3>Complete Dataset: n</h3>
<p>A dataset is nothing but a collection values. When measuring
complexity a dataset can be represented by the letter <code>n</code>. Below are a series of <a
href="http://rob-bell.net/2009/06/a-beginners-guide-to-big-o-notation/">efficientcy
classifications</a> along with syntax used to represent <code>n</code></p>

<img src="http://jsdo-it-static-contents.s3.amazonaws.com/images/capture/n/t/P/ntPo.jpg?t=1312505692"/>

<h3>Incomplete Dataset: m</h3>
<p><code>n</code> represents a dataset which is full, but what if we want to represent a
dataset that is not full? An unfilled dataset can be referred to using the letter
<code>m</code>. Suppose we have an Array
with 10 positions but only 6 of those positions have values, and all other
positions are null (no reference). An unfilled dataset can be represented by the
letter <code>m</code>. <code>m</code> represents a dataset which is either not
full or only partially full.</p>
